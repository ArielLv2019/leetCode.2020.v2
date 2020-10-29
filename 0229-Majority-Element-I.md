```
Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times.

Follow-up: Could you solve the problem in linear time and in O(1) space?

 

Example 1:

Input: nums = [3,2,3]
Output: [3]

Example 2:

Input: nums = [1]
Output: [1]

Example 3:

Input: nums = [1,2]
Output: [1,2]
```
```go
// map + count
func majorityElement(nums []int) []int {
    m := map[int]int{}
    for _, v := range nums{
        m[v]++
    }
    
    res := []int{}
    for k, v := range m{
        if v > len(nums)/3{
            res = append(res, k)
        }
    }
    return res
}
```
```go
func majorityElement(nums []int) []int {
    var(
        n1, n2 int
        c1, c2 = 0, 0
    )
    for _, v := range nums{
        if v != n2 && c1 == 0{
            n1 = v
            c1++
            continue
        }
        if v != n1 && c2 == 0{ //[2,2]
            n2 = v
            c2++
            continue
        }
        
        if n1 == v{
            c1++
            continue
        }
        
        if n2 == v{
            c2++
            continue
        }
        
        c1--
        c2--
    }
    
    result := []int{}
    if c1 > 0 && count(nums, n1) > len(nums)/3{
        result = append(result, n1)
    }
    if c2 > 0 && count(nums, n2) > len(nums)/3{ // [0, 0, 0]
        result = append(result, n2)
    }
    return result
}

func count(nums []int, target int) int{
    res := 0
    for _, v := range nums{
        if target == v{
           res++ 
        }
    }
    
    return res
}
```
