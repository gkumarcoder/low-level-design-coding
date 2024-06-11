<pre>


</pre>

```

class ValidPalindrome {

  public static String isPalindrome(String s) {
    
    int left = 0;                 // POINTER ONE
    int right = s.length() - 1;   // POINTER TWO
    int i = 1;

    // The terminating condition for the loop is when both the pointers reach the same element or when they cross each other.
    while (left < right) {
      left = left + 1;        // Heading towards the right
      right = right - 1;      // Heading towards the left
      i = i + 1;
      System.out.println(new String(new char[100]).replace('\0', '-'));
    }
    System.out.println("Loop terminated with left = " + left + ", right = " + right);
    return "The pointers have either reached the same index, or have crossed each other, hence we don't need to look further.";
  }

  //Driver code
  public static void main(String[] arg) {
    String[] testCase = {
      "RACECAR",
      "ABBA",
      "TART"
    };
    for (int k = 0; k < testCase.length; k++) {
      System.out.println("Test Case # " + (k + 1));
      System.out.println(isPalindrome(testCase[k]));
      System.out.println(new String(new char[100]).replace('\0', '-'));
    }
  }
}
```
