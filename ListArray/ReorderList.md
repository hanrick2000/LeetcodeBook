# [ReorderList](http://www.lintcode.com/en/problem/reorder-list/)

## Question

Reverse the half rest of given list, and merge as a reordered list.

## Examples

![](https://farm5.staticflickr.com/4279/35093015610_9305de8155_o.jpg)

## Analysis

Three points here:

- Dummy node is used to avoid edge cases so we don't need to check if this head is null or not when using head.next. We just use dummy.next.
- Dummy node is used to preserve head node when we need to traverse this list.
- Dummy node is used to construct a linked list when we don't know which node could be the head node.

BTW, use for loop to move forward steps.

## Code

```java
public void reorderList(ListNode head) {
    // 还是写复杂了啊!!! 不要盲目使用dummy node, 还是要把整个过程给拆开来才行.
    if (head == null) {
        return;
    }
    // dummy1
    ListNode dummy1 = new ListNode(0);
    dummy1.next = head;
    head = dummy1;

    // dummy2
    ListNode dummy2 = new ListNode(0);

    // split
    int length = getLength(dummy1.next);
    for (int i = 0; i < length / 2; i++) {
        // 从dummy开始, 走两步
        // 走多少步停止这种, 感觉还是用for loop比较清楚
        // 永远记住, while或者for loop都一样, 跳出去之后, 当前的状态, 肯定
        // 就是第一个不满足condition的状态.
        // 比如这个从i = 0开始length / 2是2, 其实就是往前走两步, 所以现在在第三步
        head = head.next;
    }

    // clear
    dummy2.next = head.next;
    head.next = null;

    // reverse
    dummy2.next = reverse(dummy2.next);
    // merge two given lists
    merge(dummy1.next, dummy2.next);
}

// merge l2 into l1
private void merge(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0);
    ListNode head = dummy;
    int count = 0;
    while (l1 != null && l2 != null) {
        count++;
        if (count % 2 == 0) {
            head.next = l2;
            l2 = l2.next;
        } else {
            head.next = l1;
            l1 = l1.next;
        }
        head = head.next;
    }
    if (l1 != null) {
        head.next = l1;
    }
    if (l2 != null) {
        head.next = l2;
    }
}

// reverse a linked list
private ListNode reverse(ListNode head) {
    ListNode prev = null;
    while (head != null) {
        ListNode temp = head.next;
        head.next = prev;
        prev = head;
        head = temp;
    }
    return prev;
}

// get length of a linked list
private int getLength(ListNode head) {
    int len = 0;
    while (head != null) {
        head = head.next;
        len++;
    }
    return len;
}
```