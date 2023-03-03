En español pilas, tiene una estructura LIFO (last in firt out) el primer elemento apunta a un null, cuando se ingresa un nuevo elemento este va apuntar al primer elemento, el ultimo elemento en ingresar es el primero en ser eliminado,

## Operaciones Basicas
pop() elimina el ultimo elemento y lo devuelve
push() ingresa un elemento al final de la estructura
peek() trae el ultimo elemento sin eliminarlo

Existen dos tipos de memoria RAM, stack y heap, stack se usa para guardar variables y funciones, su acceso es mas rapido pero es de un tamaño mas pequeño, heap tiene un tamaño mas grande, el acceso es mas lento, y sirve para instanciar clases, por ende va almacenar objetos, la referencia de un objeto se va a guardar en la stack memory pero el objeto como tal se almacena en la heap memory

### Implementacion en codigo

Se crea una clase generica, este va a ser el nodo y va contener la informacion
```
public class Node<T> {  
  
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
        return "" + data;  
    }  
}
```

Luego se crea la clase Stack que va a tener dos parametros, y cuatro funciones
```
public class Stack<T> {  
  
//    the LIFO last item we inserted is the first one we take out  
//    when the pop() method is called  
    private Node<T> head;  
    private int count;  
    public void push(T data){  
        count++;  
        if (head == null) {  
            head = new Node<>(data);  
        } else {  
            Node<T> oldNode = head;  
            head = new Node<>(data);  
            head.setNextNode(oldNode);  
         }  
    }    
    public T pop(){  
		if (isEmpty()) return null;
        T item = head.getData();  
        head = head.getNextNode();  
        count--;  
        return item;  
    }  
    public int size(){  
        return count;  
    }  
    public boolean isEmpty(){  
        return count == 0;  
    }  
}
```

Para implementar esta solucion hacemos lo siguiente
```
public class Main {  
    public static void main(String[] args) {  
  
        Stack<String> names = new Stack<>();  
  
        names.push("Daniel");  
        names.push("Juan");  
        names.push("Camila");  
        names.push("Ana");  
  
        while (!names.isEmpty()) {  
            System.out.println(names.pop());  
        }  
    }}
```

### Implementacion de Stack con Arrays
Creamos una clase generica con dos elementos, un array generico, como los Arrays no pueden extender de un generico en el constructor se extiende de Object, cuando se implementa el metodo push() si el elemento count es igual al largo del array se crea un metodo para apliar el tamaño del mismo, ya que los arrays no son dinamicos.
Para el metodo pop() se devuelve el item que se remueve y si es necesario se reduce el tamaño del array
```
public class Stack<T> {  
  
    private T[] stack;  
    private int count;  
  
    public Stack() {  
        stack = (T[]) new Object[1];  
    }  
    public T pop() {  
        if (isEmpty()) return null;  
        T item = stack[--count];  
        stack[count] = null;  
        if (count > 0 && count == stack.length/4)  
            resize(stack.length/2);  
        return item;  
    }  
    public boolean isEmpty(){  
        return count == 0;  
    }  
    public int size(){  
        return count;  
    }  
    public void push(T newData) {  
//        Arrays are not dinamic data structures  
//        we have to resize the underline array if necessary  
        if (count == stack.length)  
            resize(2*stack.length);  
        stack[count++] = newData;  
    }  
    private void resize(int capacity) {  
        T[] stackCopy = (T[]) new Object[capacity];  
        for (int i=0; i<count; i++){  
            stackCopy[i] = stack[i];  
        }  
        stack = stackCopy;  
    }  
}
```

La implementacion en el metodo main quedaria
```
public class Main {  
    public static void main(String[] args) {  
  
        Stack<Integer> nums = new Stack<>();  
  
        nums.push(1);  
        nums.push(2);  
        nums.push(3);  
        nums.push(4);  
        nums.push(5);  
        nums.push(6);  
  
        while (!nums.isEmpty())  
            System.out.println(nums.pop());  
    }  
}
```

### Dijkstra Interpreter Implementacion

```
import java.util.Stack;  
  
public class Algoritmo {  
  
    private Stack<String> operationStack;  
    private Stack<Double> valueStack;  
  
    public Algoritmo() {  
        this.operationStack = new Stack<>();  
        this.valueStack = new Stack<>();  
    }  
    public void interpreterExpresion(String expresion) {  
        String[] expresionArray = expresion.split(" ");  
        for (String s: expresionArray){  
            if (s.equals("(")){  
            } else if (s.equals("+")) {  
                this.operationStack.push(s);  
            } else if (s.equals("*")) {  
                this.operationStack.push(s);  
            } else if (s.equals(")")) {  
                String operation = this.operationStack.pop();  
                if (operation.equals("+")){  
                    this.valueStack.push(this.valueStack.pop() + this.valueStack.pop());  
                } else if (operation.equals("*")) {  
                    this.valueStack.push(this.valueStack.pop() * this.valueStack.pop());  
                }  
            } else {  
                this.valueStack.push(Double.parseDouble(s));  
            }  
        }    }    public void result() {  
        System.out.println(this.valueStack.pop());  
    }  
}
```

```
public class Main {  
    public static void main(String[] args) {  
  
        Algoritmo algoritmo = new Algoritmo();  
  
        algoritmo.interpreterExpresion("( ( 1 + 2 ) * ( 2 + 1 ) )");  
  
        algoritmo.result();  
    }  
}
```