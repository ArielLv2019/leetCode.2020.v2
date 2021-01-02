```
You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.

 

Example 1:

Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
Explanation: 
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7

Example 2:
Input: nums = [1], k = 1
Output: [1]

Example 3:
Input: nums = [1,-1], k = 1
Output: [1,-1]

Example 4:
Input: nums = [9,11], k = 2
Output: [11]

Example 5:
Input: nums = [4,-2], k = 2
Output: [4]

Constraints:
    1 <= nums.length <= 105
    -104 <= nums[i] <= 104
    1 <= k <= nums.length

Test Case:
[1,3,-1,-3,5,3,6,7]
3
[1]
1
[1,-1]
1
[9, 11]
2
[1,3,1,2,0,5]
3

```
```go
// go + sliding window
func maxSlidingWindow(nums []int, k int) []int {
    if len(nums) < k{
        return nil
    }
    res := []int{}
    window := []int{}
    for i := 0; i < len(nums); i++{
        if i >= k && len(window) > 0 && window[0] <= i - k{
            window = window[1:]
        }
        
        for len(window) > 0 && nums[window[len(window)-1]] < nums[i]{
            window = window[0:len(window)-1]
        }
        
        window = append(window, i)
        
        if i >= k-1 {
            res = append(res, nums[window[0]])
        } 
        
    }
    return res
}
```
```cpp
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        if(nums.size() < k) {
            return std::vector<int>{};
        }
        std::deque<int> window;
        std::vector<int> res; 
        for( int i = 0; i < nums.size(); i++){
            if(i >= k && !window.empty() && window[0] <= i - k){
                window.pop_front();
            }
            
            while(!window.empty() && nums[window.back()] < nums[i]){
                window.pop_back();
            }
            
            window.emplace_back(i); // Note: 保存的是下标
            
            if (i >= k-1){
                res.emplace_back(nums[window[0]]);
            }
        }
        return res;
    }
};
```
