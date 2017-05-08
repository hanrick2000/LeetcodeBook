# [LevelOrderTraversal2](http://lintcode.com/en/problem/binary-tree-level-order-traversal-ii/)

## Question

Return level order traversal from bottom to top.

## Examples

![](https://farm3.staticflickr.com/2837/34366392332_4f0b4a44dd_o.jpg)

## Analysis

BFS must have operations like removing elements from the queue, otherwise the `while(!queue.isEmpty())` cannot end. By the way, this question can actually be simplified using normal level order traversal method, combined with `Collections.reverse(res)`. But I have to know about deque, which is much more powerful than queue.

## Code

```java
public ArrayList<ArrayList<Integer>> levelOrderBottom(TreeNode root) {
    ArrayList<ArrayList<Integer>> res = new ArrayList<>();
    Deque<TreeNode> queue = new LinkedList<>();
    Deque<TreeNode> queue2 = new LinkedList<>();
    ArrayList<Integer> sizes = new ArrayList<>();
    if (root == null) {
        return res;
    }
    queue.addFirst(root);
    // get sizes
    while (!queue.isEmpty()) {
        int size = queue.size();
        sizes.add(size);
        for (int i = 0; i < size; i++) {
            TreeNode curr = queue.removeLast();
            queue2.addFirst(curr);
            if (curr.right != null) {
                queue.addFirst(curr.right);
            }
            if (curr.left != null) {
                queue.addFirst(curr.left);
            }
        }
    }
    //System.out.println(sizes);
    // add to res
    while (!queue2.isEmpty()) {
        for (int i = sizes.size() - 1; i >= 0; i--) {
            ArrayList<Integer> temp = new ArrayList<>();
            for (int j = 0; j < sizes.get(i); j++) {
                TreeNode curr = queue2.removeFirst();
                //System.out.println(curr.val);
                temp.add(curr.val);
            }
            res.add(temp);
        }
    }
    return res;
}
```