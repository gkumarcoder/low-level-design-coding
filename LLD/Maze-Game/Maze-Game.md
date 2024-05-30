



```
import java.util.Arrays;

public class Maze {

  static void solveMazeWithPrintPathMatrix(String path, boolean[][] maze, int row, int col,
                                           int[][] pathMatrix, int level) {

    if (row == maze.length - 1 && col == maze[0].length - 1) {
      pathMatrix[row][col] = level;
      displayPathMatrix(pathMatrix);
      System.out.println(path);
      System.out.println("===================");
      return;
    }

    if (!maze[row][col]) {
      return;
    }
    maze[row][col] = false;
    pathMatrix[row][col] = level;

    // DOWN
    if (row < maze.length - 1) {
      solveMazeWithPrintPathMatrix(path + "D", maze, row + 1, col, pathMatrix, level + 1);
    }
    // RIGHT
    if (col < maze[0].length - 1) {
      solveMazeWithPrintPathMatrix(path + "R", maze, row, col + 1, pathMatrix, level + 1);
    }
    // UP
    if (row > 0) {
      solveMazeWithPrintPathMatrix(path + "U", maze, row - 1, col, pathMatrix, level + 1);
    }
    // LEFT
    if (col > 0) {
      solveMazeWithPrintPathMatrix(path + "L", maze, row, col - 1, pathMatrix, level + 1);
    }

    maze[row][col] = true;
    pathMatrix[row][col] = 0;
  }

  private static void displayPathMatrix(int[][] pathMatrix) {
    for (int[] arr : pathMatrix) {
      System.out.println(Arrays.toString(arr));
    }
  }

  public static void main(String[] args) {
    boolean[][] boardPrintPathMatrix = {
        {true, true, true},
        {true, true, true},
        {true, true, true}
    };
    int[][] pathMatrix = new int[boardPrintPathMatrix.length][boardPrintPathMatrix[0].length];
    solveMazeWithPrintPathMatrix("", boardPrintPathMatrix, 0, 0, pathMatrix, 1);
  }
}

```
