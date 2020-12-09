```
Implement a basic calculator to evaluate a simple expression string.

The expression string may contain open ( and closing parentheses ), the plus + or minus sign -, non-negative integers and empty spaces .

Example 1:
Input: "1 + 1"
Output: 2

Example 2:
Input: " 2-1 + 2 "
Output: 3

Example 3:
Input: "(1+(4+5+2)-3)+(6+8)"
Output: 23
```
```cpp
//cpp
class Solution {
public:
    int calculate(string s) {
        stack<int> sta;
        int sign = 1;
        int ans = 0;
        for(int i = 0; i < s.size(); ){
            if (isdigit(s[i])){
                int start = i;
                while(i < s.size() && isdigit(s[i])) {
                    i++;
                }
                int num = stoi(s.substr(start, i-start));
                ans += sign * num;
                continue;
            }else if(s[i] == '+'){
                sign = 1;
            }else if(s[i] == '-'){
                sign = -1;
            }else if(s[i] == '('){
                sta.emplace(ans);
                sta.emplace(sign);
                ans = 0, sign = 1;
            }else if(s[i] == ')'){
                int tmpSign = sta.top();
                sta.pop();
                ans = tmpSign * ans + sta.top();
                sta.pop();
            }
            i++;
        }
        
        return ans;
    }
};
```
