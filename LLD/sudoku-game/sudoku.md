
**First, we will design our logic for a 4x4 board.**

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
