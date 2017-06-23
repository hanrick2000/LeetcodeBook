# [RotateList](http://www.lintcode.com/en/problem/rotate-list/#)

## Question

Rotate a given list to the right by k places.

## Examples

![](https://farm5.staticflickr.com/4214/34668254693_afcb5dc7e7_o.jpg)

## Analysis

It's hard to understand `by k`. And it might be a better a solution that we use fast and slow pointers.

We should put `end.next = dummy.next` at first line.

## Code

```java
public ListNode rotateRight(ListNode head, int k) {
    // edge cases:
    // 1. head = null
    // 2. k >= length
    // 3. k = 0

    // edge
    if (head == null) {
        return null;
    }

    // get length
    int length = getLength(head);

    // Create dummy node
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    head = dummy;

    // move to end
    ListNode end = getLastNode(head);

    // move to length - k
    k = k % length;
    int pos = 0;
    while (pos < length - k) {
        head = head.next;
        pos++;
    }

    // reverse
    // put `end.next = dummy.next` as first, otherwise one edge case would fail, k = 0, head = 1->null
    // Always assign `prev` when reversing a linked list
    end.next = dummy.next; // important!!!
    dummy.next = head.next;
    head.next = null;
    return dummy.next;
}

// 没毛病的, 其实就可以想象成一个链条, 自己用手指着数数, 最开始不就是0吗,
// 一直到最后一个, 就是n个了
// 只是说平时我们用手来数数, 没有null和0这两种概念
// 0或者说null这个概念, 在我们生活的逻辑中经常被忽视, 所以导致编程的时候
// 不是很习惯. 因为没有就是没有, 没看到就是没有, 不存在说我非要拿一个东西
// 出来代表null这个东西. 只要拿出了null这种实体, 那就输了. 所以逻辑上不太
// 习惯.
// 永远记住, CS是来自于生活的抽象, 就像Paxos的作者所说一样, 我这平时的生活
// 经验都积累了二十几年了, 何尝不把这些经验利用进CS的学习中呢, 相当于就是在
// 自己的技术上加了二十几年的岁月之力, 真的牛逼.
private int getLength(ListNode head) {
    int len = 0;
    while (head != null) {
        head = head.next;
        len++;
    }
    return len;
}

private ListNode getLastNode(ListNode head) {
    while (head.next != null) {
        head = head.next;
    }
    return head;
}
```