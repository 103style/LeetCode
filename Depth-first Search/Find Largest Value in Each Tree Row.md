# 515. [Find Largest Value in Each Tree Row](https://leetcode.com/problems/find-largest-value-in-each-tree-row/description/)

You need to find the largest value in each row of a binary tree.

    Example:
    Input: 

              1
             / \
            3   2
           / \   \  
          5   3   9 

    Output: [1, 3, 9]
    
### Solution
* **java**
```
// D = depth  O(2^D)time O(2^D)space
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<Integer> largestValues(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        int depth = 0;
        if(root == null){
            return res;
        }
        List<TreeNode> list = new ArrayList<>();
        list.add(root);
        while(list.size() > 0){
            res.add(getMaxValue(list));
            List<TreeNode> temp = new ArrayList<>();
            for(int i = 0 ; i < list.size(); i++){
                TreeNode node = list.get(i);
                if(node.left != null){
                    temp.add(node.left);    
                }
                if(node.right != null){
                    temp.add(node.right);    
                }
            }
            list = temp;
        }
        return res;
        
    }
    
    public int getMaxValue(List<TreeNode> nodes){
        int max = nodes.get(0).val;
        if(nodes.size() < 2){
            return max;
        }
        for(int i = 1; i < nodes.size(); i++){
            max = Math.max(max, nodes.get(i).val);
        }
        return max;
    }
}
```

* **the most votes**
```
public class Solution {
    public List<Integer> largestValues(TreeNode root) {
        List<Integer> res = new ArrayList<Integer>();
        helper(root, res, 0);
        return res;
    }
    private void helper(TreeNode root, List<Integer> res, int d){
        if(root == null){
            return;
        }
       //expand list size
        if(d == res.size()){
            res.add(root.val);
        }
        else{
        //or set value
            res.set(d, Math.max(res.get(d), root.val));
        }
        helper(root.left, res, d+1);
        helper(root.right, res, d+1);
    }
}
```

