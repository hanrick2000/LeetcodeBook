# [TopKLargestNumbers](http://www.lintcode.com/en/problem/top-k-largest-numbers/#)

## Question

Given an integer array, find the top k largest numbers in it.

## Examples

Given [3,10,1000,-99,4,100] and k = 3.

Return [1000, 100, 10].

## Analysis

Almost the same with kth largest element by just using a min heap.

## Code

```java
public int[] topk(int[] nums, int k) {
    int[] res = new int[k];
    PriorityQueue<Integer> minHeap = new PriorityQueue<>(k);
    for (int i = 0; i < nums.length; i++) {
        minHeap.offer(nums[i]);
        if (minHeap.size() > k) {
            minHeap.poll();
        }
    }

    for (int i = res.length - 1; i >= 0; i--) {
        res[i] = minHeap.poll();
    }

    return res;
}
```