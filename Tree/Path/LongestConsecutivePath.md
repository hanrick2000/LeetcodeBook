#### Question
Find longest consecutive path that is from parent to child with increasing order.
#### Examples
Given 3,#,2,#,1 return 1

Given 2,#,3,2,#,1 return 2
#### Analysis
This one is much easier since it already constrains that the path is from parent to child with specific order.
#### Code
```java
private class ResultType {
    int max;
    int len;
    public ResultType (int max, int len) {
        this.max = max;
        this.len = len;
    }
}
public int longestConsecutive(TreeNode root) {
    return helper(root).max;
}

private ResultType helper(TreeNode root) {
    if (root == null) {
        return new ResultType(0, 0);
    }

    ResultType left = helper(root.left);
    ResultType right = helper(root.right);

    int max = 0, len = 0;
    if (root.left != null && root.val == root.left.val - 1) {
        len = Math.max(len, left.len + 1);
    }
    if (root.right != null && root.val == root.right.val - 1) {
        len = Math.max(len, right.len + 1);
    }
    len = Math.max(1, len); // if current node is alone, the len should be 1
    max = Math.max(len, Math.max(left.max, right.max));
    return new ResultType(max, len);
}
```