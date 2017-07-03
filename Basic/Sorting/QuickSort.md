# [QuickSort](http://www.geeksforgeeks.org/quick-sort/)

## Question

Given an integer array, sort it in ascending order. Use quick sort, merge sort, heap sort or any O(nlogn) algorithm.

## Examples

Given 3,2,1,4,5, return 1,2,3,4,5.

## Analysis

Quick sort implementation. The key part is partition algorithm.

Each time when we are doing a partition, we hope that left part and right part have identical number of elements.

How to do the partition?

- The number of elements that are smaller than pivot is equal to the number of elements that are greater than pivot.

How to analyze time complexity?

Worst case is that each time we choose the min or max pivot.

The key point is that how to partition.

这个快排是可以排, 但是有个漏洞啊, 你的 pivot 实际上的这个 element 可能最后并不在中间, 而是混在了左边或者右边里, 那这样用 quick select 就不行了. 尝试了在此版本基础上去做 quick select, 但是情况太多了, 没有意义. 那这个算法没有普适性啊, 只是说给我的quick select 做了个引子, 因为我最后需要的还是

## Code

```java
public void sortIntegers2(int[] A) {
    // Quick sort
    // Basically it's a divide-and-conquer algorithm, which is implemented
    // with recursion
    if (A.length == 0) {
        return;
    }
    quickSort(0, A.length - 1, A);
}

// start: start index
// end: last index
// A: array to sort
private void quickSort(int start, int end, int[] A) {
    // return
    if (start >= end) {
        return;
    }
    // 快排也太难些了把
    // choose pivot and init pointers
    // 第一个关键在于, pivot只是随机选择的一个值而已, 指针才是重要的. 既是
    // 用来分配pivot 两端的值的, 也是划分下一次 quickSort 的界线的
    // How to choose?
    // Don't choose first or last value as pivot, since if the array is sorted
    // then the solution is n^2. If we just choose other positions like mid,
    // then the worst case is that we choose max or min each time, whihc is
    // of a lot lower possibility.
    // Array 的普遍特殊情况
    // Three conditions:
    // 1. pivot is max or min value
    // 2. pivot is a normal mid value
    // 3. there are only 1 or 2 or 3 numbers in the array, numbers are all 
    // the same
    int left = start, right = end;
    int pivot = A[(start + end) / 2];
    // 第二个关键在于, 要让 left 和 right 彻底分开, 不能允许 left == right
    // 的时候停止, 如果这样, 那中间的left == right 那个数如何自处?
    // < pivot, 不能用<= pivot, 因为 if 语句会帮助处理了
    // 反正必须把 left 和 right分开, 不然当只有两个元素时, 会发生死循环.
    // 如果是<= pivot, 那 right 可能一路减减到0, 如果 pivot 恰好是最小值.
    while (left <= right) {
        while (left <= right && A[left] < pivot) {
            left++;
        }
        while (left <= right && A[right] > pivot) {
            right--;
        }
        if (left <= right) {
            int temp = A[right];
            A[right] = A[left];
            A[left] = temp;
            left++;
            right--;
        }
    }
    // start to left - 1 are smaller
    // right + 1 to end are greater
    quickSort(start, right, A);
    quickSort(left, end, A);
}
```