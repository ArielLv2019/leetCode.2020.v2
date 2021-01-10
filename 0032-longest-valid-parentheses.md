```
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
// cpp + stack + dp
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

```go
// go + slice + dp
func longestValidParentheses( s string ) int {
    // write code here
    sta := []int{-1}
    res := 0
    for i, ch := range s{
        switch ch{
            case '(':
                sta = append(sta, i)
            case ')':
                sta = sta[:len(sta)-1]
            if len(sta) > 0 {
                if val := i - sta[len(sta)-1]; val > res{
                    res = val
                }
            }else{
                sta = append(sta, i)
            }
        }
    }
    return res
}
```
