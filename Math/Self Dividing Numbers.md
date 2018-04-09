# 728. [Self Dividing Numbers](https://leetcode.com/problems/self-dividing-numbers/description/)

A self-dividing number is a number that is divisible by every digit it contains.

For example, 128 is a self-dividing number because `128 % 1 == 0`, `128 % 2 == 0`, and `128 % 8 == 0`.

Also, a self-dividing number is not allowed to contain the digit zero.

Given a lower and upper number bound, output a list of every possible self dividing number, including the bounds if possible.

### Example 1:
    Input: 
    left = 1, right = 22
    Output: [1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 12, 15, 22]

### Note:
* The boundaries of each input argument are `1 <= left <= right <= 10000`.

### Solution

* **java**
```
class Solution {
    public List<Integer> selfDividingNumbers(int left, int right) {
        List<Integer> res = new ArrayList<>();
        for(int i = left; i <= right; i++){
            //0结尾的
            if(i % 10 == 0){
                continue;
            }
            if(i < 10){
                res.add(i);
                continue;
            }
            if(i < 100){
                if(i % (i / 10) == 0 && i % (i % 10) == 0){
                    res.add(i);
                }
                continue;
            }
            //十位为0的 跳过
            if( i / 10 % 10 == 0){
                continue;
            }
            
            if(i < 1000){
                if(i % (i / 100) == 0 
                   && i % ((i % 100) / 10) == 0
                   && i % (i % 10) == 0){
                    res.add(i);
                }
                continue;
            }
            //百位为0的 跳过
            if(i / 100 % 10 == 0){
                continue;
            }
            
            if(i < 10000){
                if(i % (i / 1000) == 0
                   && i % ((i % 1000) / 100) == 0
                   && i % ((i % 100) / 10) == 0
                   && i % (i % 10) == 0){
                    res.add(i);
                }
                continue;
            }
        }
        return res;
    }
}
```

