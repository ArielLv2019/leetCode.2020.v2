```
Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Follow up: If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

 

Example 1:

Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
Example 2:

Input: nums = [1]
Output: 1
Example 3:

Input: nums = [0]
Output: 0
Example 4:

Input: nums = [-1]
Output: -1
Example 5:

Input: nums = [-2147483647]
Output: -2147483647
```
```
// test case
[-2,1,-3,4,-1,2,1,-5,4]
[1]
[0]
[-1]
[-2147483647]
```

```go
func maxSubArray(nums []int) int {
    if len(nums) == 0 {
        return 0
    }
    
    sum, res := 0, nums[0]
    for i := 0; i < len(nums); i++ {
        sum += nums[i]
        if sum > res {
            res = sum
        }
        if sum < 0 {
            sum = 0
        }
    }
    
    return res
}
```
