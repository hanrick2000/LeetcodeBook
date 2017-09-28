# [TwoSumDifferenceEqual]()

## Question

Given an array of integers, find two numbers that their difference equals to a target value, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are NOT zero-based.

## Examples

Given nums = [2, 7, 15, 24], target = 5

return [1, 2] (7 - 2 = 5)

## Analysis

Still use 变量控制法, 会轻易发现是同向指针.

## Code

```java
// Standard two pointers solution
private class Pair {
    public int index;
    public int val;
    public Pair(int index, int val) {
        this.index = index;
        this.val = val;
    }
}

public int[] twoSum7(int[] nums, int target) {
    if (nums.length <= 1) {
        return null;
    }

    Pair[] pairs = new Pair[nums.length];
    for (int i = 0; i < nums.length; i++) {
        pairs[i] = new Pair(i, nums[i]);
    }

    Arrays.sort(pairs, new Comparator<Pair>(){
        public int compare(Pair p1, Pair p2) {
            return p1.val - p2.val;
        }
    });
    int left = 0, right = 1;
    if (target < 0) {
        target = -target;
    }

    while (right < pairs.length) {
        int diff = pairs[right].val - pairs[left].val;
        if (left == right) {
            right++;
        }

        if (diff < target) {
            right++;
        } else if (diff > target) {
            left++;
        } else {
            if (pairs[left].index < pairs[right].index) {
                return new int[]{pairs[left].index + 1, pairs[right].index + 1};
            } else {
                return new int[]{pairs[right].index + 1, pairs[left].index + 1};
            }

        }
    }

    return new int[]{};
}

// My HashMap solution

public int[] twoSum7(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        if (map.containsKey(nums[i] + target)) {
            return new int[]{map.get(nums[i] + target) + 1, i + 1};
        }

        if (map.containsKey(nums[i] - target)) {
            return new int[]{map.get(nums[i] - target) + 1, i + 1};
        }

        map.put(nums[i], i);
    }

    return null;
}
```