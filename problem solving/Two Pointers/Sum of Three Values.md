
```
class SumOfThree {
	public static boolean findSumOfThree(int nums[], int target) {
		// Sort the input list
		Arrays.sort(nums);
		int low, high, triples;

		// Fix one integer at a time and find the other two
		for (int i = 0; i < nums.length - 2; i++) {
			// Initialize the two pointers
			low = i + 1;
			high = nums.length - 1;

			// Traverse the list to find the triplet whose sum equals the target
			while (low < high) {
				triples = nums[i] + nums[low] + nums[high];

				// The sum of the triplet equals the target
				if (triples == target) {
					return true;
				}
				// The sum of the triplet is less than target, so move the low pointer forward
				else if (triples < target) {
					low++;
				} 
				// The sum of the triplet is greater than target, so move the high pointer backward
				else {
					high--;
				}
			}
		}

		// No such triplet found whose sum equals the given target
		return false;
	}

	// Driver code
	public static void main(String[] args) {
		int[][] numsList = {{3, 7, 1, 2, 8, 4, 5},
                       {-1, 2, 1, -4, 5, -3},
                       {2, 3, 4, 1, 7, 9},
                       {1, -1, 0},
                       {2, 4, 2, 7, 6, 3, 1}};
					   
		int[] testList = {10, 7, 20, -1, 8};

		
		for (int i=0; i<testList.length; i++) {
			System.out.print(i+1);
			System.out.println(".\tInput array: " + Arrays.toString(numsList[i]));
			
			if (findSumOfThree(numsList[i], testList[i])) {
			System.out.println("\tSum for " + testList[i] + " exists ");
			} else {
			System.out.println("\tSum for " + testList[i] + " does not exist ");
			}
			
			System.out.println(new String(new char[100]).replace('\0', '-'));
		}
	}
}
```
