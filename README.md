# HW_ProgrammingParadigms
Java
import java.util.Arrays;
import java.util.stream.Collectors;
import java.util.List;

public class Main
{
	public static void main(String[] args) {
		int[] numbers = {8,2,17,1,9,5};
		
	
	   //императивное прогр.
		bubbleSortForDecreasing(numbers);
		System.out.println("Sorted List for decreasing by Itterative Method: ");
		for(int number: numbers){
		    System.out.print(number + " ");
		}
		
		//декларативное прогр.
		int[] reverseSorttedNumbers = Arrays.stream(numbers)
		                              .boxed()
		                              .sorted((a,b) -> b.compareTo(a))
		                              .mapToInt(Integer::intValue)
		                              .toArray();
		
		System.out.println();
		System.out.println("Sorted List for decreasing by Declarative Method: ");
		String result = Arrays.stream(reverseSorttedNumbers)
		                       .mapToObj(String::valueOf)
		                       .collect(Collectors.joining(" "));
		System.out.println(result);
		
	}
	
	//Метод пузырьковой сортировки для императивного программирования на практике
	public static void bubbleSortForDecreasing(int list[]) {
        int l = list.length;
        for(int i = 0; i < l - 1; i++){
            for(int j = 0; j < l - i - 1; j++){
                if(list[j] < list[j+1]){
                    int temp = list[j];
                    list[j] = list[j+1];
                    list[j+1] = temp;
                }
            }
        }
	}
	
	
}





---------------------------------
HW02


import java.util.Scanner;

public class Main {
    
    public static void main(String[] args){
        Scanner scanner = new Scanner(System.in);
        System.out.print("Please input number n for multiply:  ");
        int n = scanner.nextInt();
        
        multiplyTableCalc(n);
    }
    
    public static void multiplyTableCalc(int num) {
        for(int i = 1; i < num + 1; i++){
            for (int j = 1; j < num + 1; j++){
                int count = i * j;
               System.out.printf("%d * %d = %d \t", i,  j, count);
            }
    
            System.out.println();
        }
        
    }
    
}


-------------------------
HW04

import java.util.Arrays;
import java.util.stream.IntStream;


class Main {
    
     public static void main(String[] args){
         int[] x = {1, 2, 3, 4, 5};
         int[] y = {4, 7, 6, 2, 1};

        double correlation = calculatePearsonCorr(x, y);
        System.out.println("Pearson correlation: " + correlation);
     }


 // Функциональная парадигма в данном случае упрощает вычисления и делает код более компактным.
 // Императивные программы имеют склонность акцентировать последовательности шагов 
 //для выполнения какого-то действия, а функциональные программы к расположению 
 //и композиции функций, часто не обозначая точной последовательности шагов.
    public static double calculatePearsonCorr(int[] x, int[] y){
          
        double sumX = Arrays.stream(x).sum();
        double sumY = Arrays.stream(y).sum();
        // императивный:
        //double sumX = 0;
        //    for (int i = 0; i < x.length; i++) {
        //         sumX += x[i];
        //    }
        
        double sumXSq = Arrays.stream(x).mapToDouble(a -> a * a).sum();
        double sumYSq = Arrays.stream(y).mapToDouble(a -> a * a).sum();
        // императивный:
        //double sumXSq = 0;
        //    for (int i = 0; i < x.length; i++) {
        //         sumXSq += x[i] * x[i];
        //    }
        

        double sumProdXY = IntStream.range(0, x.length).mapToDouble(i -> x[i] * y[i]).sum();
        // императивный:
        //double sumProdXY = 0;
        //    for (int i = 0; i < x.length; i++) {
        //         sumProdXY += x[i] * y[i];
        //    }
        
        double numerator = sumProdXY - sumX * sumY;
        
        double denominator = Math.sqrt((sumXSq - Math.pow(sumX, 2)) * (sumYSq - Math.pow(sumY, 2)));
        
        
        if (denominator == 0) {
            return 0; // если знаменатель равен нулю, корреляция будет равна 0
        } return numerator / denominator;

    }
        
    }
