#### Question
Given a binary tree, find all of its path sum. The path is from root to any of leaf nodes.
#### Examples
![](https://farm3.staticflickr.com/2876/34315485026_03a3911c1c_o.png)
#### Analysis
The key point is to decide when to add buffer list into result. And we must make sure every node can reach __buffer.remove(buffer.size() - 1)__ except null node. 
#### Code
```java
public List<List<Integer>> binaryTreePathSum(TreeNode root, int target) {
    List<List<Integer>> res = new ArrayList<>();
    List<Integer> buffer = new ArrayList<>();
    helper(root, res, buffer, target);
    return res;
}
    
private void helper(TreeNode root, List<List<Integer>> res, List<Integer> buffer, int target) {
    if (root == null) {
        return;
    }
    
    buffer.add(root.val);
    // The end of path must be a leaf node
    if (root.left == null && root.right == null && target == root.val) {
        res.add(new ArrayList<>(buffer));
    }
    helper(root.left, res, buffer, target - root.val);
    helper(root.right, res, buffer, target - root.val);
    buffer.remove(buffer.size() - 1);
}
```