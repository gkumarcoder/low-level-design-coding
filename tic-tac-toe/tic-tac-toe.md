
PROBLEM : 
Tic Tac Toe is one of the classic games with pretty simple rules. Two players take turns placing characters on an n by n board. The first player that connects n consecutive characters horizontally, vertically, or diagonally wins the game. Traditionally (and in this problem), the board width is fixed at 3. However, to help demonstrate the efficiency of each approach, we will refer to the board width as n throughout this article.

     0     1     2    
    -----------------
  0 |   |     |     |    
    -----------------
  1 |   |     |     |   
    -----------------
  2 |   |     |     |  
    -----------------

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




