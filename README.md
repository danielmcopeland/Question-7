# Question-7
Data Analysis for Question 7


import java.util.Arrays;

public class Test {
	
	static float[] rangeArray = new float[] {0, 0, 0, 0, 0, 0};
		//The array showing the # of responses for each salary range
	
	static float[] percArray = new float[] {0, 0, 0, 0, 0, 0};
		//The array showing the percentages of responses for each salary range
	
	static int[] badArray = new int[] {0, 0, 0, 0, 0, 0};
		//The array showing the Colazzi's Method and its inaccuracy
	
	static float[] badPercArray = new float[] {0, 0, 0, 0, 0, 0};
		//The array showing the Colazzi's Method percentages of responses for each salary range
	
	public static void addtoArray(float lower, float higher) {
		addtoRangeArray(lower, higher);
		addtoBadArray(lower, higher);
	}
		//passes input ranges to both arrays
	
	public static void addtoRangeArray(float lower, float higher) {
		if (lower > higher) {
			System.out.println("Error: Start should be less than or equal to rangeEnd");
		}
		// Checks if the input ranges are ordered correctly
		
		for (int i=0, j=30000; i < rangeArray.length; i++, j+=10000) {
			// checks the input for each salary range starting with 30000 - 39999
			if (lower >= j) {
					
				if (higher <= j+10000) {
					// checks if the input range is within 
					// a single salary range of the array
					
					if (lower-j == (j+10000)-higher) {
						rangeArray[i] += 1;
					}
					// adds 100% to a salary range if the input is 
					// distributed directly in the middle of the range
					// i.e. 44000-46000, 45000-45000, 50000-60000
						
					else {
						float low = (lower+higher)/2 -5000;
						float high = (lower+higher)/2 +5000;
						addtoArray(low, high);
						break;
					}
					// if the input range is skewed towards one end of a salary range, 
					// expands the input range to cover multiple salary ranges and runs the loop recursively
					// i.e. 40000-45000 becomes 37500-47500
					// this provides for more accurate data when put on a graph
				}
					
				else if (lower < j+10000) {
					float total = higher - lower;
					float lowdif = j+10000 - lower;
					float perc = (lowdif)/total;
					rangeArray[i]+= perc;
				}
				// if lowest part of an input range falls within a salary range,
				// calculates the percentage of the input range to add to the salary range
			}
				
			else if (higher >= j+10000) {
				float total = higher - lower;
				float perc = (10000)/total;
				rangeArray[i]+= perc;
			}
			// if the input range contains a salary range completely,
			// calculates the percentage of the input range to add to the salary range
			
			else if (higher > j && higher <= j+10000) {
				float total = higher - lower;
				float highdif = higher - j;
				float perc = (highdif)/total;
				rangeArray[i]+= perc;
			}
			// if highest part of an input range falls within a salary range,
			// calculates the percentage of the input range to add to the salary range
		}
	}
		//passes input ranges to rangeArray
	
	public static void addtoBadArray(float lower, float higher) {
		if (lower > higher) {
			System.out.println("Error: Start should be less than or equal to rangeEnd");
		}
		for (int i=0, j=30000; i < badArray.length; i++, j+=10000) {
				if (lower >= j) {
					if (lower < j+10000) {
					badArray[i]++;
					}
				}
				else if (higher > j) {
					badArray[i]++;
				}
			}
	}
		//passes input ranges to badArray
	
	public static void addRangePerc() {
		float total = rangeTotalCheck();
		for (int i=0; i < rangeArray.length; i++) {
			percArray[i] = rangeArray[i]*100/total;
		}
	}
		//populates range percentages array
	
	public static void addBadPerc() {
		float total = badTotalCheck();
		for (int i=0; i < badArray.length; i++) {
			badPercArray[i] = badArray[i]*100/total;
		}
	}
		//populates bad badpercentages array
	
	public static void printArray() {
		addRangePerc();
		addBadPerc();
		for (int i=0, j=30; i < rangeArray.length; i++, j+=10) {
			System.out.println(j + ",000 - " +(j+9)+ ",999 = " + badArray[i] + ", " + badPercArray[i] + "%" + ", " + rangeArray[i] + ", " + percArray[i] + "%");
		}
		System.out.println("Totals: Colazzi's: " + badTotalCheck() + ", Mine: " + rangeTotalCheck());
	}
		//calls addBadPerc() and addRangePerc() then prints the organized data to the console for comparison
	
	public static float badTotalCheck() {
		float total = 0;
		for (float s : badArray) {
			total += s;
		}
		return total;
	}
		//calculates the total data points of Colazzi's Method
	
	public static float rangeTotalCheck() {
		float total = 0;
		for (float s : rangeArray) {
			total += s;
		}
		return total;
	}
		//calculates the total number of inputs (through my method)
	
	public static void clearArrays() {
		for (int i=0; i<rangeArray.length; i++) {
			rangeArray[i] = 0;
		}
		
		for (int i=0; i<badArray.length; i++) {
			badArray[i] = 0;
		}
		
		for (int i=0; i<percArray.length; i++) {
			percArray[i] = 0;
		}
		
		for (int i=0; i<badPercArray.length; i++) {
			badPercArray[i] = 0;
		}
	}
	//Clears the arrays
	
	public static void main(String[] args) {
		addtoArray(60000, 60000);
		addtoArray(40000, 50000);
		addtoArray(46000, 55000);
		addtoArray(43680, 43680);
		addtoArray(43535, 69635);
		addtoArray(36000, 48000);
		addtoArray(50000, 50000);
		addtoArray(38000, 57000);
		addtoArray(50000, 60000);
		addtoArray(45000, 50000);
		addtoArray(40000, 45000);
		addtoArray(32000, 38000);
		addtoArray(45000, 50000);
		addtoArray(40000, 45000);
		printArray();
		clearArrays();
		System.out.println();
		addtoArray(80000, 85000);
		addtoArray(45000, 50000);
		addtoArray(40000, 40000);
		addtoArray(45000, 55000);
		addtoArray(35000, 35000);
		addtoArray(60000, 80000);
		addtoArray(45000, 45000);
		addtoArray(30000, 50000);
		addtoArray(50000, 75000);
		addtoArray(70000, 70000);
		addtoArray(60000, 70000);
		addtoArray(40000, 45000);
		addtoArray(40000, 50000);
		addtoArray(50000, 60000);
		addtoArray(50000, 60000);
		addtoArray(70000, 85000);
		addtoArray(45000, 55000);
		addtoArray(50000, 60000);
		printArray();
	}

}

