```
Given a string s, return the longest palindromic substring in s.

 

Example 1:

Input: s = "babad"
Output: "bab"
Note: "aba" is also a valid answer.
Example 2:

Input: s = "cbbd"
Output: "bb"
Example 3:

Input: s = "a"
Output: "a"
Example 4:

Input: s = "ac"
Output: "a"
```
```go
// 递归，执行最快
package main

/**
 * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
 * 
 * @param A string字符串 
 * @param n int整型 
 * @return int整型
*/
func getLongestPalindrome( A string ,  n int ) int {
    // write code here
    if len(A) < 2 {
        return len(A)
    }
    res := 1
    for i := 0; i < len(A) - 1; i++{
        generatePalindrome(A, i, i, &res)
        generatePalindrome(A, i, i+1, &res)
    }
    
    return res
}
func generatePalindrome(A string, i, j int, res *int){
    for i >= 0 && j < len(A) && A[i]==A[j]{
        i--
        j++
    }
    if j - i - 1 > *res{
        *res = j - i - 1
    }
}
```
```cpp
// 递归
class Solution {
public:
    string longestPalindrome(string s) {
        if(s.size() < 2){
            return s;
        }
        
        for(int i = 0; i < s.size() - 1; i++){
            extendPalindrome(s,i,i);
            extendPalindrome(s,i, i + 1);
        }
        
        return s.substr(start, maxLen);
    }
    
    void extendPalindrome(string s, int i, int j){
        while(i >= 0 && j < s.size() && s[i] == s[j]){
            i--;
            j++;
        }
       
        if(j-i-1> maxLen){
            start = i+1;  //Note: the begin need to +1;
            maxLen = j-i-1;
        }
    }
private:
    int start = 0;
    int maxLen = 1;
};
```
```cpp
class Solution {
public:
    int getLongestPalindrome(string A, int n) {
        // write code here
        int res = 0;
        for(int i = 0; i < n; i++){
            for(int j = i+1; j < n; j++){
                if(isPal(A, i, j) ){
                    res = std::max(j-i+1, res);
                }
            }
        }
        return res;
    }
    
    bool isPal(string A, int i, int j){
        for(; i <= j; i++, j--){
            if(A[i] != A[j]){
                return false;
            }
        }
        
        return true;
    }
};
```
