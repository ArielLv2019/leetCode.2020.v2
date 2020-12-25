```
Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

Example 1:
Input: [3,2,1,5,6,4] and k = 2
Output: 5

Example 2:
Input: [3,2,3,1,2,4,5,5,6] and k = 4
Output: 4

Note:
You may assume k is always valid, 1 ≤ k ≤ array's length.
```
```
// cpp: priority_queue
kth-largest-element-in-an-array
```

```
// go: partation sort
// 大->小排序
func findKthLargest(nums []int, k int) int {
    n := len(nums) - 1
    idx := partation(nums, 0, n)
    for idx != k-1{
        if(idx < k-1){
            idx = partation(nums, idx + 1, n)
        }else if(idx > k-1){
            idx = partation(nums, 0, idx - 1)
        }
    }
    
    return nums[idx]
}

func partation(nums []int, left, right int) int{
    pivot := nums[left]
    for left < right{
        for left < right && nums[right] <= pivot{
            right--
        }
        nums[left] = nums[right]
        
        for left < right && nums[left] >= pivot{
            left++
        }
        nums[right] = nums[left]
    }
    
    nums[left] = pivot
    return left
}
```
