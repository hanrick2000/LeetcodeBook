# [3Sum](http://lintcode.com/en/problem/3sum/#)

## Question

Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Notice

Elements in a triplet (a,b,c) must be in non-descending order. (ie, a ≤ b ≤ c)

The solution set must not contain duplicate triplets.

## Examples

For example, given array S = {-1 0 1 2 -1 -4}, A solution set is:

(-1, 0, 1)

(-1, -1, 2)

## Analysis

Such questions you have to find the meaning of your traversal. For this question, it should be traverse through the array, and get the biggest number in those three numbers.

Also, we should be able to guess the solution by estimating the running time, the brute force solution is O(n^3) for this question, so the optimal one could be O(n^2).

## Code

```java
public List<List<Integer>> threeSum(int[] numbers) {
    // Two pointers
    List<List<Integer>> result = new ArrayList<>();
    if (numbers.length == 0 || numbers == null) {
        return result;
    }

    Arrays.sort(numbers);
    for (int i = 0; i < numbers.length - 2; i++) {
        // while (i > 2 && i < numbers.length && numbers[i] == numbers[i - 1]) {
        //     i++;
        // }

        // if (i >= numbers.length) {
        //     break;
        // }

        // It's better to ues continue!
        if (i > 0 && numbers[i] == numbers[i - 1]) {
            continue;
        }

        int c = numbers[i];
        // int left = 0, right = i - 1; this is wrong! We should find sum after target, because it will contain all the possible values, we cannot find sumb before target, it's not complete. In [-2,-3,-4,-5,-100,99,1,4,4,4,5,1,0,-1,2,3,4,5], [-2,1,1] could be missing.
        twoSum(i + 1, numbers.length - 1, numbers, c, result);
    }

    return result;
}

private void twoSum(int left, int right, int[] numbers, int c, List<List<Integer>> result) {
    while (left < right) {
        int a = numbers[left];
        int b = numbers[right];
        if (a + b == -c) {
            List<Integer> tempList = new ArrayList<>();
            tempList.add(c);
            tempList.add(a);
            tempList.add(b);
            result.add(tempList);
            // To avoid duplicates, like -1 + -2 = -3, a = -2, b = -1, and the next
            // number after a is still -2, so we must move two pointers simultaneously.
            // This is exactly the same with two sum unique pairs.
            left++;
            right--;
            while (left < right && numbers[left] == numbers[left - 1]) {
                left++;
            }

            while (left < right && numbers[right] == numbers[right + 1]) {
                right--;
            }

        } else if (a + b < -c) {
            left++;
        } else {
            right--;
        }
    }
}

// Too complicated!!! Is there any simpler solution?
private void twoSumHashMap(int left, int right, int[] numbers, int a, List<List<Integer>> result) {
    // -2,1,1 edge case
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = left; i <= right; i++) {
        int c = numbers[i];
        int b = -a - c;
        if (map.containsKey(c)) {
            if (map.get(c) >= 1 && b != c) {
                continue;
            }

            if (b == c && map.get(c) >= 2) {
                continue;
            }
        }

        if (map.containsKey(b)) {
            List<Integer> tempList = new ArrayList<>();
            tempList.add(a);
            tempList.add(b);
            tempList.add(c);
            result.add(tempList);
        }

        if (map.containsKey(c)) {
            map.put(c, map.get(c) + 1);
        } else {
            map.put(c, 1);
        }
    }
}
```