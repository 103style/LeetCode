# 807. Max Increase to Keep City Skyline

In a 2 dimensional array `grid`, each value `grid[i][j]` represents the height of a building located there. We are allowed to increase the height of any number of buildings, by any amount (the amounts can be different for different buildings). Height 0 is considered to be a building as well. 

At the end, the "skyline" when viewed from all four directions of the grid, i.e. top, bottom, left, and right, must be the same as the skyline of the original grid. A city's skyline is the outer contour of the rectangles formed by all the buildings when viewed from a distance. See the following example.

What is the maximum total sum that the height of the buildings can be increased?

### Example:
    Input: grid = [[3,0,8,4],[2,4,5,7],[9,2,6,3],[0,3,1,0]]
    Output: 35
    Explanation: 
    The grid is:
    [ [3, 0, 8, 4], 
      [2, 4, 5, 7],
      [9, 2, 6, 3],
      [0, 3, 1, 0] ]

    The skyline viewed from top or bottom is: [9, 4, 8, 7]
    The skyline viewed from left or right is: [8, 7, 9, 3]

    The grid after increasing the height of buildings without affecting skylines is:

    gridNew = [ [8, 4, 8, 7],
                [7, 4, 7, 7],
                [9, 4, 8, 7],
                [3, 3, 3, 3] ]

### Notes:
* `1 < grid.length = grid[0].length <= 50`.
* All heights `grid[i][j]` are in the range `[0, 100]`.
* All buildings in `grid[i][j]` occupy the entire grid cell: that is, they are a `1 x 1 x grid[i][j]` rectangular prism.


### Solution
* **java**
```
// O(n^2) time  O(n) space
class Solution {
    public int maxIncreaseKeepingSkyline(int[][] grid) {
        int w = grid[0].length;
        int h = grid.length;
        int[] lTR = new int[h];
        int[] tTB = new int[w];
        for(int i = 0; i < w; i++){
            for(int j = 0; j < h; j++){
                tTB[i] = Math.max(tTB[i],grid[j][i]); 
            }
        }
        for(int i = 0; i < h; i++){
            for(int j = 0; j < w; j++){
                lTR[i] = Math.max(lTR[i],grid[i][j]); 
            }
        }
        int res = 0;
         for(int i = 0; i < h; i++){
            for(int j = 0; j < w; j++){
                int temp = grid[i][j];
                res += Math.min(lTR[i],tTB[j]) - temp; 
            }
        }
        return res;
    }
}
```
