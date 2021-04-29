```
Given two strings text1 and text2, return the length of their longest common subsequence. If there is no common subsequence, return 0.

A subsequence of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

For example, "ace" is a subsequence of "abcde".
A common subsequence of two strings is a subsequence that is common to both strings.

 

Example 1:

Input: text1 = "abcde", text2 = "ace" 
Output: 3  
Explanation: The longest common subsequence is "ace" and its length is 3.
Example 2:

Input: text1 = "abc", text2 = "abc"
Output: 3
Explanation: The longest common subsequence is "abc" and its length is 3.
Example 3:

Input: text1 = "abc", text2 = "def"
Output: 0
Explanation: There is no such common subsequence, so the result is 0.
```
```cpp
// cpp
// DP
// dp[i][j] = (text1[i-1] == text2[j-1]) ? dp[i-1][j-1]+1:max(dp[i-1][j], dp[i][j-1]);
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        if(text1.size() == 0 || text2.size() == 0){
            return 0;
        }
        
        vector<vector<int>> dp(text1.size()+1, vector<int>(text2.size()+1, 0));
        for(int i = 1; i < text1.size() + 1; i++){
            for(int j = 1; j < text2.size() + 1; j++){
                dp[i][j] = (text1[i-1] == text2[j-1]) ? dp[i-1][j-1]+1:max(dp[i-1][j], dp[i][j-1]);
            }
        }
        return dp[text1.size()][text2.size()];
    }
};
```
```cpp
// 要求返回最终的字符串
```
