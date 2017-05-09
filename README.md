# jeff-trabalho1

package matrixGenerator;
import java.io.BufferedReader;
import java.io.File;
import java.io.FileReader;
import java.io.IOException;
import java.util.Scanner;
import java.util.Stack;

/* 
 * 
 * https://en.wikipedia.org/wiki/Flood_fill

10 10
0110011111
1000110101
1000011001
1100000001
1011100000
1011100110
0000100111
0001100101
1110010001
1011110101

*/

public class Main {
	
	public static void main(String [] args){
	
		int[][] numArray;
		
	try {
		File file = new File("src/matrixGenerator/teste.txt");
		FileReader fileReader = new FileReader(file);
		BufferedReader bufferedReader = new BufferedReader(fileReader);
		StringBuffer stringBuffer = new StringBuffer();
		String 	line = bufferedReader.readLine();
		//String pulaCabecalho =  bufferedReader.readLine();	
			
		//Tamanho da matrix
		String[] dimensao = line.split("\\s+");
		  int rows = Integer.parseInt(dimensao[0]);
	        int cols = Integer.parseInt(dimensao[1]);

	    	//System.out.println(dimensao[0]);
	    	//System.out.println(dimensao[1]);
	                        
	        numArray = new int[rows][cols];
	        
	        int row = 0;
	        
	        while ((line = bufferedReader.readLine()) != null){
	           String[] tokens = line.split("");
	            
	            
	            for(int column = 0; column < tokens.length; column++) {
	               
	                    int value = Integer.parseInt(tokens[column]);
	                    numArray[row][column] = value; 
	            }
	            row++;
	            
	        }            
	       // printaMatrix(numArray);	
	        //System.out.println();

	        
		fileReader.close();
		
		contaIlhas(numArray);
		
		int numOfIslands = contaIlhas(numArray);
		//numero de ilhas é:
		System.out.println(+numOfIslands);
		
		} catch (IOException e) {}	
	}
	
	public static void printaMatrix(int[][] numArray){

	 for (int row = 0; row < numArray.length; row++) {
	        for (int column = 0; column < numArray[row].length; column++) 
	        {
	            System.out.print(numArray[row][column]);
	        }
	        System.out.println();
	 	}
	 
	   //main2() ;

	} 
	

////////////////////////////////////////	


	public static int contaIlhas(int[][] numArray) {
		boolean[][] checked = new boolean[numArray.length][numArray.length];
		for (int i = 0; i < numArray.length; i++) {
			for (int j = 0; j < numArray.length; j++) {
				checked[i][j] = false;
			}
		}

		
		//int[][] numArrayTeste = numArray; //
		
		int totalIlhas = 0;
		for (int i = 0; i < numArray.length; i++) {
			for (int j = 0; j < numArray.length; j++) {
				if (checked[i][j]) 						
					continue;
				if (numArray[i][j] == 0) {
					checked[i][j] = true;
					
					//
					//numArrayTeste[i][j] = 1;
					//System.out.println(numArrayTeste[i][j]);
					//
							
					continue;
				}
				totalIlhas++;
				floodFill(i, j, numArray, checked); 
			}
		}
		return totalIlhas;
	}
	
	public static void floodFill(int row, int col, int[][] sea, boolean[][] checked) {
		if (sea[row][col] == 0 || checked[row][col]) return;
		checked[row][col] = true;
		if (col < sea.length - 1) floodFill(row, col+1, sea, checked);
		if (row < sea.length - 1) floodFill(row+1, col, sea, checked);
		if (col > 0) floodFill(row, col-1, sea, checked);
		if (row > 0) floodFill(row-1, col, sea, checked);
	}


}
