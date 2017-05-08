# [ZigZagLevelOrder](http://lintcode.com/en/problem/binary-tree-zigzag-level-order-traversal/)

## Question

Level order traversal, from left to right, then from right to left.

## Examples

![](https://farm5.staticflickr.com/4164/34398113151_f17e1087ca_o.jpg)

## Analysis

Just follow CLRS BFS standard, which is a little verbose, but clear and helpful. Actually for now, I find CLRS standard works well on graph questions, but it's a little verbose on tree questions. Anyway, I think CLRS standard can be helpful on complicated questions.

## Code

```java
ArrayList<ArrayList<Integer>> res = new ArrayList<>();
    Stack<TreeNode> stack1 = new Stack<>();
    Stack<TreeNode> stack2 = new Stack<>();
    if (root == null) {
        return res;
    }
    stack1.push(root);
    ArrayList<Integer> rootList = new ArrayList<>();
    rootList.add(root.val);
    res.add(rootList);
    // 思考清楚, 还是用的CLRS遍历到的时候就算访问了, 也就是顺序就决定了
    while (!stack1.isEmpty() || !stack2.isEmpty()) {
        int size1 = stack1.size();
        ArrayList<Integer> temp1 = new ArrayList<>();
        for (int i = 0; i < size1; i++) {
            TreeNode curr = stack1.pop();
            if (curr.right != null) {
                stack2.push(curr.right);
                temp1.add(curr.right.val);
            }
            if (curr.left != null) {
                stack2.push(curr.left);
                temp1.add(curr.left.val);
            }
        }
        if (temp1.size() > 0) {
            res.add(temp1);
        }
        int size2 = stack2.size();
        ArrayList<Integer> temp2 = new ArrayList<>();
        for (int i = 0; i < size2; i++) {
            TreeNode curr = stack2.pop();
            if (curr.left != null) {
                stack1.push(curr.left);
                temp2.add(curr.left.val);
            }
            if (curr.right != null) {
                stack1.push(curr.right);
                temp2.add(curr.right.val);
            }
        }
        if (temp2.size() > 0) {
            res.add(temp2);
        }
    }
    return res;
```
