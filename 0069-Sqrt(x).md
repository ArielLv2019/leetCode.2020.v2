```
Implement int sqrt(int x).

Compute and return the square root of x, where x is guaranteed to be a non-negative integer.

Since the return type is an integer, the decimal digits are truncated and only the integer part of the result is returned.

Example 1:
Input: 4
Output: 2

Example 2:
Input: 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since 
             the decimal part is truncated, 2 is returned.
```
```cpp
//二分法
class Solution {
public:
    int mySqrt(int x) {
        if(x == 0 || x == 1){
            return x;
        }
        int l = 1, r = x, res;
        while(l <= r){
            int mid = l + (r - l)/2; //防止溢出
            if ( mid == x / mid ){
                return mid;
            }
            if(mid < x / mid){
                l = mid + 1;
                res = mid;
            }else{
                r = mid - 1;
            }   
        }
        return res;
    }
};
```

```cpp
// 牛顿迭代法
class Solution {
public:
    int mySqrt(int x) {
        if(x == 0 || x == 1){
            return x;
        }
        
        double ans = x;
        double delta = 0.0001;
        while( fabs(ans*ans - x) > delta){
            ans = (ans + x / ans) /2;
        }
        return ans;
    }
};
```

