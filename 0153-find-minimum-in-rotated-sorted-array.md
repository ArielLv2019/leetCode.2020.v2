```
Suppose an array of length n sorted in ascending order is rotated between 1 and n times. For example, the array nums = [0,1,2,4,5,6,7] might become:

[4,5,6,7,0,1,2] if it was rotated 4 times.
[0,1,2,4,5,6,7] if it was rotated 7 times.
Notice that rotating an array [a[0], a[1], a[2], ..., a[n-1]] 1 time results in the array [a[n-1], a[0], a[1], a[2], ..., a[n-2]].

Given the sorted rotated array nums, return the minimum element of this array.

 

Example 1:

Input: nums = [3,4,5,1,2]
Output: 1
Explanation: The original array was [1,2,3,4,5] rotated 3 times.
Example 2:

Input: nums = [4,5,6,7,0,1,2]
Output: 0
Explanation: The original array was [0,1,2,4,5,6,7] and it was rotated 4 times.
Example 3:

Input: nums = [11,13,15,17]
Output: 11
Explanation: The original array was [11,13,15,17] and it was rotated 4 times.
```
```
Classic binary search problem.

Looking at subarray with index [start,end]. We can find out that if the first member is less than the last member, 
there's no rotation in the array. So we could directly return the first element in this subarray.

If the first element is larger than the last one, then we compute the element in the middle, and compare it with the first element. 
If value of the element in the middle is larger than the first element, we know the rotation is at the second half of this array. 
Else, it is in the first half in the array.
```
```go
func findMin(nums []int) int {
    left, right := 0,len(nums)-1
    for left < right { // 判断条件
        if nums[left] < nums[right]{
            return nums[left]
        }
        mid := left + (right - left) / 2
        if nums[left] <= nums[mid]{
            left = mid + 1
        }else{
            right = mid //递增条件
        }
    }
    
    return nums[left]
}
```
