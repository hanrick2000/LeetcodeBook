# [KthLargestElement](http://lintcode.com/en/problem/kth-largest-element/#)

## Question

Find kth largest element.

## Examples

[9,3,2,4,8], k = 3, return 4

## Analysis

Three solutions.

## Code

```java
// First solution, O(kn)
public int kthLargestElement(int k, int[] nums) {
    // We can have three solutions to solve this problem. First one is to just traverse for k times.
    if (k > nums.length) {
        return 0;
    }

    for (int i = 0; i < k; i++) {
        int max = Integer.MIN_VALUE;
        int maxIndex = 0;
        for (int j = 0; j < nums.length - i; j++) {
            if (nums[j] > max) {
                max = nums[j];
                maxIndex = j;
            }
        }

        swap(nums, maxIndex, nums.length - i - 1);
    }

    return nums[nums.length - k];
}

private void swap(int[] nums, int i, int j) {
    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
}

// Second solution using max heap
public int kthLargestElement(int k, int[] nums) {
    // Should use min heap
    // PriorityQueue<Integer> queue = new PriorityQueue<>(k, new IncreasingComparator());
    PriorityQueue<Integer> queue = new PriorityQueue<>(k, new Comparator<Integer>(){
       @Override
       public int compare(Integer a, Integer b) {
           return a.compareTo(b);
       }
    });
    for (int i = 0; i < k; i++) {
        queue.offer(nums[i]);
    }

    for (int i = k; i < nums.length; i++) {
        if (nums[i] > queue.peek()) {
            queue.poll();
            queue.offer(nums[i]);
        }
    }

    return queue.peek();
}

private class IncreasingComparator implements Comparator<Integer> {
    @Override
    public int compare(Integer a, Integer b) {
        return a.compareTo(b);
    }
}

// Best solution using quick select written by myself
public int kthLargestElement(int k, int[] nums) {
    // Quick select
    return findKthLargest(nums, 0, nums.length - 1, k);
}

private int findKthLargest(int[] nums, int start, int end, int k) {
    int pivotPos = partition(nums, start, end);
    int target = nums.length - k;
    if (pivotPos == target) {
        return nums[pivotPos];
    }

    if (pivotPos < target) {
        // narrow down scope since we've already checked pivotPos
        return findKthLargest(nums, pivotPos + 1, end, k);
    } else {
        return findKthLargest(nums, start, pivotPos - 1, k);
    }
}

// Return pivot index
// 双指针是真的恶心啊!!!
// 还有可能需要考虑一下数组有没有可能越界
private int partition(int[] nums, int start, int end) {
    // edge case 有, start == end, start + 1 == end, 这两种情况很关键.
    int pivot = nums[start];
    int pivotPos = start;
    // 更容易理解, 把第一个位置预留给 pivot
    start++;
    // 对撞型指针, 肯定是会先到达一个状态也就是 start == end, 对撞. 找清楚这个是最重要的, final state 肯定是两个指针对撞.
    while (start <= end) {
        while (start <= end && nums[start] < pivot) {
            start++;
        }

        // < and >= should be comparable so that it can make sure that two pointers can move forward always
        // Note that end pointer could point to an element that is smaller than pivot, also it's possible it points to an element greater than pivot!!! So assume, when start reaches end, no matter it's small or great, start pointer can always move forward! 有可能end 指针还没动, start 就撞上去了.
        while (start <= end && nums[end] >= pivot) {
            end--;
        }

        if (start <= end) {
            swap(nums, start, end);
        } else {
            swap(nums, pivotPos, end);
        }
    }

    // We must make sure that end pointer always points to an element that is smaller than pivot!!!
    return end;
}

private void swap(int[] nums, int i, int j) {
    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
}
```