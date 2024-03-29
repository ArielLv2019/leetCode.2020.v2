```
Given a string s, find the length of the longest substring without repeating characters.

Example 1:
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.

Example 2:
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.

Example 3:
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

Example 4:
Input: s = ""
Output: 0

"abcabcbb"
"bbbbb"
"pwwkew"
"ab"
" "
"abba"
3
1
3
2
1
2
```
```go
// go: 
func lengthOfLongestSubstring(s string) int {
    m := map[byte]int{}
    start, res := -1, 0
    for i := 0; i < len(s); i++{        
        if preIdx, ok := m[s[i]]; ok && preIdx > start{
            start = preIdx
        }
        if curLen := i - start; curLen > res{
            res = curLen
        }
        m[s[i]] = i
    }
    return res
}
```
