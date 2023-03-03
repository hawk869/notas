Son estructuras de datos que son capaces de guardar items de manera eficiente, porque los objetos se guardan en orden, los arboles binarios tienen un nodo padre y este a su vez tiene un maximo de dos nodos hijos, de esta forma cuando de busca un item se reduce a la mitad del arbol, siempre y cuando este arbol este balanceado

## Implementacion

Creamos una clase Node
```
public class Node<T> {  
    private T data;  
    private Node<T> leftChild;  
    private Node<T> rightChild;  
    private Node<T> parentNode;  
    public Node(T data, Node<T> parentNode) {  
        this.data = data;  
        this.parentNode = parentNode;  
    }  
  
    public T getData() {  
        return data;  
    }  
  
    public void setData(T data) {  
        this.data = data;  
    }  
  
    public Node<T> getLeftChild() {  
        return leftChild;  
    }  
  
    public void setLeftChild(Node<T> leftChild) {  
        this.leftChild = leftChild;  
    }  
  
    public Node<T> getRightChild() {  
        return rightChild;  
    }  
  
    public void setRightChild(Node<T> rightChild) {  
        this.rightChild = rightChild;  
    }  
  
    public Node<T> getParentNode() {  
        return parentNode;  
    }  
  
    public void setParentNode(Node<T> parentNode) {  
        this.parentNode = parentNode;  
    }  
  
    @Override  
    public String toString() {  
        return "" + data;  
    }  
}
```

Luego creamos una interface Tree
```
public interface Tree<T> {  
  
    public void insert(T data);  
    public void remove(T data);  
    public void traversal();  
    public T getMin();  
    public T getMax();  
}
```

Luego creamos la clase que va a implementar esta interface
Para esto creamos una variable que va a representar el rootnode de tipo node e importamos el metodo insert de la interface
```
@Override  
public void insert(T data) {  
    if (rootNode==null){  
        rootNode = new Node<>(data, null);  
    } else {  
        insert(data, rootNode);  
    }  
}  
  
private void insert(T data, Node<T> node) {  
    if (node.getData().compareTo(data) > 0){  
        if (node.getLeftChild() != null)  
            insert(data, node.getLeftChild());  
        else  
            rootNode.setLeftChild(new Node<>(data, node));  
    } else {  
        if (node.getRightChild() != null)  
            insert(data, node.getRightChild());  
        else  
            node.setRightChild(new Node<>(data, node));  
    }  
}
```

Modificamos el metodo getMax que es para obtener el valor maximo
```
@Override  
public T getMax() {  
    if (rootNode==null)  
        return null;  
    return getMax(rootNode);  
}  
  
private T getMax(Node<T> node) {  
    if (node.getRightChild() != null)  
        return getMax(node.getRightChild());  
    return node.getData();  
}
```

El metodo getMin() quedaria
```
@Override  
public T getMin() {  
    if (rootNode==null)  
        return null;  
    return getMin(rootNode);  
}  
  
private T getMin(Node<T> node) {  
    if (node.getLeftChild() != null)  
        return getMin(node.getLeftChild());  
    return node.getData();  
}
```

El metodo traversal
