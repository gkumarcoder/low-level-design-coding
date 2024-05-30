
**First, we will design our logic for a 4x4 board.**

AS we know it 

1. Fill Each row uniqley.
   
2. Fill each Col from 1 to N
   
3. Each SubGrid should have value from 1 to N-1

And N Value is 4 here 

<PRE>
    0   1   2   3
  |---|---|---|---|
0 | 1 |   | 3 |   |
  |---|---|---|---|
1 |   |   | 2 | 1 |
  |---|---|---|---|
2 |   | 1 |   | 2 |
  |---|---|---|---|
3 | 2 | 4 |   |   |
  |---|---|---|---|

  </PRE>

  How to Solve this problem

 Step 1: We need to identify empty cells.
 
 Step 2: Attempt to position all available choices within the range of 1 to 4


```
public class Sudoku{

public void displayBoard(int board[][]){
 for(int[] myBoard : board ){
 System.out.println(Arrays.toString(myBoard));
 }
}

 public static void main(String[] args){
 int board[][] =
         {
         {1, 0, 3, 0},
         {0, 0, 2, 1},
         {0, 1, 3, 2},
         {2, 4, 0, 0}
         };
   if(solveSudoku(board)){
    displayBoard(board);
   }else{
     System.out.println("Sorry, No Solution");
   }
 }
}

```


 

 

 
