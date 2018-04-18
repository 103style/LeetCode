# 349. [Intersection of Two Arrays](https://leetcode.com/problems/intersection-of-two-arrays/description/)

Given two arrays, write a function to compute their intersection.

### Example:
Given nums1 = `[1, 2, 2, 1]`, nums2 = `[2, 2]`, return `[2]`.

### Note:
* Each element in the result must be unique.
* The result can be in any order.

### Solution
* **Java**
```
// O(N)time  O(N)space    Runtime: 5 ms
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        if(nums1 == null ||nums1.length == 0
           || nums2 == null || nums2.length == 0){
            return new int[0];
        }
        Map<Integer,Integer> map = new HashMap<>();
        for(int i = 0; i < nums1.length; i++){
            map.put(nums1[i],1);
        }
        Map<Integer,Integer> resMap = new HashMap<>();
        for(int i = 0; i < nums2.length; i++){
            if(map.containsKey(nums2[i])){
                resMap.put(nums2[i], 1);
            }
        }
        Set<Integer> resSet = resMap.keySet();
        if(resSet.size() == 0){
            return new int[0];
        }else{
            int [] res = new int[resSet.size()];
            Iterator<Integer> iterator = resSet.iterator();
            int i = 0;
            while(iterator.hasNext()){
                res[i] = iterator.next();
                i++;
            }
            return res;
        }
    }
}
```

* **the most votes**
```
// O(nlogn)time O(n)space
public class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set = new HashSet<>();
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        int i = 0;
        int j = 0;
        while (i < nums1.length && j < nums2.length) {
            if (nums1[i] < nums2[j]) {
                i++;
            } else if (nums1[i] > nums2[j]) {
                j++;
            } else {
                set.add(nums1[i]);
                i++;
                j++;
            }
        }
        int[] result = new int[set.size()];
        int k = 0;
        for (Integer num : set) {
            result[k++] = num;
        }
        return result;
    }
}
```
```
//O(nlogn)time O(n)space
public class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set = new HashSet<>();
        Arrays.sort(nums2);
        for (Integer num : nums1) {
            if (binarySearch(nums2, num)) {
                set.add(num);
            }
        }
        int i = 0;
        int[] result = new int[set.size()];
        for (Integer num : set) {
            result[i++] = num;
        }
        return result;
    }
    
    public boolean binarySearch(int[] nums, int target) {
        int low = 0;
        int high = nums.length - 1;
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (nums[mid] == target) {
                return true;
            }
            if (nums[mid] > target) {
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }
        return false;
    }
}
```

* **amazing two line Solution**
`Two-line java 8 solution using Stream`
```
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set = Arrays.stream(nums2).boxed().collect(Collectors.toSet());
        return Arrays.stream(nums1).distinct().filter(e-> set.contains(e)).toArray();
    }
}
```
