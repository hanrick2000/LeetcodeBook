# [KthLargestElement2](http://www.lintcode.com/en/problem/kth-largest-element-ii/#)

## Question

Find K-th largest element in an array. and N is much larger than k.

## Examples

In array [9,3,2,4,8], the 3rd largest element is 4.

In array [1,2,3,4,5], the 1st largest element is 5, 2nd largest element is 4, 3rd largest element is 3 and etc.

## Analysis

Totally the same question with kth largest element but using min heap.

## Code

```java
public int kthLargestElement2(int[] nums, int k) {
    // min heap
    PriorityQueue<Integer> maxHeap = new PriorityQueue<>(k);
    for (int i = 0; i < nums.length; i++) {
        maxHeap.offer(nums[i]);
        if (maxHeap.size() > k) {
            maxHeap.poll();
        }
    }

    return maxHeap.peek();
}
```