#### Question
Given a binary tree, find all of its path sum. The path doesn’t need to start from root and end at leaf. But it has to be straight down.
#### Examples
![](https://farm3.staticflickr.com/2942/33540904993_6cff1f1cbc_o.jpg)
#### Analysis
This is a so typical question. It's quite hard to solve without Path and Path2 questions. Anyway, the key point is to find all conditions that could lead to a longest path.
#### Code
```java
private class ResultType {
        int max;
        int up;
        int down;
        public ResultType (int max, int up, int down) {
            this.max = max;
            this.up = up;
            this.down = down;
        }
    }
public int longestConsecutive3(MultiTreeNode root) {
    return helper(root).max;
}

private ResultType helper(MultiTreeNode root) {
    if (root == null) {
        return new ResultType(0, 0, 0);
    }
    
    Map<MultiTreeNode, ResultType> results = new HashMap<>();
    for (MultiTreeNode child : root.children) {
        results.put(child, helper(child));
    }
    
    int max = 0, up = 0, down = 0;
    for (MultiTreeNode child : root.children) {
        if (child != null) {
            if (root.val == child.val + 1) {
                up = Math.max(up, results.get(child).up + 1);
            }
            if (root.val == child.val - 1) {
                down = Math.max(down, results.get(child).down + 1);
            }
            if (results.get(child).max > max) {
                max = results.get(child).max;
            }
        }
    }
    int len = up + 1 + down; // 这一句就包含了三种情况
    max = Math.max(len, max);
    return new ResultType(max, up, down);
}
```