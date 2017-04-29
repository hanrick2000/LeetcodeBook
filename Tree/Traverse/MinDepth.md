#### Question
Find number of nodes along the shortest path from root to __leaf node__.
#### Examples
Given 1,2,3,#,#,4,5 return 2
Given 1,#,2,3 return 3
#### Analysis
Typical traverse method.
#### Code
```java
private int minDepth = Integer.MAX_VALUE;
public int minDepth(TreeNode root) {
    // Edge case
    if (root == null) {
        return 0;
    }
    helper(root, 1);
    return minDepth;
}

private void helper(TreeNode root, int depth) {
    if (root == null) {
        return;
    }
    // Notice it should be leaf node!
    if (root.left == null && root.right == null && depth < minDepth) {
        minDepth = depth;
    }
    helper(root.left, depth + 1);
    helper(root.right, depth + 1);
}
```