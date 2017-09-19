# [PartitionArray](http://lintcode.com/en/problem/partition-array/#)

## Question

![](https://i.imgur.com/3U3vJUS.jpg)

## Examples

Given [3,2,2,1] and k = 2, return 1.

## Analysis

Just a follow-up to quick select. But it's quite basic, it's not even using recursion. Actually still quick sort it the most complicated one.

## Code

```java
public int partitionArray(int[] nums, int k) {
    // [1,2], k = 1  [1,2], k = 2  [1,2] k = 3
    int start = 0, end = nums.length - 1;
    while (start <= end) {
        while (start <= end && nums[start] < k) {
            start++;
        }

        while (start <= end && nums[end] >= k) {
            end--;
        }

        if (start <= end) {
            swap(nums, start, end);
            start++;
            end--;
        }
    }

    // Actually we don't need this, because at most start is nums.length
    if (start >= nums.length) {
        return nums.length;
    }

    return start;
}

private void swap(int[] nums, int x, int y) {
    int temp = nums[x];
    nums[x] = nums[y];
    nums[y] = temp;
}
```