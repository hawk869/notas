## Middle Node in Linked Lists

Para encontrar el punto medio de una lista creamos dos punteros, uno va a viajar al doble de velocidad del otro y cuando cuando este llegue al final, el mas lento va a estar en la mitad de la lista 
```
public Node<T> getMiddleNode(){  
    Node<T> slow = this.root;  
    Node<T> fast = this.root;  
    while (fast.getNextNode() != null && fast.getNextNode().getNextNode() != null){  
        slow = slow.getNextNode();  
        fast = fast.getNextNode().getNextNode();  
    }  
    return slow;  
}
```

## Reversed a Linked List

```
public void reverse() {  
    Node<T> currentNode = this.root;  
    Node<T> previousNode = null;  
    Node<T> nextNode = null;  
    while (currentNode != null) {  
        nextNode = currentNode.getNextNode();  
        currentNode.setNextNode(previousNode);  
        previousNode = currentNode;  
        currentNode = nextNode;  
    }  
    this.root = previousNode;  
}
```