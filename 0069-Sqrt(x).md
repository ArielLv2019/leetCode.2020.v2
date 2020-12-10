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
        if( x == 0 || x == 1){
            return x;
        } 
        int l = 1, r = x;
        int res = 0;
        while( l <= r ){
            int mid = l + ( ( r - l ) >> 2 ); // 右移操作必须加括号
            int ans = x / mid; //必须得用商，2147395599会溢出
            if ( mid == ans ){
                return mid;
            }else if( mid > ans ){
                r = mid - 1;
            }else{
                l = mid + 1;
                res = mid;
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
        if( x == 0 || x == 1){
            return x;
        } 
        long r = x;
        while( r * r > x){
            r = (r + x/r)/2;
        }
        
        return r;
    }
};
```

