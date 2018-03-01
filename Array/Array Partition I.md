# Array Partition I

Given an array of `2n` integers, your task is to group these integers into `n` pairs of integer, say (a1, b1), (a2, b2), ..., (an, bn) which makes sum of min(ai, bi) for all i from 1 to n as large as possible.

# Example 1:
    Input: [1,4,3,2]

    Output: 4
    Explanation: n is 2, and the maximum sum of pairs is 4 = min(1, 2) + min(3, 4).
    
# Note:
* `n` is a positive integer, which is in the range of [1, 10000].
* All the integers in the array will be in the range of [-10000, 10000].

# Solution
* java
```
class Solution {
    public int arrayPairSum(int[] nums) {
        //Arrays.sort(nums);
       //sort(nums, 0, nums.length - 1);
        threePartSort(nums, 0, nums.length - 1);
        int sum = 0;
        for(int i = 0; i < nums.length; i+=2){
            sum += nums[i];
        }
        return sum;
    }
    
    public void threePartSort(int[] a,int start,int end){
        if(start < end){
            int i= start;
            int j = end;
            int k = start+1;
            int point = a[start];
            OUT_LINE:while(k <= j){
                if(a[k] < point){
                    swapIntArray(a,i,k);
                    i++;
                    k++;
                }else if(a[k] == point){
                    k++;
                }else{
                    while(a[j] > point){
                        j--;
                        if(j < k){
                            break OUT_LINE;
                        }
                    }   
                    
                    if(a[j] < point){
                        swapIntArray(a, k, j);
                        swapIntArray(a,i,k);
                        i++;
                        
                    }else{
                        swapIntArray(a,k,j);
                    }
                    k++;
                }
            }
            threePartSort(a, start, i-1);
            threePartSort(a, j+1, end);
        }
    }
    
    
    public void sort(int[] a, int left, int right) {
		if(left < right){
            int i = left;
            int k = left + 1;
            int point = a[left];
            while(k <= right){
                if(a[k] < point){
                    i++;
                    swapIntArray(a, i, k);
                }
                k++;
            }
            swapIntArray(a, left, i);
            sort(a, left, i - 1);
            sort(a, i + 1, right);
        }
	}
    
    public void swapIntArray(int[] a, int pos1, int pos2){
        int temp = a[pos1];
        a[pos1] = a[pos2];
        a[pos2] = temp;
    }
}
```
