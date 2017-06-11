# [PartitionList](http://www.lintcode.com/en/problem/partition-list/#)

## Question

Partition a list such that all nodes less than x come before nodes greater than or equal to x.

## Examples

![](https://i.imgur.com/caT6G4p.jpg)

## Analysis

Since the structure has been modified, we need dummy node. We are unsure about what the head node might be, so we need to involve dummy node into our program.

## Code

```java
public ListNode partition(ListNode head, int x) {
    ListNode dummyLeft = new ListNode(0);
    ListNode dummyRight = new ListNode(0);
    ListNode headLeft = dummyLeft;
    ListNode headRight = dummyRight;
    while (head != null) {
        if (head.val < x) {
            headLeft.next = head;
            headLeft = headLeft.next;
        } else {
            headRight.next = head;
            headRight = headRight.next;
        }
        head = head.next;
    }
    // clear and connect
    headRight.next = null; // we need to avoid loops
    headLeft.next = dummyRight.next;
    return dummyLeft.next;
}
```