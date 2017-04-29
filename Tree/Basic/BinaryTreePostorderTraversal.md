#### Question
Given a tree node, return a list of int values which represent the postorder traversal. 

#### Examples
Given 1,2,3,4,5,6,7 return 4,5,2,6,7,3,1

#### Solution
Need to understand why postorder uses if conditon but not while condition like inorder traversal, and why we need to use prev pointer. 

#### Analysis
Time: O(n)  
Space: O(1)

#### Code

* Recursion

```java
public static List<Integer> postorder(TreeNode root){
    List<Integer> res = new ArrayList<>();
    helper(res, root);
    return res;
}

public static void helper(List<Integer> res, TreeNode root) {
    if (root == null) {
        return;
    }
    helper(res, root.left);
    helper(res, root.right);
    res.add(root.val);
}
```

* Iterative

```java
public static List<Integer> postorder(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    Stack<TreeNode> stack = new Stack<>();
    // 得保留一个之前的node链接, 在回溯时prev就成为root了
    TreeNode prev = null;
    TreeNode curr = root;
    if (root != null) {
        stack.push(root);
    }
    // 一句话概括, 就是按照递归的顺序push节点
    // stack.push()就等于递归里的遍历到了这个点
    while (!stack.isEmpty()) {
        // 这里用peek, 只有在add完之后才pop.
        curr = stack.peek();
        if (prev == null || prev.left == curr || prev.right == curr) {
            if (curr.left != null) {
                stack.push(curr.left);
            } else if (curr.right != null) {
                stack.push(curr.right);
            }
        } else if (curr.left == prev) {
            if (curr.right != null) {
                stack.push(curr.right);
            }
        } else {
            // 加完了, 没用了当然就需要pop了, 也就是之后都不会再
            // 访问该节点了. 
            res.add(curr.val);
            stack.pop();
        }
        prev = curr; // 向下和回溯都需要更新prev
    }
    return res;
}
```
