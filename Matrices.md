```
public class ProductoMA {  
    public static void main(String[] args) {  
        int matrizA[][] = {{3,1,-2}, {0,4,2}, {7,5,1}};  
        int matrizB[][] = {{-1,0,8}, {3,6,9}, {0,0,3}};  
        int matrizResultado[][] = new int[3][3];  
  
        for (int i=0; i < 3; i++){  
            for (int j=0; j<3; j++){  
                matrizResultado[i][j] = matrizA[i][0]*matrizB[0][j] + matrizA[i][1]*matrizB[1][j] + matrizA[i][2]*matrizB[2][j];  
            }  
        }       
         showMatriz(matrizA);  
        System.out.println();  
        showMatriz(matrizB);  
        System.out.println();  
        showMatriz(matrizResultado);  
  
//  loop para domino  
//        for (int i=0; i<7; i++){  
//            for (int j=0+i; j<7; j++){  
//                System.out.print(i+"|"+j+" ");  
//            }  
//            System.out.println();  
//        }  
    }  
    static void showMatriz(int matriz[][]){  
        for (int i=0; i< matriz.length; i++){  
            for (int j=0; j<matriz[i].length; j++){  
                System.out.print(matriz[i][j]+"\t");  
            }  
            System.out.println();  
        }  
    }
    }
```

## Matrices dinamicas
Tiene que ser un array de punteros donde cada elemento a punta a un array especifico:

array padre

[ ]     => 3 elementos              
[ ]     => 5 elementos
[ ]     => 4 elementos

