Las colas son estructuras de datos abstratas, los sistemas operativos son los que mas emplean este tipo de estructuras, emplea FIFO, significa que el primer elemento en entrar es el primero en salir.

Para implementar una Queue creamos una clase Node con dos campos Data de tipo generico, y un puntero que apunta al siguiente nodo
```
public class Node<T extends Comparable<T>> {  
  
    private T data;  
    private Node<T> nextNode;  
  
    public Node(T data) {  
        this.data = data;  
    }  
  
    public T getData() {  
        return data;  
    }  
  
    public void setData(T data) {  
        this.data = data;  
    }  
  
    public Node<T> getNextNode() {  
        return nextNode;  
    }  
  
    public void setNextNode(Node<T> nextNode) {  
        this.nextNode = nextNode;  
    }  
  
    @Override  
    public String toString() {  
        return this.data.toString();  
    }  
}
```

La clase Queue quedaria
```
public class Queue<T extends Comparable<T>> {  
  
    private Node<T> firstNode;  
    private Node<T> lastNode;  
    private int count;  
    public boolean isEmpty() {  
        return this.firstNode == null;  
    }  
    public int size() {  
        return this.count;  
    }  
    public void enqueue(T newData) {  
  
        this.count ++;  
        Node<T> oldLastNode = this.lastNode;  
        this.lastNode = new Node<>(newData);  
        this.lastNode.setNextNode(null);  
  
        if (isEmpty()) {  
            this.firstNode = this.lastNode;  
        } else {  
            oldLastNode.setNextNode(this.lastNode);  
        }  
    }    public T dequeue() {  
        this.count --;  
        T dataToDequeue = this.firstNode.getData();  
        this.firstNode = this.firstNode.getNextNode();  
        if (isEmpty()) {  
            this.lastNode = null;  
        }   
return dataToDequeue;  
    }  
}
```

La implementacion en el metodo main quedaria
```
public class Main {  
    public static void main(String[] args) {  
  
        Queue<Integer> myQueue = new Queue<>();  
  
        myQueue.enqueue(10);  
        myQueue.enqueue(100);  
        myQueue.enqueue(1000);  
  
        System.out.println(myQueue.size());  
  
        System.out.println(myQueue.dequeue());  
        System.out.println(myQueue.dequeue());  
        System.out.println(myQueue.dequeue());  
    }  
}
```

Igualmente Java ya viene con una interface llamada Queue que tiene ya implementado estos metodos
```
import java.util.LinkedList;  
import java.util.Queue;  
  
public class Main {  
    public static void main(String[] args) {  
  
        Queue<Integer> queue = new LinkedList<>();  
  
        queue.add(1);  
        queue.add(2);  
        queue.add(3);  
  
        System.out.println(queue.element());  
        System.out.println(queue.size());  
  
        while (!queue.isEmpty()) {  
            System.out.println(queue.remove());  
        }  
    }  
}
```

### Solucion al problema devolver el maximo valor de un stack:

para esto creamos dos stacks, uno va a ser el principal, y el otro va almacenar el valor mas grande, estonces cada vez que insertamos un valor en el mainStack vamos a comparar con el valor del maxStack, si es menor vamos a duplicar el valor en el maxStack
```
import java.util.Stack;  
  
public class MaxItemStack {  
  
    private Stack<Integer> mainStack;  
    private Stack<Integer> maxStack;  
  
    public MaxItemStack() {  
        this.mainStack = new Stack<>();  
        this.maxStack = new Stack<>();  
    }  
    public void push(int item) {  
        mainStack.push(item);  
        if (mainStack.size()==1) {  
            maxStack.push(item);  
            return;  
        }  
        if (item>maxStack.peek()) {  
            maxStack.push(item);  
        } else {  
            maxStack.push(maxStack.peek());  
        }  
    }    public int pop() {  
        maxStack.pop();  
        return mainStack.pop();  
    }  
    public int getMaxItem() {  
        return maxStack.peek();  
    }  
}
```

### Implementar una cola con stacks

```
import java.util.Stack;  
  
public class QueueProblem {  
  
    private Stack<Integer> enqueueStack;  
    private Stack<Integer> dequeueStack;  
    public QueueProblem() {  
        this.dequeueStack = new Stack<>();  
        this.enqueueStack = new Stack<>();  
    }  
    public void enqueue(int item) {  
        this.enqueueStack.push(item);  
    }  
    public int dequeue(int item) {  
        if (enqueueStack.isEmpty() && dequeueStack.isEmpty())  
            throw new RuntimeException("Stacks are empty");  
  
        if (dequeueStack.isEmpty()) {  
            while (!enqueueStack.isEmpty()){  
                dequeueStack.push(enqueueStack.pop());  
            }  
        }        return dequeueStack.pop();  
    }  
}
```

### Resolviendo problema con recursion
```
import java.util.Stack;  
  
public class OneStackQueue {  
    private Stack<Integer> stack;  
    public OneStackQueue() {  
        this.stack = new Stack<>();  
    }  
    public void enqueue(int item) {  
        this.stack.push(item);  
    }  
    public int dequeue() {  
        if (stack.size() == 1)  
            return stack.pop();  
        int item = stack.pop();  
        int lastDequeueItem = dequeue();  
        enqueue(item);  
        return lastDequeueItem;  
    }  
}
```

Luego implementamos en la clase main
```
public class Main {  
    public static void main(String[] args) {  
  
        OneStackQueue oneStackQueue = new OneStackQueue();  
  
        oneStackQueue.enqueue(10);  
        oneStackQueue.enqueue(5);  
        oneStackQueue.enqueue(20);  
  
        System.out.println(oneStackQueue.dequeue());  
  
        oneStackQueue.enqueue(100);  
  
        System.out.println(oneStackQueue.dequeue());  
        System.out.println(oneStackQueue.dequeue());  
        System.out.println(oneStackQueue.dequeue());
     }
 }       
```