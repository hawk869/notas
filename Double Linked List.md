1. Creamos el nodo, que va a ser de tipo generico, va a contener la data y los punteros con la informacion del nodo anterior y el siguiente 

```
public class Node<T extends Comparable<T>> {  
  
    private T data;  
//    this es even more memory heavy than single linked list  
    private Node<T> nextNode;  
    private Node<T> previousNode;  
  
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
  
    public Node<T> getPreviousNode() {  
        return previousNode;  
    }  
  
    public void setPreviousNode(Node<T> previousNode) {  
        this.previousNode = previousNode;  
    }  
  
    @Override  
    public String toString() {  
        return "" + data;  
    }  
}
```

2. Luego creamos la clase DoubleLimkedList que igualmente va a ser generica y va apuntar al head y al tail, va a tener los metodos de insertar data en la lista, ademas va a incluir los metodos de recorrer la lista en ambos sentidos

```
public class DoubleLinkedList<T extends Comparable<T>> {  
  
    private Node<T> head;  
    private Node<T> tail;  
  
    public void insert(T data){  
        Node<T> newNode = new Node<>(data);  
//        this is the first item in the list  
        if (tail == null){  
//            both of the pointers arepointing to the new node  
            tail = newNode;  
            head = newNode;  
        } else {  
//            we insert new item to the end of the list  
            newNode.setPreviousNode(tail);  
            tail.setNextNode(newNode);  
            tail = newNode;  
        }  
    }//    let's traverse the list forward  
    public void traverseForward(){  
        Node<T> actualNode = head;  
        while (actualNode != null){  
            System.out.println(actualNode);  
            actualNode = actualNode.getNextNode();  
        }  
    }    //    let's traverse the list backward  
    public void traverseBackward(){  
        Node<T> actualNode = tail;  
        while (actualNode != null){  
            System.out.println(actualNode);  
            actualNode = actualNode.getPreviousNode();  
        }  
    }}
```

3. Luego en la clase main vamos a insertar la data a la lista que para este caso van a ser de tipo strings

```
public class Main {  
    public static void main(String[] args) {  
  
        DoubleLinkedList<String> names = new DoubleLinkedList<>();  
  
        names.insert("Daniel");  
        names.insert("Pedro");  
        names.insert("Juan");  
        names.insert("Camila");  
        names.insert("Ana");  
  
        names.traverseBackward();  
    }  
}
```
4. Tambien se puede implementar la clase LinkedList de Java que ya viene con metodos creados
```
LinkedList<String> dll = new LinkedList<>();

dll.addFirst("Daniel");
dll.addFirst("Ana");
dll.addFirst("Kevin");

for(String name: dll)
	System.out.println(name);
	
```

```
import java.util.LinkedList;  
  
public class Main {  
    public static void main(String[] args) {  
  
        LinkedList<String> dll = new LinkedList<>();  
  
        dll.addLast("Ana");  
        dll.addLast("Daniel");  
        dll.addLast("Camila");  
  
        dll.removeFirst();  
  
        for (String name: dll)  
            System.out.println(name);  
    }  
}
```

## Haciendo una prueba de tiempo comparando Arrays vs linked list

La prueba se hace comparando la insercion de datos en la primera posicion
```
import java.util.ArrayList;  
import java.util.LinkedList;  
  
public class Main {  
    public static void main(String[] args) {  
  
        ArrayList<Integer> array = new ArrayList<>();  
        long now = System.currentTimeMillis();  
  
        for (int i=0; i<500000; i++)  
            array.add(0,i);  
  
        System.out.println("Time taken for ArrayList: " + (System.currentTimeMillis() - now));  
  
        LinkedList<Integer> list = new LinkedList<>();  
        now = System.currentTimeMillis();  
  
        for (int i=0; i<500000; i++)  
            list.addFirst(i);  
  
        System.out.println("Time taken for LinkedList: " + (System.currentTimeMillis() - now));  
    }  
}
```

Para este caso especifico la LinkedList es mas rapida:
```
Time taken for ArrayList: 11740
Time taken for LinkedList: 29
```

Pero si queremos comparar la insercion agregando el nuevo item al final, van a ser igual de rapidos ambos metodos
```
Time taken for ArrayList: 8
Time taken for LinkedList: 30
```
