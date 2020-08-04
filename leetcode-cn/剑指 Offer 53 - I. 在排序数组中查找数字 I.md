# [剑指 Offer 53 - I. 在排序数组中查找数字 I](https://leetcode-cn.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/)

---

> **Difficulty** : **Easy**
>
> **Related Topics** : **Array**、**Binary Search**

---

> 统计一个数字在排序数组中出现的次数。
>
>  
>
> ### 示例 1:
> ```
> 输入: nums = [5,7,7,8,8,10], target = 8
> 输出: 2
> ```
>
> ### 示例 2:
> ```
> 输入: nums = [5,7,7,8,8,10], target = 6
> 输出: 0
> ```
>
> ### 限制：
> * `0 <= 数组长度 <= 50000`

---

### Solution
* **mine**
  * **Java**

    ```
    public int search(int[] nums, int target) {
        return find(nums, target + 1) - find(nums, target);
    }

    int find(int[] nums, int target){
        int l = 0, r = nums.length;
        while(l < r){
            int mid = (l + r) >>> 1;
            if(nums[mid] >= target){
                r = mid;
            }else{
                l = mid + 1;
            }
        }
        return l;
    }
    ```


---
