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

## Code

```java

```