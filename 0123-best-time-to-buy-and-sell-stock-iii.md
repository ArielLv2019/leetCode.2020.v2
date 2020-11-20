```
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

Example 1:
Input: prices = [3,3,5,0,0,3,1,4]
Output: 6
Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.

Example 2:
Input: prices = [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are engaging multiple transactions at the same time. You must sell before buying again.

Example 3:
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.

Example 4:
Input: prices = [1]
Output: 0
 

Constraints:
1 <= prices.length <= 105
0 <= prices[i] <= 105

https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/discuss/135704/Detail-explanation-of-DP-solution
```

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if(prices.size() <= 0){
            return 0;
        }
        int result = 0;
        int K = 3;
        vector<vector<int>> dp(K, vector<int>(prices.size()));
        for(int k = 1; k < K; k++){
            int tmpMax = dp[k-1][0] - prices[0];
            for(int i = 1; i < prices.size(); ++i){
                dp[k][i] = max(dp[k][i-1], prices[i] + tmpMax);
                tmpMax = max(tmpMax, dp[k-1][i] - prices[i]);
            }        
        }
        
        return dp[2][prices.size() - 1];
    }
};
```
```cpp
// If we slight swap the two 'for' loops:
// We need to save max for each transaction, so there are k 'max'.
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if(prices.size() <= 0){
            return 0;
        }
       
        int K = 3;
        vector<vector<int>> dp(K, vector<int>(prices.size()));
        vector<int> tmpMax(K, -prices[0]);// tmp[k]: 第k次的最大值
        for(int i = 1; i < prices.size(); ++i){
            for(int k = 1; k < K; k++){
                dp[k][i] = max(dp[k][i-1], prices[i] + tmpMax[k]); 
                tmpMax[k] = max(tmpMax[k], dp[k-1][i] - prices[i]); 
            }        
        }
        
        return dp[2][prices.size() - 1];
    }
};
```
```cpp
// We can find the second dimension (variable i) is only dependent on the previous one (i-1), so we can compact this dimension.
// (We can choose the first dimension (variable k) as well since it is also only dependent on its previous one k-1, but can't compact both.)
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if(prices.size() <= 0){
            return 0;
        }
       
        int K = 3;
        vector<int> dp(K);
        vector<int> tmpMax(K, -prices[0]);
        for(int i = 1; i < prices.size(); ++i){
            for(int k = 1; k < K; k++){
                dp[k] = max(dp[k], prices[i] + tmpMax[k]); 
                tmpMax[k] = max(tmpMax[k], dp[k-1] - prices[i]); 
            }        
        }
        
        return dp[2];
    }
};
```
```cpp
//In this case, K is 2. We can expand the array to all named variables:
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if(prices.size() <= 0){
            return 0;
        }
       
        int sell1 = 0, sell2 = 0;
        int buy1 = -prices[0], buy2 = -prices[0];
        for(int i = 1; i < prices.size(); ++i){
            sell2 = max(sell2, prices[i] + buy2); // The maximum if we've just sold 2nd stock so far.
            buy2 = max(buy2, sell1-prices[i]); // The maximum if we've just buy  2nd stock so far.
            sell1 = max(sell1, prices[i] + buy1); // The maximum if we've just sold 1nd stock so far.
            buy1 = max(buy1, -prices[i]);  // The maximum if we've just buy  1st stock so far.                  
        }
        
        return sell2;
    }
};

```
