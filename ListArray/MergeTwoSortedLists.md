# [MergeTwoSortedLists](https://leetcode.com/problems/merge-two-sorted-lists/#/description)

## Question

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

## Examples

1,3,5 and 2,4,6. Return 1,2,3,4,5,6.

## Analysis

We have to use dummy node to preserve head node, otherwise we don't know when to create or copy a head node.

## Code

```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0);
    ListNode head = dummy;
    while (l1 != null && l2 != null) {
        if (l1.val < l2.val) {
            head.next = l1;
            l1 = l1.next;
        } else {
            head.next = l2;
            l2 = l2.next;
        }
        head = head.next;
    }
    if (l1 != null) {
        head.next = l1;
    }
    if (l2 != null) {
        head.next = l2;
    }
    return dummy.next;
}
```