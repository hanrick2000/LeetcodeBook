#### Question
Given a binary tree, find all of its path sum. The path doesn’t need to start from root and end at leaf. But it has to be straight down.
#### Examples
![](https://farm3.staticflickr.com/2807/33509682064_25fc55d14e_o.jpg)
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
    
    int max = 0, up = 0, down = 0;
    for (MultiTreeNode child : root.children) {
        ResultType res = helper(child);
        if (child != null) {
            if (root.val == child.val + 1) {
                up = Math.max(up, res.up + 1);
            }
            if (root.val == child.val - 1) {
                down = Math.max(down, res.down + 1);
            }
            max = Math.max(max, res.max);
        }
    }
    int len = up + 1 + down; // 这一句就包含了三种情况
    max = Math.max(len, max);
    return new ResultType(max, up, down);
}
```