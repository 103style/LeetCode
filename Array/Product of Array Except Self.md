# 238. Product of Array Except Self

Given an array of n integers where n > 1, `nums`, return an array `output` such that `output[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

Solve it without division and in O(n).

For example, given `[1,2,3,4]`, return `[24,12,8,6]`.

Follow up:
Could you solve it with constant space complexity? 
(Note: The output array **does not** count as extra space for the purpose of space complexity analysis.)

### Solution

**java  the most votes**
 ```
 class Solution {
    public int[] productExceptSelf(int[] nums) {
//         int [] res = new int[nums.length];
//         for(int i = 0, temp = 1; i < nums.length - 1; i++){
//             res[i] = temp;
//             temp *= nums[i];
//         }
        
//         for(int i = nums.length - 1, temp = 1; i >= 0 ; i--){
//             res[i] *= temp;
//             temp *= nums[i];
//         }
//         return res;
        
        int n = nums.length;
        int[] res = new int[n];
        res[0] = 1;
        for (int i = 1; i < n; i++) {
            res[i] = res[i - 1] * nums[i - 1];
        }
        int right = 1;
        for (int i = n - 1; i >= 0; i--) {
            res[i] *= right;
            right *= nums[i];
        }
        return res;
    }
}
 ```
