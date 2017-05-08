# [BinaryTreeLevelList](http://lintcode.com/en/problem/convert-binary-tree-to-linked-lists-by-depth/)

## Question

Convert binary tree to a list of node by level order.

## Examples

![](https://farm3.staticflickr.com/2869/33689756664_2c23a4a831_o.jpg)

## Analysis

Same as level order traversal, but with dummy node.

## Code

```java
public List<ListNode> binaryTreeToLists(TreeNode root) {
    Queue<TreeNode> queue = new LinkedList<>();
    List<ListNode> res = new ArrayList<>();
    if (root == null) {
        return res;
    }
    queue.offer(root);
    while (!queue.isEmpty()) {
        int size = queue.size();
        ListNode node = new ListNode(0);
        ListNode dummy = node;
        for (int i = 0; i < size; i++) {
            TreeNode curr = queue.poll();
            node.next = new ListNode(curr.val);
            node = node.next;
            if (curr.left != null) {
                queue.offer(curr.left);
            }
            if (curr.right != null) {
                queue.offer(curr.right);
            }
        }
        res.add(dummy.next);
    }
    return res;
}
```
