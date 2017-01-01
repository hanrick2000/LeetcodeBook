#### Question
You have an array for which the ith element is the price of a given stock on day i. Find the maximum profit, under the condition that you may complete as many transactions as you like, but you must sell the stock before buying again, and you cannot buy stock on next day after you sell it. 

#### Examples
Given [1,2,3,4,5], return 2. (which is 2-1 + 5-4) 

Given [1,2,3,10,5], return 9. (which is 10-1)

Given [1,2,5,1,2], return 4. (which is 5-1 since 5-1 is greater than 2-1 + 2-1) 

Given [1,4,1,1,4], return 6. (which is 4-1 + 4-1)

Given [6,1,3,2,4,7], return 6. (which is 7-1 since it's greater than 3-1 + 7-4) This case has gone beyond i =1,2,3, which I don't know how to handle with. I thought about adding a min variable to keep track of the minimum price of all time. So maybe this case is the key to this problem which implies we cannot just use dp[1], dp[2], dp[3] three conditons to cover all conditions. 

#### Solution
The constraint that you cannot buy stock on next day after you sell it cuts the array from consecutive to discrete. There are too many possibilities. The key to dp problems is to find the variables to represent every possible state. There are three states here: rest, buy, sell.

#### Analysis


#### Code

```java
public int maxProfit(int[] prices) {
    // 尝试了使用一个dp[]数组来存储maximum profit till current day, 发现还是不行. 
    // 主要是超过了i-3就没法记录了. 
    if (prices.length < 2) {
        return 0;
    } else if (prices.length == 2) {
        return Math.max(prices[1] - prices[0], 0);
    }
    int[] dp = new int[prices.length]; // dp[i] represents maximum profit till day i
    dp[0] = 0;
    dp[1] = Math.max(prices[1] - prices[0], 0);
    // Three conditions for dp[2]
    dp[2] = Math.max(Math.max(prices[2] - prices[1], dp[1]), prices[2] - prices[0]);
    for (int i = 3; i < prices.length; i++) {
        // There are three conditions
        int p1 = Math.max(dp[i - 1], prices[i] - prices[i - 1]);
        int p2 = Math.max(dp[i - 2], prices[i] - prices[i - 2]);
        int p3 = Math.max(dp[i - 3] + Math.max(prices[i] - prices[i - 1], 0));
        dp[i] = Math.max(Math.max(p1, p2), p3);
    }
    return dp[dp.length - 1];
}
```

```java
// 根本不会啊, 这题也太难了把. 这种dp还真不如考我字符串dp...
// 把sequence tree里最后只有buy的枝全部砍掉. 因为单从自己举的test case来看, 
// 肯定不会让最后一个操作是buy的, 最后一个操作buy那肯定还不如不buy. 所以最后
// 一个操作一定是sell或者cooldown. 
// 这道题真他妈是终极难, 让人觉得似乎有头绪, 但是就是做不出来. 
public int maxProfit(int[] prices) {
    // 大概懂了, dp的题最重要的是在于定义state, 而这个state本身的定义是代表结果的状态. 而不是
    // action, 这道题来说, action也可以理解为choice, 一共有三种, buy/sell/rest. 而最后的state
    // 可以理解为手里有股票和没股票. 所以就两个数组, 一个代表手里有, 一个代表手里没有. 
    int[] sell = new int[prices.length];
    int[] buy = new int[prices.length];
    sell[0] = 0;
    buy[0] = -prices[0];
    for (int i = 1; i < prices.length; i++) {
        sell[i] = Math.max(sell[i - 1], buy[i - 1] + prices[i]);
        buy[i] = Math.max(buy[i - 1], (i > 1 ? sell[i - 2] : 0) - prices[i]);
    }
    return sell[prices.length - 1];
}
```





