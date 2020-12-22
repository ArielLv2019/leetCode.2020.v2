Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

Example 1:
Input: s = "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()".

Example 2:
Input: s = ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()".

Example 3:
Input: s = ""
Output: 0```
```

```cpp
// stack
class Solution {
public:
    int longestValidParentheses(string s) {
        stack<int> sta;
        sta.emplace(-1);
        int res = 0;
        for( int i = 0; i < s.size(); i++ ){
            if(s[i] == '('){
                sta.emplace(i);
            }else{
                sta.pop();
                if(!sta.empty()){
                    res = max(res, i - sta.top());
                }else{
                    sta.emplace(i);
                }
            }
        }
        return res;
    }
};
```
