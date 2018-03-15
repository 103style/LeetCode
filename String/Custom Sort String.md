# 791. Custom Sort String

`S` and `T` are strings composed of lowercase letters. In `S`, no letter occurs more than once.

`S` was sorted in some custom order previously. We want to permute the characters of `T` so that they match the order that `S` was sorted. More specifically, if `x` occurs before `y` in `S`, then `x` should occur before `y` in the returned string.

# Example 1:
Example :
    Input: 
    S = "cba"
    T = "abcd"
    Output: "cbad"
    Explanation: 
    "a", "b", "c" appear in S, so the order of "a", "b", "c" should be "c", "b", and "a". 
    Since "d" does not appear in S, it can be at any position in T. "dcba", "cdba", "cbda" are also valid outputs.
    
# Note:
   * `S` has length at most 26, and no character is repeated in `S`.
   * `T` has length at most 200.
   * `S` and `T` consist of lowercase letters only.

# Solution
* ### java
```
class Solution {
	public static String customSortString(String S, String T) {
		if (S == null || S.length() == 0) {
			return T;
		}
		//输出的字符串
		StringBuffer reslut = new StringBuffer();
		Map<String, Integer> tempMap = new HashMap<>();
		for (int i = 0; i < T.length(); i++) {
			String value = String.valueOf(T.charAt(i));
			//先判断S里面是不是有这个字符，没有直接加在输出字符串上
			if (S.indexOf(value) == -1) {
				reslut.append(value);
				continue;
			}
			if (tempMap.containsKey(value)) {
				//保存过 值加一
				int temp = tempMap.get(value);
				temp++;
				tempMap.put(value, temp);
			} else {
				//没保存过 直接设置为1
				tempMap.put(value, 1);
			}
		}
		for (int i = 0; i < S.length(); i++) {
			String key = String.valueOf(S.charAt(i));
			Integer value = tempMap.get(key);
            if(value == null){
                continue;
            }
			for (int j = 0; j < value; j++) {
				reslut.append(key);
			}
		}
		return reslut.toString();
	}
}
```
* ### the most votes
```
public String customSortString(String S, String T) {
	int[] count = new int[26];
	for (char c : T.toCharArray()) {
		// count each char in T.
		++count[c - 'a']; 
	}  
	StringBuilder sb = new StringBuilder();
	for (char c : S.toCharArray()) {                            
		while (count[c - 'a']-- > 0) { 
		 // sort chars both in T and S by the order of S.
			sb.append(c); 
		}   
	}
	for (char c = 'a'; c <= 'z'; ++c) {
		while (count[c - 'a']-- > 0) { 
			// group chars in T but not in S.
			sb.append(c); 
		}   
	}
	return sb.toString();
}
```
