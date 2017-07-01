# [SubarraySum](http://www.lintcode.com/en/problem/subarray-sum/)

## Question

Given an integer array, find a subarray where the sum of numbers is zero. Your code should return the index of the first number and the index of the last number.

## Examples

![](https://farm5.staticflickr.com/4054/35603688506_fd7ed0243c_o.jpg)

## Analysis

 A very classic subarray problem!

## Code

```java
// 看清题目, 只需要找出一个即可, 想复杂了, 因为我以为要全部找出来, 只用找一个的话, 就简单了,即便后面的覆盖了也没关系, 找出一个就行了
public ArrayList<Integer> subarraySum(int[] nums) {
    // -3,1,2,-3,4
    // n^2
    // init
    ArrayList<Integer> res = new ArrayList<>();
    int[] sums = new int[nums.length];
    // put sum
    putSum(sums, nums);
    // check zero
    for (int i = 0; i < sums.length; i++) {
        if (sums[i] == 0) {
            res.add(0);
            res.add(i);
            return res;
        }
    }
    // traverse
    // 避免不了 n^2
    for (int i = 1; i < nums.length; i++) {
        for (int j = i; j < nums.length; j++) {
            if (sums[j] - sums[i - 1] == 0) {
                res.add(i);
                res.add(j);
                return res;
            }
        }
    }
    return res;
}
// 相当于小小地利用了一下 memoization, 因为计算和是可以利用之前的结果的
private void putSum(int[] sums, int[] nums) {
    sums[0] = nums[0];
    for (int i = 1; i < nums.length; i++) {
        sums[i] += sums[i - 1] + nums[i];
    }
}

// A simpler solution, 其实复杂度和上面的解法是一样的, 因为上面的解法根本不会进入到第二层循环里
public ArrayList<Integer> subarraySum(int[] nums) {
    // -3,1,2,-3,4
    // n^2 -> n
    // init
    ArrayList<Integer> res = new ArrayList<>();
    // <sum, index>
    Map<Integer, Integer> map = new HashMap<>();
    int sum = 0;
    for (int i = 0; i < nums.length; i++) {
        sum += nums[i];
        if (nums[i] == 0) {
            res.add(i);
            res.add(i);
            break;
        }
        if (sum == 0) {
            res.add(0);
            res.add(i);
            break;
        }
        if (map.containsKey(sum)) {
            res.add(map.get(sum) + 1);
            res.add(i);
            break;
        }
        map.put(sum, i);
    }
    return res;
}

// Best solution!!!
public ArrayList<Integer> subarraySum(int[] nums) {
    // -3,1,2,-3,4
    // n^2 -> n
    // init
    ArrayList<Integer> res = new ArrayList<>();
    // <sum, index>
    // 艹, 三种情况还能归并
    Map<Integer, Integer> map = new HashMap<>();
    int sum = 0;
    // 为了处理 sum == 0的情况, 增加了一个节点
    map.put(0 , -1);
    for (int i = 0; i < nums.length; i++) {
        sum += nums[i];
        // 这个就已经包含了两种情况, 一种是nums[i]自己就等于0, 另一种是
        // 普遍的中间情况
        if (map.containsKey(sum)) {
            res.add(map.get(sum) + 1);
            res.add(i);
            break;
        }
        map.put(sum, i);
    }
    return res;
}
```