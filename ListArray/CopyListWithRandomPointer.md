# [CopyListWithRandomPointer](http://lintcode.com/en/problem/copy-list-with-random-pointer/#)

## Question

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

## Examples

1,2,3,4 -> 1,2,3,4

## Analysis

Normal deep copy.

Use dummy node.

Break down a big problem into smaller ones. Write logic like `head.next = head;` first, because anyway they will be called.

## Code

```java
public RandomListNode copyRandomList(RandomListNode head) {
    // write your code here
    // 1. traverse
    // 2. create dummy
    // 3. create new current node
    // 4. assign random pointer, we need a map here, using set will lose references
    // 5. combine and refactor
    RandomListNode newHead = new RandomListNode(head.label);
    RandomListNode dummy = new RandomListNode(0);
    dummy.next = newHead;
    newHead = dummy;
    Map<RandomListNode, RandomListNode> oldToNew = new HashMap<>();
    while (head != null) {
        int label = head.label;
        RandomListNode newNode;
        if (oldToNew.containsKey(head)) {
            newNode = oldToNew.get(head);
        } else {
            newNode = new RandomListNode(label);
            oldToNew.put(head, newNode);
        }

        RandomListNode random = head.random;
        if (random != null) {
            if (oldToNew.containsKey(random)) {
                newNode.random = oldToNew.get(random);
            } else {
                newNode.random = new RandomListNode(random.label);
                oldToNew.put(random, newNode.random);
            }
        }
        head = head.next;
        newHead.next = newNode;
        newHead = newHead.next;
    }
    return dummy.next;
}
```