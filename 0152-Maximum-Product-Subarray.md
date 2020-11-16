```
Given an integer array nums, find the contiguous subarray within an array (containing at least one number) which has the largest product.

Example 1:
Input: [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.

Example 2:
Input: [-2,0,-1]
Output: 0
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.
```
```cpp
// 改良版二维数组
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        if(nums.size() <= 0){
            return 0;
        }
        vector<vector<int>> dp(2, vector<int>(2));
        dp[0][0] = nums[0], dp[0][1] = nums[0];
        int result = nums[0];
        for(int i = 1; i < nums.size(); i++){
            int x = i % 2, y = (i-1) % 2;
            dp[x][0] = max( max(dp[y][0] * nums[i], dp[y][1]*nums[i]), nums[i]);//把nums[i]考虑进去是可能存在[0,2]这种情况
            dp[x][1] = min(min(dp[y][0] * nums[i], dp[y][1]*nums[i]), nums[i]);
            result = max(result, dp[x][0]);
        }
        
        return result;
    }
};
```
```cpp
// 二维数组
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        if(nums.size() <= 0){
            return 0;
        }
        vector<vector<int>> dp(nums.size(), vector<int>(2));
        dp[0][0] = nums[0], dp[0][1] = nums[0];
        int result = nums[0];
        for(int i = 1; i < nums.size(); i++){
            dp[i][0] = max( max(dp[i-1][0] * nums[i], dp[i-1][1]*nums[i]), nums[i]);//把nums[i]考虑进去是可能存在[0,2]这种情况
            dp[i][1] = min(min(dp[i-1][0] * nums[i], dp[i-1][1]*nums[i]), nums[i]);
            result = max(result, dp[i][0]);
        }
        
        return result;
    }
};
```
```cpp
// 变量
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        if(nums.size() <= 0){
            return 0;
        }
        
        int preMax = nums[0], preMin = nums[0];
        int result = nums[0];
        for(int i = 1; i < nums.size(); i++){
            int curMax = preMax * nums[i], curMin = preMin * nums[i];
            preMax = max(max(curMax, curMin), nums[i]);//把nums[i]考虑进去是可能存在[0,2]这种情况
            preMin = min(min(curMax, curMin), nums[i]);
            result = max(result, preMax);
        }
        
        return result;
    }
};
```
