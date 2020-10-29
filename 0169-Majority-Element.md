```
Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.

Example 1:
Input: [3,2,3]
Output: 3

Example 2:
Input: [2,2,1,1,1,2,2]
Output: 2
```
```
method 1: 暴力两遍循环
method 2: map统计计数
method 3: sort
method 4: divide && conquer
```
```go
func majorityElement(nums []int) int {
    count, res := 0, -1
    for i := 0; i < len(nums); i++{
        if count == 0{
            res = nums[i]
            count++
            continue
        }
        if nums[i] == res{
            count++
        }else{
            count--
        }
    }
     
    return res
}
```
```go
// map
func majorityElement(nums []int) int {
    m := map[int]int{}
    for _, num := range nums{
        m[num]++
    }
    
    for k, v := range m{
        if v > len(nums) / 2{
            return k
        }
    }
    
    return -1
}
```

```go
//sort
func majorityElement(nums []int) int {
    sort.Slice(nums, func(i, j int)bool{
        return nums[i] < nums[j]
    })
    
    count, res := 0, nums[len(nums)/2]
    for i := 0 ; i < len(nums); i++{
        if nums[i] == res{
            count++
            if count > len(nums)/2{
                return res
            }
        }else{
            count = 0
        }
    }
     
    return -1
```
