# Reshape the Matrix

In MATLAB, there is a very useful function called 'reshape', which can reshape a matrix into a new one with different size but keep its original data.

You're given a matrix represented by a two-dimensional array, and two `positive` integers r and c representing the `row` number and `column` number of the wanted reshaped matrix, respectively.

The reshaped matrix need to be filled with all the elements of the original matrix in the same `row-traversing` order as they were.

If the 'reshape' operation with given parameters is possible and legal, output the new reshaped matrix; Otherwise, output the original matrix.

# Example 1:

    Input: 
    nums = 
    [[1,2],
     [3,4]]
    r = 1, c = 4
    Output: 
    [[1,2,3,4]]
    Explanation:
    The row-traversing of nums is [1,2,3,4]. The new reshaped matrix is a 1 * 4 matrix, fill it row by row by using the previous list.
    
    
# Example 2:
    
    Input: 
    nums = 
    [[1,2],
     [3,4]]
    r = 2, c = 4
    Output: 
    [[1,2],
     [3,4]]
    Explanation:
    There is no way to reshape a 2 * 2 matrix to a 2 * 4 matrix. So output the original matrix.
    
# Note:
  * The height and width of the given matrix is in range [1, 100].
  * The given r and c are all positive.
  
  
# Solution
* ### java
```
class Solution {
    public int[][] matrixReshape(int[][] nums, int r, int c) {
//         int count = nums.length * nums[0].length;
//         if(r*c > count){
//             return nums;
//         }
        
//         int [] temp =new int[count];
//         for(int i = 0;i<nums.length;i++){
//             for(int j =0; j < nums[i].length; j++){
//                 temp[i*nums[i].length + j] = nums[i][j];
//             }
//         }
        
//         int[][] sort = new int[r][c];
//         for(int i = 0;i<r;i++){
//             for(int j =0; j < c; j++){
//                 sort[i][j]= temp[i*c + j] ;
//             }
//         }
//         return  sort;
        
        
        int rowCount = nums.length;
        int colCount = nums[0].length;
        if(rowCount*colCount != r*c){
            return nums;
        }
        int[][] res = new int[r][c];
        for(int i = 0; i < r *c ; i++){
            res[i / c][i % c] = nums[i / colCount][i % colCount];
        }
        return res;
    }
}
```
* ### the most votes 
```
public int[][] matrixReshape(int[][] nums, int r, int c) {
    int n = nums.length, m = nums[0].length;
    if (r*c != n*m) return nums;
    int[][] res = new int[r][c];
    for (int i=0;i<r*c;i++) 
        res[i/c][i%c] = nums[i/m][i%m];
    return res;
}
```
