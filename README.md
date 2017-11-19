# Question-7
Data Analysis for Question 7


import java.util.Arrays;

public class Test {
	
	static int[] rangeArray = new int[] {0, 0, 0, 0, 0};
	//T he array that will print out at the end with percentages for each salary range
	
	static int decimal = 10000;
	//How many decimal places the data are shown as
	// 100 = xx% 
	// 10000 = xx.xx%
	
	public static void addtoArray(int lower, int higher) {
		
		if (lower > higher) {
			System.out.println("Error: Start should be less than or equal to rangeEnd");
		}
		// Checks if the input ranges are ordered correctly
		
		for (int i=0, j=30000; i < rangeArray.length; i++, j+=10000) {
			// checks the imput for each salary range starting with 30000 - 39999
			if (lower >= j) {
					
				if (higher <= j+10000) {
					// checks if the input range is within 
					// a single salary range of the array
					
					if (lower-j == (j+10000)-higher) {
						rangeArray[i] += 100;
					}
					// adds 100% to a salary range if the input is 
					// distributed directly in the middle of the range
					// i.e. 44000-46000, 45000-45000, 50000-60000
						
					else {
						int low = (lower+higher)/2 -5000;
						int high = (lower+higher)/2 +5000;
						addtoArray(low, high);
						break;
					}
					// if the input range is skewed towards one end of a salary range, 
					// expands the input range to cover multiple salary ranges and runs the loop recursively
					// i.e. 40000-45000 becomes 37500-47500
					// this provides for more accurate data when put on a graph
				}
					
				if (lower < j+10000) {
					int total = higher - lower;
					int lowdif = j+10000 - lower;
					int perc = (lowdif*decimal)/total;
					rangeArray[i]+= perc;
				}
				// if lowest part of an input range falls within a salary range,
				// calcuates the percentage of the input range to add to the salary range
			}
				
			else if (higher >= j+10000) {
				int total = higher - lower;
				int perc = (10000*decimal)/total;
				rangeArray[i]+= perc;
			}
			// if 
			
			else if (higher > j && higher <= j+10000) {
				int total = higher - lower;
				int highdif = higher - j;
				int perc = (highdif*decimal)/total;
				rangeArray[i]+= perc;
			}
		}
	}
	public static void printArray() {
		System.out.println("30,000 - 39,999 = " + rangeArray[0]);
		System.out.println("40,000 - 49,999 = " + rangeArray[1]);
		System.out.println("50,000 - 59,999 = " + rangeArray[2]);
		System.out.println("60,000 - 69,999 = " + rangeArray[3]);
		System.out.println("70,000 - 79,999 = " + rangeArray[4]);
	}
	public static void main(String[] args) {
		addtoArray(40000, 45000);
		addtoArray(40000, 70000);
		addtoArray(40000, 40000);
		printArray();
	}

}
