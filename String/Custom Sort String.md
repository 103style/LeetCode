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
    public boolean judgeCircle(String moves) {
        //先判空 以及 长度不是2的倍数
        if(moves == null || moves.length() == 0
           || moves.length() % 2 != 0){
            return false;
        }
        //定义一个原点位置 第一个位置表示上下移动  U 加一  D 减一
        //第二个位置表示左右移动  R 加一  L 减一
        int [] point= {0, 0};
        //把string变成String数组
        String[] moveArray = moves.split("");
        for(String s : moveArray){
            switch(s){
                case "U":
                    point[0]++;    
                    break;
                case "D":
                    point[0]--;    
                    break;
                case "R":
                    point[1]++;    
                    break;
                case "L":
                    point[1]--;    
                    break;
                default:
                    return false;
            }
        }
        //如果最后point还是{0，0}的话 就返回true
        return point[0] == 0 && point[1] == 0;
    }
}

// OR

class Solution {
    public boolean judgeCircle(String moves) {
        int [] point= {0, 0};
        if(moves == null || moves.length() == 0){
            return false;
        }
        for(int i = 0; i < moves.length(); i++){
            char s = moves.charAt(i);
            switch(s){
                case 'U':
                    point[0]++;    
                    break;
                case 'D':
                    point[0]--;    
                    break;
                case 'R':
                    point[1]++;    
                    break;
                case 'L':
                    point[1]--;    
                    break;
                default:
                    return false;
            }
        }
        return point[0] == 0 && point[1] == 0;
    }
}
```
* ### the most votes
```
public class Solution {
    public boolean judgeCircle(String moves) {
        int x = 0;
        int y = 0;
        for (char ch : moves.toCharArray()) {
            if (ch == 'U') y++;
            else if (ch == 'D') y--;
            else if (ch == 'R') x++;
            else if (ch == 'L') x--;
        }
        return x == 0 && y == 0;
    }
}
```
