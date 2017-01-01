#### Question
You have an array for which the ith element is the price of a given stock on day i. Find the maximum profit, under the condition that you may complete as many transactions as you want (buy one and sell one), but you must sell your stock before you buy it again.

#### Examples
Given [1,2,3,4,5], return 4. (which should be 2-1 + 3-2 + 4-3 + 5-4) 

Given [5,4,1,3,4,2], return 3. (which should be 3-1 + 4-3)

**Given** [4,5,1,2,3], return 3. (which should be 5-4 + 2-1 + 3-2)

Given [] or [1], return 0.

#### Solution
We can simplify the problem as to find all increasing subarray in a given array, and calculate the totoal profits.
Notice the case [4,5,1,2,3], when the last day is also greater than the previous day, we need to update profit again outside the loop.

#### Analysis
Time: O(n)
Space: O(1)

#### Code

```java
public int maxProfit(int[] prices) {
    if (prices.length == 0) {
        return 0;
    }
    int profit = 0; // current maximum profit
    int min = prices[0]; // minimum price for current increasing subarray
    int max = prices[0]; // maximum price for current increasing subarray
    // For first day, there is no previous day, so just start from second day
    for (int i = 1; i < prices.length; i++) {
        // we need to know if current price is greater than previous price
        if (prices[i] < prices[i - 1]) {
            profit += max - min;
            // Use min and max to record start and end of subarray
            min = prices[i];
            max = prices[i];
        } else {
            max = prices[i];
        }
    }
    profit += max - min; // Update profit once more
    return profit;
}
```

```java
// Simpler version
public int maxProfit(int[] prices) {
    int profit = 0;
    for (int i = 1; i < prices.length; i++) {
        int diff = prices[i] - prices[i - 1];
        if (diff > 0) {
            profit += diff;
        }
    }
    return profit;
}
```


