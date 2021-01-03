```
Count the number of prime numbers less than a non-negative number, n.

Example 1:
Input: n = 10
Output: 4
Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.

Example 2:
Input: n = 0
Output: 0

Example 3:
Input: n = 1
Output: 0
```
```go
// go: hash
func countPrimes(n int) int {
    if n <= 2 {
        return 0
    }
    m := map[int]bool{}
    res := 0
    for i; i < n; i++{
        if _, ok := m[i]; !ok{
            res++
            for j := 2; i * j < n; j++{
                m[i*j] = true
            }
        }
    }
    
    return res
}
```
