# [InsertIntoCyclicSortedList](http://www.lintcode.com/en/problem/insert-into-a-cyclic-sorted-list/#)

## Question

Given a node in a cyclic sorted linked list, insert a new node into the list, and return this new node.

## Examples

![](https://farm5.staticflickr.com/4172/34603361531_b90c07d291_o.jpg)

## Analysis

Slow and fast pointers are a key point in linked list problems. But actually this problem doesn't need slow and fast pointers.

## Code

```java
// A simple version
public ListNode insert(ListNode node, int x) {
    // linkedlist 一共就那么几种 API
    // find(), insert(), delete(), reverse()
    ListNode newNode = new ListNode(x);
    if (node == null) {
        newNode.next = newNode;
        return newNode;
    }
    ListNode head = node;
    node = node.next;
    while (head != node) {
        // check
        if (node.val < x && node.next.val > x || node.val == x) {
            break;
        }
        node = node.next;
    }
    insertAfter(node, newNode);
    return newNode;
}

private void insertAfter(ListNode head, ListNode newNode) {
    ListNode next = head.next;
    head.next = newNode;
    newNode.next = next;
}

// A tricky version
public ListNode insert(ListNode node, int x) {
    // linkedlist 一共就那么几种 API
    // find(), insert(), delete(), reverse()
    ListNode newNode = new ListNode(x);
    if (node == null) {
        newNode.next = newNode;
        return newNode;
    }
    ListNode slow = node.next;
    ListNode fast = node.next.next;
    while (fast != slow) {
        fast = fast.next.next;
        slow = slow.next;
        // check
        if (slow.val < x && slow.next.val > x || slow.val == x) {
            insertAfter(slow, newNode);
            return newNode;
        }
    }
    insertAfter(slow, newNode);
    return newNode;
}

private void insertAfter(ListNode head, ListNode newNode) {
    ListNode next = head.next;
    head.next = newNode;
    newNode.next = next;
}
```