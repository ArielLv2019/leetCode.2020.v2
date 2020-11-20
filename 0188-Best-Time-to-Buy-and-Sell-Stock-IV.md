```
You are given an integer array prices where prices[i] is the price of a given stock on the ith day.

Design an algorithm to find the maximum profit. You may complete at most k transactions.

Notice that you may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

 
Example 1:
Input: k = 2, prices = [2,4,1]
Output: 2
Explanation: Buy on day 1 (price = 2) and sell on day 2 (price = 4), profit = 4-2 = 2.

Example 2:
Input: k = 2, prices = [3,2,6,5,0,3]
Output: 7
Explanation: Buy on day 2 (price = 2) and sell on day 3 (price = 6), profit = 6-2 = 4. Then buy on day 5 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
 

Constraints:
0 <= k <= 109
0 <= prices.length <= 1000
0 <= prices[i] <= 1000```
```
```cpp
// dp[i][k][j]: i[0~prices.size()), k[0~k+1], j[0,1]
// dp[i][k][j]: 到第i个元素，交易k次的最大收益； j=0: 未持有股票； j=1:持有股票
// dp[0][k][0] = 0;
// dp[0][k][1] = -prices[0]
// result = max{dp[n-1, 0...k, 0]}

class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        if(prices.size() <= 1){
            return 0;
        }
        if ( k > prices.size()){
            return greedy(prices);
        }
        int result = 0;
        vector<vector<vector<int>>> dp(prices.size(), vector<vector<int>>(k+1, vector<int>(2)));
        
        for(int kIdx = 0; kIdx <= k; kIdx++){
            dp[0][kIdx][0] = 0;
            dp[0][kIdx][1] = -prices[0];
        }
        
        for(int i = 1; i < prices.size(); ++i){
            for(int kIdx = 0; kIdx <= k; ++kIdx){
                dp[i][kIdx][0] = max(dp[i-1][kIdx][0], (kIdx != 0) ? dp[i-1][kIdx-1][1]+prices[i] : INT_MIN);
                dp[i][kIdx][1] = max(dp[i-1][kIdx][1], dp[i-1][kIdx][0]-prices[i]);
                result = max(dp[i][kIdx][0], result);
            }
        }
        return result;
    }
private: 
    int greedy(vector<int>& prices){
        int result = 0;
        for(int i = 0; i < prices.size() - 1; ++i){
            if(prices[i+1] > prices[i]){
                result += prices[i+1] - prices[i];
            }
        }
        return result;
    }
};
```
```cpp
// dp[i][j]: i[0~k+1], j[0~prices.size())
// dp[i][j]: 元素j交易i次的最大利益
// dp[0][j] = 0: 交易0次的收益都为0
// dp[i][0] = 0: prices只有一个元素的时候获得的交易也是0
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        if(prices.size() <= 1){
            return 0;
        }
        if ( k > prices.size()){
            return greedy(prices);
        }
        
        int result = 0;
        vector<vector<int>> dp(k+1, vector<int>(prices.size()));      
        for(int i = 1; i <= k; i++){
            for(int j = 1; j < prices.size(); j++){
                dp[i][j] = dp[i][j-1];
                for(int m = 0; m < j; m++){
                   dp[i][j] = max(dp[i][j], prices[j] - prices[m] + dp[i-1][m] );     
                }
            }           
        }
        return dp[k][prices.size()-1];
    }
private: 
    int greedy(vector<int>& prices){
        int result = 0;
        for(int i = 0; i < prices.size() - 1; ++i){
            if(prices[i+1] > prices[i]){
                result += prices[i+1] - prices[i];
            }
        }
        return result;
    }
};
```
```cpp
// 优化
```cpp上一版的实现
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        if(prices.size() <= 1){
            return 0;
        }
        if ( k > prices.size()){
            return greedy(prices);
        }
        
        int result = 0;
        vector<vector<int>> dp(k+1, vector<int>(prices.size()));      
        for(int i = 1; i <= k; i++){
            int tmpMax = dp[i-1][0] - prices[0];
            for(int j = 1; j < prices.size(); j++){
                dp[i][j] = max(dp[i][j-1], prices[j] + tmpMax);     
                tmpMax = max(tmpMax, dp[i-1][j] - prices[j]);
            }           
        }
        return dp[k][prices.size()-1];
    }
private: 
    int greedy(vector<int>& prices){
        int result = 0;
        for(int i = 0; i < prices.size() - 1; ++i){
            if(prices[i+1] > prices[i]){
                result += prices[i+1] - prices[i];
            }
        }
        return result;
    }
};
```
