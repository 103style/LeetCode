# 169. [Majority Element](https://leetcode.com/problems/majority-element/description/)

Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.

### Solution
* **java**
```
// O(n)time  O(n)space
class Solution {
    public int majorityElement(int[] nums) {
        Map<Integer,Integer> map = new HashMap<>();
        for(int i = 0; i < nums.length; i++){
            int t = nums[i];
            if(map.containsKey(t)){
                map.put(t, map.get(t) + 1);
            }else{
                map.put(t,1);
            }
        }
        for(Integer i : map.keySet()){
            if(map.get(i) > nums.length / 2){
                return i;
            }
        }
        return 0;
    }
}
```

* **the most votes**
```
//O(n) time O(1) space fastest solution
public class Solution {
    public int majorityElement(int[] num) {
        int major=num[0], count = 1;
        for(int i=1; i<num.length;i++){
            if(count==0){
                count++;
                major=num[i];
            }else if(major==num[i]){
                count++;
            }else count--;
            
        }
        return major;
    }
}
```
* **use Arrays.sort**
```
//O(nlgn) time    O(1) or O(n) space
public class Solution {
    public int majorityElement(int[] nums) {
        Arrays.sort(nums);
	return nums[nums.length/2];
    }
}
```

* **Boyer-Moore Voting Algorithm**
```
//O()time  O(1)space
class Solution {
    public int majorityElement(int[] nums) {
        int count = 0;
        Integer candidate = null;

        for (int num : nums) {
            if (count == 0) {
                candidate = num;
            }
            count += (num == candidate) ? 1 : -1;
        }

        return candidate;
    }
}
```
[more solution](https://leetcode.com/problems/majority-element/solution/)
