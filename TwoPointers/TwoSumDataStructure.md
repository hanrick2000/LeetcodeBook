# [TwoSumDataStructure](http://lintcode.com/en/problem/two-sum-data-structure-design/)

## Question

Design and implement a TwoSum class. It should support the following operations: add and find.

add - Add the number to an internal data structure.

find - Find if there exists any pair of numbers which sum is equal to the value.

## Examples

```java
add(1); add(3); add(5);
find(4) // return true
find(7) // return false
```

## Analysis

This question is more complex than I thought, previously I was thinking about using HashSet should be enough. But we need to consider about the edge case that the sum is 6, and if there are two 3 added, it should return true, but if there is only one 3 added, if should return false. So we have to use HashMap to record the times that number appeared.

## Code

```java
public class TwoSum {
    private List<Integer> list = new ArrayList<>();
    private Map<Integer, Integer> map = new HashMap<>();
    // Add the number to an internal data structure.
    public void add(int number) {
        if (map.containsKey(number)) {
            map.put(number, map.get(number) + 1);
        } else {
            map.put(number, 1);
            list.add(number);
        }
    }

    // Find if there exists any pair of numbers which sum is equal to the value.
    public boolean find(int value) {
        for (int i = 0; i < list.size(); i++) {
            int target = value - list.get(i);
            if (target == list.get(i) && map.get(target) > 1) {
                return true;
            }

            if (target != list.get(i) && map.containsKey(target)) {
                return true;
            }
        }

        return false;
    }
}
```