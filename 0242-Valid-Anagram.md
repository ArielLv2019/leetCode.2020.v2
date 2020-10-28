```
Given two strings s and t , write a function to determine if t is an anagram of s.

Example 1:

Input: s = "anagram", t = "nagaram"
Output: true

Example 2:

Input: s = "rat", t = "car"
Output: false

Note:
You may assume the string contains only lowercase alphabets.

Follow up:
What if the inputs contain unicode characters? How would you adapt your solution to such case?
```
```go
func isAnagram(s string, t string) bool {
    if len(s) != len(t){
        return false
    }
    
    m := make([]int, 26)
    for _, ch := range s{
        m[ch - 'a']++
    }
    
    for _, ch := range t{
        m[ch - 'a']--
    }
    
    for _, v := range m{
        if v != 0{
            return false
        }
    }
    return true
}
```
```cpp
// sort + compare
class Solution {
public:
    bool isAnagram(string s, string t) {
        std::sort(s.begin(), s.end());
        std::sort(t.begin(), t.end());
        return s.compare(t) == 0;
    }
};
```
```go
func isAnagram(s string, t string) bool {
    if len(s) != len(t){
        return false
    }
    
    m := map[rune]int{}
    for _, ch := range s{
        m[ch]++
    }
    
    for _, ch := range t{
        if _, ok := m[ch]; !ok{
            return false
        }
        m[ch]--
        if m[ch] == 0{
            delete(m, ch)
        }
    }
    
    return len(m) == 0
}
```
