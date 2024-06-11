
```
import java.util.*;

public class SumOfThree{
   public static boolean findSumOfThree(int[] nums, int target) {
      
     Arrays.sort(nums);

     for(int i = 0; i < nums.length - 2; i++){
        int first = nums[i];
        int start = i + 1;
        int end = nums.length - 1;
        while(start < end){
           int result = first + nums[start] + nums[end];
           if(result ==  target){
              return true;
           }
           	else if (result < target) {
					start++;
				} 
				else {
					end--;
				}  
        }
     }
      return false;
   }
}
```
