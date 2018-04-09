# 537. [Complex Number Multiplication](https://leetcode.com/problems/complex-number-multiplication/description/)

Given two strings representing two [complex numbers](https://en.wikipedia.org/wiki/Complex_number).

You need to return a string representing their multiplication. Note i2 = -1 according to the definition.

### Example 1:
    Input: "1+1i", "1+1i"
    Output: "0+2i"
    Explanation: (1 + i) * (1 + i) = 1 + i2 + 2 * i = 2i, and you need convert it to the form of 0+2i.

### Example 2:
    Input: "1+-1i", "1+-1i"
    Output: "0+-2i"
    Explanation: (1 - i) * (1 - i) = 1 + i2 - 2 * i = -2i, and you need convert it to the form of 0+-2i.

### Note:
* The input strings will not have extra blank.
* The input strings will be given in the form of a+bi, where the integer a and b will both belong to the range of [-100, 100]. And the output should be also in this form.

### Solution
* **java**
```
class Solution {
    public String complexNumberMultiply(String a, String b) {
        //找到+的位置
        int splitA = a.indexOf("+");
        int splitB = b.indexOf("+");
        //取出前部分的数字
        int a1 = Integer.parseInt(a.substring(0, splitA));
        //获取后面一截字符串
        String tempA2 = a.substring(splitA + 1, a.length() - 1);
        int a2 = 0;
        //判断是不是负数 然后取出后面一截的数字
        if(tempA2.charAt(0) == '-'){
            a2 = 0 - Integer.parseInt(tempA2.substring(1));
        }else{
            a2 = Integer.parseInt(tempA2);     
        }
       
        int b1 = Integer.parseInt(b.substring(0, splitB));
        String tempB2 = b.substring(splitB + 1, b.length() - 1);
        int b2;
        if(tempB2.charAt(0) == '-'){
            b2 = 0 - Integer.parseInt(tempB2.substring(1));
        }else{
            b2 = Integer.parseInt(tempB2);     
        }
        //计算 数字结果 （a + bi）(c + di) = ac- bd + (ad + bc)i;
        int resultA = a1 * b1 - a2 * b2;
        int resultB = a1 * b2 + b1 * a2;
        return resultA + "+" + resultB + "i";
    }
}
```

* **the most votes**
```
public String complexNumberMultiply(String a, String b) {
    int[] coefs1 = Stream.of(a.split("\\+|i")).mapToInt(Integer::parseInt).toArray(), 
          coefs2 = Stream.of(b.split("\\+|i")).mapToInt(Integer::parseInt).toArray();
    return (coefs1[0]*coefs2[0] - coefs1[1]*coefs2[1]) + "+" + (coefs1[0]*coefs2[1] + coefs1[1]*coefs2[0]) + "i";
}
```

* **[more](https://leetcode.com/problems/complex-number-multiplication/solution/)**
