```
Given a string s which represents an expression, evaluate this expression and return its value. 

The integer division should truncate toward zero.


Example 1:
Input: s = "3+2*2"
Output: 7

Example 2:
Input: s = " 3/2 "
Output: 1

Example 3:
Input: s = " 3+5 / 2 "
Output: 5
```

```cpp
// by stack
class Solution {
public:
    int calculate(string s) {
        string sign = "+";
        stack<int> sta;
        int num = 0;
        
        for(int i = 0; i < s.size(); ){
            if(s[i] == ' '){
                i++;
                continue;
            }
            
            if(isdigit(s[i])){
                int start = i;
                while(i < s.size() && isdigit(s[i])){
                    i++;
                }
                num = stoi(s.substr(start, i-start));
            }
            if(sign == "+"){
                sta.emplace(num);
            }else if(sign == "-"){
                sta.emplace(-num);
            }else if(sign == "*"){
                int tmp = sta.top();
                sta.pop();
                sta.emplace(tmp * num);
            }else if(sign == "/"){
                int tmp = sta.top();
                sta.pop();
                sta.emplace(tmp / num);
            }
            
            sign = s[i];
            num = 0;
            i++;
        }
        
        int res = 0;
        while(!sta.empty()){
            res += sta.top();
            sta.pop();
        }
        
        return res;
    }
};
```
