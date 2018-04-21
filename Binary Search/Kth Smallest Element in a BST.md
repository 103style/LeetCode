# 230. [Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/description/)

Given a binary search tree, write a function `kth Smallest` to find the kth smallest element in it.

### Note: 
You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

### Follow up:
What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?

### Credits:
Special thanks to @ts for adding this problem and creating all test cases.


### Solution

* **java**
```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
 //not binary search
class Solution {
    public int kthSmallest(TreeNode root, int k) {
        List<Integer> res = getValue(root);
        Object[]  array = res.toArray();
        Arrays.sort(array);
        return Integer.parseInt(array[k-1].toString());
    }
    
    public List<Integer> getValue(TreeNode node){
        List<Integer> res = new ArrayList<>();
        if(node != null){
            res.add(node.val);
            TreeNode left = node.left;
            TreeNode right = node.right;
            if(left != null){
                res.addAll(getValue(left));
            }
            if(right != null){
                res.addAll(getValue(right));
            } 
        }
        return res;
    }
}
```

* **the most votes** 
```
```
