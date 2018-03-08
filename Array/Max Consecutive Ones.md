# Max Consecutive Ones

Given a binary array, find the maximum number of consecutive 1s in this array.

# Example 1:
    Input: [1,1,0,1,1,1]
    Output: 3
    Explanation: The first two digits or the last three digits are consecutive 1s.
        The maximum number of consecutive 1s is 3.
    
# Note:
* The input array will only contain 0 and 1.
* The length of input array is a positive integer and will not exceed 10,000

# Solution
* ### java
```
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int max = 0;
        int temp = 0;
        for(int i = 0; i < nums.length; i++){
            if(nums[i] == 1){
                temp++;
                max = (temp > max && i + 1 == nums.length) ? temp : max;
            }else{
                max = temp > max ? temp : max;
                temp = 0;
            }
        }
        return max;
    }
}
```
* ### the most votes
```
public int findMaxConsecutiveOnes(int[] nums) {
    int maxHere = 0, max = 0;
    for (int n : nums)
        max = Math.max(max, maxHere = n == 0 ? 0 : maxHere + 1);
    return max; 
} 
```
