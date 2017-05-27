# [ReverseLinkedList](http://www.lintcode.com/en/problem/reverse-linked-list/#)

## Question

Reverse a linked list.

## Examples

![](https://farm5.staticflickr.com/4251/34924998315_7c99e486b5_o.jpg)

## Analysis

Use two pointers. This question is actually about moving two pointers `curr` and `prev`.

## Code

```java
public ListNode reverse(ListNode head) {
    // write your code here
    ListNode prev = null;
    ListNode curr = head;
    while (curr != null) {
        ListNode temp = curr.next;
        curr.next = prev;
        prev = curr;
        curr = temp;
    }
    return prev;
}
```