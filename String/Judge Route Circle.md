# Judge Route Circle

Initially, there is a Robot at position (0, 0). Given a sequence of its moves, judge if this robot makes a circle, which means it moves back to `the original place`.

The move sequence is represented by a string. And each move is represent by a character. The valid robot moves are `R` (Right), `L` (Left), `U` (Up) and `D` (down). The output should be true or false representing whether the robot makes a circle.

# Example 1:
    Input: "UD"
    Output: true
    
# Example 2: 
    Input: "LL"
    Output: false


# Solution
* ### java
```
class Solution {
    public boolean judgeCircle(String moves) {
        int [] point= {0, 0};
        if(moves == null || moves.length() == 0){
            return false;
        }
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
        return point[0] == 0 && point[1] == 0;
    }
}
```
* ### the most votes
```

```
