
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

 Step 3: SubGrid check:

 How to find begning of all the subgrid 

 squroot of board length sqrt= √4 = 2

 eg : (1, 1)  row - row % sqrt =  1-1%2 = 0
              col- col % sqrt = 1 - 1%2 = 0 
      (2,1)   2-2%2 = 2 
              1 - 1%2 = 0;
              


```
public class Sudoku{

public static void displayBoard(int board[][]) {
    for (int[] myBoard : board) {
      System.out.println(Arrays.toString(myBoard));
    }
  }

  static boolean isSafe(int board[][], int row, int col, int num) {
    int n = board.length;
    // Check the row
    for (int i = 0; i < n; i++) {
      if (board[row][i] == num) {
        return false;
      }
    }

    // Check the col
    for (int row1 = 0; row1 < n; row1++) {
      if (board[row1][col] == num) {
        return false;
      }
    }

    // Check the SubGrid
    int sqrt = (int) Math.sqrt(n);
    int startRow = row - row % sqrt;
    int startCol = col - col % sqrt;
    for (int i = startRow; i < startRow + sqrt; i++) {
      for (int j = startCol; j < startCol + sqrt; j++) {
        if (board[i][j] == num) {
          return false;
        }
      }
    }
    return true;
  }

  public static boolean solveSudoku(int board[][]) {
    int n = board.length;
    int row = -1;
    int col = -1;
    boolean isEmptyLeft = false;

    // Finding the empty cell if any
    for (int i = 0; i < n; i++) {
      for (int j = 0; j < n; j++) {
        if (board[i][j] == 0) {
          row = i;
          col = j;
          isEmptyLeft = true;
          break;
        }
      }
      if (isEmptyLeft) {
        break;
      }
    }

    // if Sudoku is solved
    if (!isEmptyLeft) {
      return true;
    }

    // Start backtracking work
    for (int num = 1; num <= n; num++) {
      // Check if it is safe to place
      if (isSafe(board, row, col, num)) {
        board[row][col] = num;
        if (solveSudoku(board)) {
          return true;
        }
        board[row][col] = 0; // backtrack
      }
    }

    return false;
  }

  public static void main(String[] args) {
    int board[][] = {
        {1, 0, 3, 0},
        {0, 0, 2, 1},
        {0, 1, 0, 2},
        {2, 4, 0, 0}
    };
    if (solveSudoku(board)) {
      displayBoard(board);
    } else {
      System.out.println("Sorry, No Solution");
    }
  }

}

```


 

 

 
