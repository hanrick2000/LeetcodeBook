# [ReverseLinkedList2](http://www.lintcode.com/en/problem/reverse-linked-list-ii/)

## Question

Given m, n satisfy the following condition: 1 ≤ m ≤ n ≤ length of list.

## Examples

![](https://farm5.staticflickr.com/4288/35231132145_de2f4d8b28_o.jpg)

## Analysis

- We must use dummy node, and define clear APIs.

## Code

```java
public ListNode reverseBetween(ListNode head, int m , int n) {
    // edge case
    if (head == null) {
        return null;
    }
    // dummy node
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    head = dummy;
    // move to mth node
    int pos = 0;
    while (pos < m - 1) {
        head = head.next;
        pos++;
    }
    ListNode start = head;
    // reverse
    reverseNextNodes(start, n - m + 1);
    return dummy.next;
}

// reverse next number of nodes, and return the reversed list
// head -> 2,3,4,5 return head -> 4,3,2,5
private void reverseNextNodes(ListNode head, int num) {
    ListNode prevHead = head;
    // move to nth node
    ListNode pointer = head;
    int pos = 0;
    while (pos < num) {
        pointer = pointer.next;
        pos++;
    }
    ListNode next = pointer.next;
    // reverse
    head = head.next;
    ListNode prev = pointer.next;
    while (head != next) {
        ListNode temp = head.next;
        head.next = prev;
        prev = head;
        head = temp;
    }
    // connect
    prevHead.next = prev;
}
```