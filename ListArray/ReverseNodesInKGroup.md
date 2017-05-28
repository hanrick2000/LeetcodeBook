# [ReverseNodesInKGroup](http://www.lintcode.com/en/problem/reverse-nodes-in-k-group/)

## Question

Reverse the nodes of a linked list k at a time. Only constant memory is allowed.

## Examples

![](https://farm5.staticflickr.com/4170/34655935401_01f799a9d9_o.jpg)

## Analysis

- My ideas
  - Write a `reverse` method.
  - One while loop.
  - Change values and length pointer at the same time, or get length first and change values.
- Solution
  - Adding **dummy node** is the key point, since the head node will actually be a different one. So we need `dummy = new ListNode(0)`, but if the head node won't change, I think we can just copy the head node by `dummy = head` to store information.
  - The question requires a clear understanding about how to use temporary variables.

## Code

```java
// 我在如何保留第一个reverseK的头部纠结了好久, 而答案显示其实只要加入一个dummy node就行了, 相当于把dummy node也作为list的一部分考虑进去了. 这样就可以把该做的操作都封装在一起.
// 反正宗旨就是, 把结构会被改变的点都扔到list里, 最常见的就是dummy node.
public ListNode reverseKGroup(ListNode head, int k) {
    // add dummy node
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    // add dummy as part of list
    head = dummy;
    while (head != null) {
        // reverse next k nodes and return next node
        head = reverseNextK(head, k);
    }
    return dummy.next;
}

// head -> n1 -> n2 -> ... -> nk -> nk+1
// head -> nk -> ... -> n2 -> n1 -> nk+1
private ListNode reverseNextK(ListNode head, int k) {
    ListNode n1 = head.next;
    // n is just a pointer used to traverse
    ListNode n = head;
    // get nk
    for (int i = 0; i < k; i++) {
        n = n.next;
        // if there are less than k nodes
        if (n == null) {
            return null;
        }
    }
    ListNode nk = n;
    // reverse
    ListNode prev = null;
    ListNode curr = n1;
    ListNode nkplus = nk.next;
    while (curr != nkplus) {
        ListNode temp = curr.next;
        curr.next = prev;
        prev = curr;
        curr = temp;
    }
    // connect
    head.next = nk;
    n1.next = nkplus;
    return n1;
}
```