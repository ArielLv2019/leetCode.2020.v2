```
Given a positive integer num, write a function which returns True if num is a perfect square else False.

Follow up: Do not use any built-in library function such as sqrt.

Example 1:
Input: num = 16
Output: true

Example 2:
Input: num = 14
Output: false
```

```go
// 二分查找
func isPerfectSquare(num int) bool {
    l, r := 1 , num
    for l <= r {
        mid := l + (r - l) / 2 
        if mid * mid == num {
            return true
        }
        if mid < num / mid {
            l = mid + 1
        }else{
            r = mid - 1
        }
    }
    
    return false
}
```
```go
//牛顿逼近法
func isPerfectSquare(num int) bool {
    ans := num
    for ans * ans > num{
        ans = (ans + num / ans) / 2
    }
        
    return ans*ans == num
}
```
```cpp
// 二分查找：注意各种溢出
class Solution {
public:
    bool isPerfectSquare(int num) {
        double l = 1, r = num;
        while( l <= r){
            int mid = l + (r-l) / 2;
            double tmp = double(mid)*mid;
            if(tmp == double(num)){
                return true;
            }
            if(tmp < double(num)){
                l = mid + 1;
            }else{
                r = mid - 1;
            }
        }
        
        return false;
    }
};
```
