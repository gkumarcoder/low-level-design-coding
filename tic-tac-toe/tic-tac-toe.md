
PROBLEM : 
Tic Tac Toe is one of the classic games with pretty simple rules. Two players take turns placing characters on an n by n board. The first player that connects n consecutive characters horizontally, vertically, or diagonally wins the game. Traditionally (and in this problem), the board width is fixed at 3. However, to help demonstrate the efficiency of each approach, we will refer to the board width as n throughout this article.

<PRE>
     0     1     2    
    -----------------
  0 |   |     |     |    
    -----------------
  1 |   |     |     |   
    -----------------
  2 |   |     |     |  
    -----------------
</PRE>     
    

First approach Intuition :

Since we have to find if the current player has won, we need to look at what the winning conditions are. The figure below illustrates the 4 winning conditions according to the rules.

![image](https://github.com/gkumarcoder/low-level-design-coding/assets/25560217/3918026a-fa51-46a9-a442-4e42de759511)

The above diagram shows that a player can win by connecting n consecutive characters in a row, column, diagonal, or anti-diagonal.

Then, how do we check if any player has won so far?

![image](https://github.com/gkumarcoder/low-level-design-coding/assets/25560217/4094d927-4c26-4900-a1ad-9f446a59de40)

STEP 1>
We can start by creating an n by n grid that represents the original board.

STEP 2>

**Diagonal:** : Next, let's take a closer look at the previous winning conditions. Notice that a character located at [row, col] will be on the diagonal when its column index equals its row index, that is row = col. 
(0,0) (1,1) (2,2)

**Anti-Diagonal** : Likewise, a character will be on the anti-diagonal when then the sum of its row index and column index is equal to n - 1, 
that is row + col = n - 1.

(0,2) (1,1) (2,0)

0 + 2 = 2

1 + 1 = 2

2 + 0 = 2

ALGORITHAM

1. Initialize a 2-dimensional array board of size n by n representing an empty board.

2. For each new move [row, col], mark the relative position board[row][col] on board with the player's id.
   Suppose player one's id is 1, and player two's id is -1.

3. Then, check if this move meets any of the winning conditions:
   i) **ROW :** Check if all cells in the current row are filled with characters from the current player.
      We traverse the row from column 0 to column n - 1 while keeping the row index constant.
   ii) **Column :** Check if all cells in the current column are filled with characters from the current player.
      We traverse the column from row 0 to row n - 1 while keeping the column index constant.
   iii) **Diagonal :** Check if this move is on the diagonal; that is, check if row equals col. If so, traverse the entire diagonal
       and check if all positions on the diagonal contain characters from this player.
   iv) **Anti-Diagonal** Check if this move is on the anti-diagonal; that is, check if row + col equals n - 1. If so,
       traverse the entire anti-diagonal and check if all positions on the anti-diagonal contain characters from this player.
   
4. If there is no winner after all of the moves have been played, we will check if the entire board is filled.
   If so, return "Draw", otherwise return "Pending", meaning the game is still on. That is, check if the length of moves equals
   the number of cells on the n by n board.


   ```
   class Solution {

    // STEP 1 : Initialize the board, n = 3 in this problem.
    private int[][] board;
    private int n = 3;
    
    public String tictactoe(int[][] moves) {
        board = new int[n][n];
        int player = 1;
        
        // Step 2 : For each move
        for (int[] move : moves) {
            int row = move[0], col = move[1];

            // Mark the current move with the current playrer's id.
            board[row][col] = player;

            //Step 3: If any of the winning conditions is met, return the current player's id.
            if (checkRow(row, player) || checkCol(col, player) || (row == col && checkDiagonal(player)) || ( row + col == n - 1 && checkAntiDiagonal(player))) {
                return player == 1 ? "A" : "B";
            }

            // If no one wins so far, change to the other player alternatively. That is from 1 to -1, from -1 to 1.
            player *= -1;       
         }

        // STEP 4: If all moves are completed and there is still no result, we shall check if the grid is full or not. If so,
       //  the game ends with draw, otherwise pending.
        return moves.length == n * n ? "Draw" : "Pending";   
    }

    // Check if any of 4 winning conditions to see if the current player has won.
   // Step 3 (I)
    private boolean checkRow(int row, int player){
        for (int col = 0; col < n; ++col){
            if (board[row][col] != player) return false;
        }
        return true;
    }
    // Step 3 (II)
    private boolean checkCol(int col, int player){
        for (int row = 0; row < n; ++row){
            if (board[row][col] != player) return false;
        }
        return true;
    }
    // Step 3 (III)
    private boolean checkDiagonal(int player){
        for (int row = 0; row < n; ++row){
            if (board[row][row] != player) return false;
        }
        return true;
    }
   
    // Step 3 (IV)
    private boolean checkAntiDiagonal(int player){
        for (int row = 0; row < n; ++row){
            if (board[row][n - 1 - row] != player) return false;
        }
        return true;
    }
   }  

   ```


**Complexity Analysis**

Let n be the length of the board and m be the length of input moves.

Time complexity: O(m⋅n)
For every move, we need to traverse the same row, column, diagonal, and anti-diagonal, which takes O(n) time.

Space complexity: O(n^2)

We use an n by n array to record every move




```

class TicTacToe {

    private int[][] board;
    private int n;

    public TicTacToe(int n) {
        board = new int[n][n];
        this.n = n;
    }

    public int move(int row, int col, int player) {
        //STEP 2: Every move, mark the row and col on the board with the current player's id player..
        board[row][col] = player;
        // check if the player wins
        if ((checkRow(row, player)) || (checkColumn(col, player)) || (row == col && checkDiagonal(player)) ||  (col == n - row - 1 && 
        checkAntiDiagonal(player))) {
            return player;
        }
        return 0;
    }

    private boolean checkDiagonal(int player) {
        for (int row = 0; row < n; row++) {
            if (board[row][row] != player) {
                return false;
            }
        }
        return true;
    }

    private boolean checkAntiDiagonal(int player) {
        for (int row = 0; row < n; row++) {
            if (board[row][n - row - 1] != player) {
                return false;
            }
        }
        return true;
    }

    private boolean checkColumn(int col, int player) {
        for (int row = 0; row < n; row++) {
            if (board[row][col] != player) {
                return false;
            }
        }
        return true;
    }

    private boolean checkRow(int row, int player) {
        for (int col = 0; col < n; col++) {
            if (board[row][col] != player) {
                return false;
            }
        }
        return true;
    }
}


```











