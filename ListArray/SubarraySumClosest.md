# [SubarraySumClosest](http://www.lintcode.com/en/problem/subarray-sum-closest/#)

## Question

Given an integer array, find a subarray with sum closest to zero. Return the indexes of the first number and last number.

## Examples

![](https://farm5.staticflickr.com/4216/35524940171_35b5ca783f_o.jpg)

## Analysis

There is not much trick actually, just use the subarray point and create a data structure to keep track of index, then we are done.

## Code

```java
private class Pair {
    public int index;
    public int sum;

    public Pair(int index, int sum) {
        this.index = index;
        this.sum = sum;
    }
}

public int[] subarraySumClosest(int[] nums) {
    // Subarray prefix sum
    Pair[] prefixSum = new Pair[nums.length + 1];
    prefixSum[0] = new Pair(0, 0);
    for (int i = 0; i < nums.length; i++) {
        prefixSum[i + 1] = new Pair(i + 1, prefixSum[i].sum + nums[i]);
    }

    // nlogn
    Arrays.sort(prefixSum, new Comparator<Pair>(){
        @Override
        public int compare(Pair a, Pair b) {
            return Integer.compare(a.sum, b.sum);
        }
    });
    int cloestSum = Integer.MAX_VALUE;
    int first = 0, last = 0;
    // n
    for (int i = 0; i < prefixSum.length - 1; i++) {
        // System.out.println(prefixSum[i].sum);
        // System.out.println(prefixSum[i].index);
        int sum = prefixSum[i + 1].sum - prefixSum[i].sum;
        if (sum < cloestSum) {
            cloestSum = sum;
            // 记住是前 i 个和前 i + 1个, 比如前3个减前1个, 那得到的 index 其实是[1,2]
            first = prefixSum[i].index < prefixSum[i + 1].index ? prefixSum[i].index: prefixSum[i + 1].index;
            last = prefixSum[i].index < prefixSum[i + 1].index ? prefixSum[i + 1].index - 1 : prefixSum[i].index - 1;
        }
    }

    return new int[]{first, last};
}
```