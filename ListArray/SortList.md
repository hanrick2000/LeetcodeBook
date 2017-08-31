# [SortList](http://lintcode.com/en/problem/sort-list/#)

## Question

Sort a linked list in O(nlogn) using constant space.

## Examples

1,2,3 -> 3,2,1

## Analysis

Still first think about dummy node.

## Code

```java
public ListNode sortList(ListNode head) {
    if (head == null) {
        return head;
    }

    // We don't need to use dummy here, because sort method will change the
    // position of dummy itself.
    return sort(head);
}

// Merge sort a list
private ListNode sort(ListNode head) {
    // head could be null, because of mid.next
    if (head == null || head.next == null) {
        return head;
    }

    // findMid is O(n)
    ListNode mid = findMid(head);
    ListNode right = sort(mid.next);
    mid.next = null;
    ListNode left = sort(head);
    // Merge is O(n)
    return merge(left, right);
}

// Merge two sorted (recursive) lists (not null)
private ListNode merge(ListNode head1, ListNode head2) {
    ListNode dummy = new ListNode(0);
    ListNode newHead = dummy;
    while (head1 != null && head2 != null) {
        if (head1.val < head2.val) {
            newHead.next = head1;
            head1 = head1.next;
        } else {
            newHead.next = head2;
            head2 = head2.next;
        }
        newHead = newHead.next;
    }

    if (head1 != null) {
        newHead.next = head1;  
    }

    if (head2 != null) {
        newHead.next = head2;
    }

    return dummy.next;
}

private ListNode findMid(ListNode head) {
    ListNode slow = head;
    // initial fast has to be head.next, so that during recursion, findMid
    // can be narrowed down to a list with only one node.
    ListNode fast = head.next;
    while(fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow;
}
```