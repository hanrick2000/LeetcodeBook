#### Question
You have an array for which the ith element is the price of a given stock on day i. If you were only permitted to complete at most one transaction (buy one and sell one), help find the maximum profit. 

#### Examples
Given [1,2,5,4,3], return 4. (which is 5 - 1)  

Given [5,3,4,1,2], return 1. (which is 4 - 3 or 2 - 1)

Given [5,3,4,2,7], return 4. (which is 7 - 2)

Given [], return 0. 

Given [1], return 0.

#### Solution
I've seen this question before, and I know we may need to use dp or greedy. But still I will use my own method to tear the question apart, and write code step by step. Actually this question is the first question that I wrote with not a 
single bug. Imagine you are a customer, you don't know what exactly the stock price is behind current day, what will you do to get maximum profit?

#### Analysis
Time: O(n)  
Space: O(1)

#### Code

```java
public int maxProfit(int[] prices) {
    if (prices.length == 0) {
        return 0;
    }
    // Find which variables to reprent which situation
    int profit = 0; // current maximum profit
    int prevMin = prices[0]; // previous minimum price
    // Now we need to know if we need to initialize these variables
    // So for the first day, which is i = 0, prevMin should be 0,
    // profit should be 0. But there seems no prevMin for first day.
    // So we need to traverse from the second day. 
    for (int i = 1; i < prices.length; i++) {
        // There are two conditions for second day, it can be bigger
        // than prevMin, or it can be smaller
        if (prices[i] < prevMin) {
            prevMin = prices[i];
        } else {
            profit = Math.max(prices[i] - prevMin, profit);
        }
    }
    // How to check if the solution is right or not. 
    // Just run several test cases.
    return profit;
}
```