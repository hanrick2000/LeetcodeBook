#### Question
Given a binary tree, find all of its path sum. The path could start and end at any node.
#### Examples
Given 1,2,0,1, return 3

Given 1,2,0,3, return 4
#### Analysis
This question is so hard. The logic is a mess. We need to choose correct result type, otherwise it cannot lead to a solution.
#### Code
 __up__ represents, for current node, the maximum length of consecutive path toward root with increasing order. __down__ represents, for current node, the maximum length of consecutive path toward root with decreasing order.

There are five conditions that may generate a current longest path:
1. max from left subtree
2. max from right subtree
3. left subtree + current node
4. right subtree + current node
5. left subtree + right subtree + current node
```java
private class ResultType {
    int up;
    int down;
    int max;
    public ResultType(int up, int down, int max) {
        this.up = up;
        this.down = down;
        this.max = max;
    }
}
public int longestConsecutive2(TreeNode root) {
    return helper(root).max;
}

private ResultType helper(TreeNode root) {
    if (root == null) {
        return new ResultType(0, 0, 0);
    }
    
    ResultType left = helper(root.left);
    ResultType right = helper(root.right);
    
    // Define returned values
    int up = 0, down = 0, cur = 0;
    // 还是用root.left != null这种表现形式, 因为更加直观, 虽然这个信息确实
    // 是在traverse的时候就能得到.
    if (root.left != null && root.val == root.left.val + 1) {
        up = Math.max(left.up + 1, up);
    }
    if (root.left != null && root.val == root.left.val - 1) {
        down = Math.max(left.down + 1, down);
    }
    if (root.right != null && root.val == root.right.val + 1) {
        up = Math.max(right.up + 1, up);
    }
    if (root.right != null && root.val == root.right.val - 1) {
        down = Math.max(right.down + 1, down);
    }
    cur = up + 1 + down;
    cur = Math.max(cur, Math.max(left.max, right.max));
    return new ResultType(up, down, cur);
}
```

The following is a false example which I didn't solve. This one I was using boolean values to represent path direction.
```java
private class ResultType {
    int cur;
    int max;
    boolean up;
    boolean down;
    public ResultType(int cur, int max, boolean up, boolean down) {
        this.cur = cur;
        this.max = max;
        this.up = up;
        this.down = down;
    }
}
public int longestConsecutive2(TreeNode root) {
    return helper(root).max;
}
    
private ResultType helper(TreeNode root) {
    if (root == null) {
        return new ResultType(0, 0, true, true);
    }
    // Divide 
    ResultType left = helper(root.left);
    ResultType right = helper(root.right);
    
    // Conquer (4 conditions, one more condition might be root is null)
    // 感觉用root.left != null不太好, 因为就不太像纯的回溯了, 因为你往下
    // 遍历其实也可以知道root.left != null, 但是new ResultType(0, 0)是只有
    // 回溯才知道的. 还是root.left != null好一些把, 比较直观.
    ResultType res = new ResultType(1, 1, false, false);
    int leftCur = 0, rightCur = 0;
    if (root.left != null) {
        if (root.val == root.left.val + 1) {
            if (left.up) {
                leftCur = left.cur;
                res.down = false;
            } else {
                leftCur = 1;
                rightCur = 0;
                res.up = false;
            }
        }
        if (root.val == root.left.val - 1) {
            if (left.down) {
                leftCur = left.cur;
                res.up = false;
            } else {
                leftCur = 1;
                rightCur = 0;
                res.down = false;
            }
        }
    }
    if (root.right != null) {
        if (root.val == root.right.val + 1) {
            if (right.up) {
                rightCur = right.cur;
                res.down = false;
            } else {
                rightCur = 1;
                leftCur = 0;
                res.up = false;
            }
        }
        if (root.val == root.right.val - 1) {
            if (right.down) {
                rightCur = right.cur;
                res.up = false;
            } else {
                rightCur = 1;
                leftCur = 0;
                res.down = false;
            }
        }
    }
    if (res.down && res.up) {
        
    }
    res.cur += leftCur + rightCur;
    res.max = Math.max(res.cur, Math.max(left.max, right.max));
    return res;
}
```