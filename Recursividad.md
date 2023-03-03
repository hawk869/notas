```
public class Main {  
    public static void main(String[] args) {  
//        System.out.println(factorialRecursion(4));  
        hanoi(2,"Origen","Destino","Auxiliar");  
    }  
// recursividad nivel basico  
    static void countdown(int number){  
        System.out.println(number);  
        if (number > 0)  
            countdown(number - 1 );  
        else  
            System.out.println("Boom!");  
    }  
//    recursividad nivel medio  
    static double factorialRecursion(double number){  
        if (number > 1)  
            number *= factorialRecursion(number - 1);  
        return number;  
    }  
//    recursividad nivel avanzado  
    static void hanoi(int cantidad, String torre1, String torre2, String torre3){  
        if (cantidad > 0){  
            hanoi(cantidad - 1, torre1, torre3, torre2);  
            System.out.println("Disco de la posicion " + torre1 + " hasta " + torre2);  
            hanoi(cantidad - 1, torre3, torre2, torre1);  
        }  
    }}
```
