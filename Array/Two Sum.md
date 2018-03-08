#  Two Sum

Given an array of integers, return `indices` of the two numbers such that they add up to a specific target.

You may assume that each input would have `exactly` one solution, and you may not use the same element twice.

# Example :

    Given nums = [2, 7, 11, 15], target = 9,
    Because nums[0] + nums[1] = 2 + 7 = 9,
    return [0, 1].
    

# Solution
* ### java( O(n) )
```
class Solution {
    public int[] twoSum(int[] nums, int target) {
       if(nums == null || nums.length == 0){
           throw new IllegalArgumentException("nums is Illegal");
       }
        Map<Integer,Integer> resMaps = new HashMap<>();
        for(int i = 0 ; i< nums.length; i++){
            int res = target - nums[i];
            if(resMaps.containsKey(res)){
                return new int[]{resMaps.get(res),i};
            }
            
            resMaps.put(nums[i],i);
        }
        
        throw new IllegalArgumentException("no solution");
    }
}
```
* ### java ( O(n​2​​ ) )
```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        if (nums != null && nums.length > 1) {
            for (int i = 0; i < nums.length; i++){
                // if(nums[i] > target){
                //     continue;
                // }
                for(int j = 0; j < nums.length ; j++){
                    if (i == j) {
                        continue;
                    }
                    if (nums[i] + nums[j] == target){
                        int [] res = new int[2];
                        res[0] = i;
                        res[1] = j;
                        return res;
                    }
                }
            }
            return null;
        } else {
            return null;
        }
    }
}
```

* ### the most votes
```
public int[] twoSum(int[] numbers, int target) {
    int[] result = new int[2];
    Map<Integer, Integer> map = new HashMap<Integer, Integer>();
    for (int i = 0; i < numbers.length; i++) {
        if (map.containsKey(target - numbers[i])) {
            result[1] = i + 1;
            result[0] = map.get(target - numbers[i]);
            return result;
        }
        map.put(numbers[i], i + 1);
    }
    return result;
}
```
