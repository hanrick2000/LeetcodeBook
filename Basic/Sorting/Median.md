# [Median](http://www.lintcode.com/en/problem/median/#)

## Question

Given a unsorted array with integers, find the median of it. **A median is the middle number of the array after it is sorted**. If there are even numbers in the array, return the N/2-th number after sorted.

## Examples

![](https://farm5.staticflickr.com/4210/35511690012_5c105ce1b4_o.jpg)

## Analysis

nlogn solution is quite straightforward.

## Code

```java
// Most simple solution, O(nlogn)
public int median(int[] nums) {
    if (nums.length == 0) {
        return 0;
    }
    Arrays.sort(nums);
    // notice the number is nums.length - 1, not nums.length
    return nums[(nums.length - 1) / 2];
}

// More complicated solution! 看似复杂, 其实思路颇为清晰, 主要思想是, 保留 pivot 的 index.
public int median(int[] nums) {
    // 感觉只需要 partition 一半就行了
    if (nums.length == 1) {
        return nums[0];
    }
    return partition(0, nums.length - 1, nums, (nums.length - 1) / 2);
}

// partition given array and return pivot index, if the pivot index is
// the middle index, then we get it
private int partition(int start, int end, int[] nums, int index) {
    int left = start, right = end + 1; //因为先++和--了
    int pivot = nums[start];
    while (true) {
        // 其实双指针碰撞别想那么复杂, 就是两种情况, 左指针从左边而来, 
        // 撞上右指针, 而右指针此刻的状态是什么? 右指针从右边而来, 左指针的
        // 状态是什么?
        while (nums[++left] < pivot) {
            if (left == end) {
                break;
            }
        }
        // right 最后停留的肯定是一个大于 pivot 的值, 因为交换过了
        while (nums[--right] > pivot) {
            if (right == start) {
                break;
            }
        }
        // 而且最后 left 和 right 指针一定是错开的
        // 其实关键是判断右指针此刻指向的一定是最后一个小于等于 pivot 的数
        // 直接 break 了, 不能执行 swap, 如果把条件写在 while里, 会去执行
        // swap
        if (left >= right) {
            break;
        }
        swap(nums, left, right);
    }
    swap(nums, start, right);
    // return
    if (right == index) {
        return nums[right];
    }
    // recursion
    if (right < index) {
        return partition(left, end, nums, index);
    } else {
        return partition(start, right - 1, nums, index);
    }
}

// swap function
private void swap(int[] nums, int left, int right) {
    int temp = nums[left];
    nums[left] = nums[right];
    nums[right] = temp;
}
```