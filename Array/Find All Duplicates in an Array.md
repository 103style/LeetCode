# Find All Duplicates in an Array

Given an array of integers, 1 ≤ a[i] ≤ n (n = size of array), some elements appear `twice` and others appear `once`.

Find all the elements that appear `twice` in this array.

Could you do it without extra space and in O(n) runtime?

# Example 1:
    Input:
    [4,3,2,7,8,2,3,1]

    Output:
    [2,3]
    

# Solution
* java

* best one
```
class Solution {
	public static List<Integer> findDuplicates2(int[] nums) {
		List<Integer> list = new ArrayList();
		int a[] = new int[nums.length + 1];
		for (int i : nums)
			a[i]++;

		for (int i = 1; i < a.length; i++) {
			if (a[i] == 2) {
				list.add(i);
			}
		}
		return list;
	}
}
	
```

```
class Solution {
    public List<Integer> findDuplicates(int[] nums) {
	Map<Integer, Integer> tempMap = new HashMap<>();
	Map<Integer, Integer> twiceMap = new HashMap<>();
	Map<Integer, Integer> twiceMoreMap = new HashMap<>();
	int num = 0;
	for (int i = 0; i < nums.length; i++) {
		num = nums[i];
		if (twiceMoreMap.containsKey(num)) {
			continue;
		}
		if (twiceMap.containsKey(num)) {
			int value = twiceMap.get(num) + 1;
			if (value > 2) {
				twiceMoreMap.put(num, 1);
				twiceMap.remove(num);
			} else {
				twiceMap.put(num, 2);
			}
			continue;
		}
		if (tempMap.containsKey(num)) {
			twiceMap.put(num, 1);
		} else {
			tempMap.put(num, 1);
		}
	}
	Set<Integer> twiceKey = twiceMap.keySet();
	List<Integer> output = new ArrayList<>();
	Iterator<Integer> it = twiceKey.iterator();
	while (it.hasNext()){
	output.add(it.next());     
        }
		return output;
	}
}
```


