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

  * Binary Search (dfs): most preferable
  ```
  public int kthSmallest(TreeNode root, int k) {
        int count = countNodes(root.left);
        if (k <= count) {
            return kthSmallest(root.left, k);
        } else if (k > count + 1) {
            return kthSmallest(root.right, k-1-count); // 1 is counted as current node
        }
        
        return root.val;
    }
    
    public int countNodes(TreeNode n) {
        if (n == null) return 0;
        
        return 1 + countNodes(n.left) + countNodes(n.right);
    }
    ```

  * DFS in-order recursive:
  ```
   // better keep these two variables in a wrapper class
    private static int number = 0;
    private static int count = 0;

    public int kthSmallest(TreeNode root, int k) {
        count = k;
        helper(root);
        return number;
    }
    
    public void helper(TreeNode n) {
        if (n.left != null) helper(n.left);
        count--;
        if (count == 0) {
            number = n.val;
            return;
        }
        if (n.right != null) helper(n.right);
    }
  ```
  * DFS in-order iterative:
  ```
  public int kthSmallest(TreeNode root, int k) {
        Stack<TreeNode> st = new Stack<>();
        
        while (root != null) {
            st.push(root);
            root = root.left;
        }
            
        while (k != 0) {
            TreeNode n = st.pop();
            k--;
            if (k == 0) return n.val;
            TreeNode right = n.right;
            while (right != null) {
                st.push(right);
                right = right.left;
            }
        }
        
        return -1; // never hit if k is valid
  }
  ```
