# [BinaryTreeSerialization](http://lintcode.com/en/problem/binary-tree-serialization/)

## Question

Serialization is to transfer data structures from memory into string and store them on disk. So it's persistent storage. Common serialization techs are XML, JSON(think it as hashmap), Thrift, ProtoBuf, etc.

## Examples

![](https://farm3.staticflickr.com/2822/33666229764_956a2227d9_o.jpg)

## Analysis

Follow standard BFS procedure illustrated in CLRS. Process nodes when adding them to the queue (including root node). Add pointer and array list to help build up the tree.

## Code

```java
public String serialize(TreeNode root) {
    // Edge cases
    if (root == null) {
        return "";
    }
    // 定义数据结构
    Queue<TreeNode> queue = new LinkedList<>();
    StringBuilder sb = new StringBuilder();
    // 如果把数据处理放在left, right condition里,那关于root的一切处理就得在外面弄
    // BFS始终有两种方法, 第一种是在left, right的时候就处理, 以及在root的时候处理
    // 第二种是在poll出来的时候处理. 按照CLRS来把, 在中间conditon的时候处理.
    queue.offer(root);
    sb.append(root.val);
    sb.append(",");
    while (!queue.isEmpty()) {
        TreeNode curr = queue.poll();
        if (curr.left != null) {
            queue.offer(curr.left);
            sb.append(curr.left.val);
        } else {
            sb.append("#");
        }
        sb.append(",");
        if (curr.right != null) {
            queue.offer(curr.right);
            sb.append(curr.right.val);
        } else {
            sb.append("#");
        }
        sb.append(",");
    }
    // Delete trailing null and delimeter
    for (int i = sb.length() - 1; i >= 0; i--) {
        if (sb.charAt(i) == '#' || sb.charAt(i) == ',') {
            sb.deleteCharAt(i);
        } else {
            break;
        }
    }
    //System.out.println(sb.toString());
    return sb.toString();
}

// Better way, it's using index to track root node, not child node
// But this way is harder to think about
public TreeNode deserialize(String data) {
    if (data.length() == 0) {
        return null;
    }
    // 定义数据结构, 存储所需信息
    // 不可能单靠几个指针就能保留整棵树的信息, 只有依靠队列来存储, 同时思路也
    // 清晰
    String[] nodes = data.split(",");
    ArrayList<TreeNode> list = new ArrayList<>();
    TreeNode root = new TreeNode(Integer.parseInt(nodes[0]));
    list.add(root);
    // for parent node
    int index = 0;
    // 两个作用, 一个是判断当前节点是左节点还是右节点, 第二个是用于判断何时递加index, 这样就可以避免null
    // 和下面另外一个方法的区别在于index追踪的是parent node, 而另外一个追踪的是child node
    boolean isLeftChild = true; 
    for (int i = 1; i < nodes.length; i++) {
        if (!nodes[i].equals("#")) {
            TreeNode node = new TreeNode(Integer.parseInt(nodes[i]));
            if (isLeftChild) {
                list.get(index).left = node;
            } else {
                list.get(index).right = node;
            }
            list.add(node);
        }
        if (!isLeftChild) {
            index++;
        }
        isLeftChild = !isLeftChild;
    }
    return root;
}

// 其实这个方法更美, 和serializa有遥相呼应的感觉, 只是会添加一些冗余的null
public TreeNode deserialize1(String data) {
    if (data.length() == 0) {
        return null;
    }
    // 定义数据结构, 存储所需信息
    // 不可能单靠几个指针就能保留整棵树的信息, 只有依靠队列来存储, 同时思路也
    // 清晰
    String[] nodes = data.split(",");
    ArrayList<TreeNode> list = new ArrayList<>();
    TreeNode root = new TreeNode(Integer.parseInt(nodes[0]));
    list.add(root);
    for (int i = 1; i < nodes.length; i++) {
        if (!nodes[i].equals("#")) {
            list.add(new TreeNode(Integer.parseInt(nodes[i])));
        } else {
            list.add(null);
        }
    }
    // 需要维护一个children的指针, 以加2的方式递进
    // 指针也算是一种数据结构, 存储信息, 说白了这些题目真的就是数据结构加算法
    // 如何用算法来利用之前存储过的信息
    int index = 1;
    for (int i = 0; i < list.size(); i++) {
        TreeNode curr = list.get(i);
        // 跳过null
        if (curr == null) {
            continue;
        }
        if (index < list.size()) {
            curr.left = list.get(index++);
        }
        if (index < list.size()) {
            curr.right = list.get(index++);
        }
    }
    // 2i+1, 2i+2只适合完全树
    return root;
}
```