```
Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

Note: For the purpose of this problem, we define empty string as valid palindrome.

Example 1:
Input: "A man, a plan, a canal: Panama"
Output: true

Example 2:
Input: "race a car"
Output: false
```

```cpp
// cpp
class Solution {
public:
    bool isPalindrome(string s) {
        for(int left = 0, right = s.size() - 1; left < right; ++left,--right){
            while( left < right && !std::isalnum(s[left]) ){
                ++left;
            }
            while( left < right && !std::isalnum(s[right]) ){
                --right;
            }
            if(std::tolower(s[left]) != std::tolower(s[right]) ) {
                return false;
            }
                       
        }
        
        return true;
    }
};
```

```go
// go: unicode.IsLetter(), unicode.IsDigit(), strings.ToLower()
func isPalindrome(s string) bool {
    str := strings.ToLower(s)
    for left, right := 0, len(str)-1; left < right;{
        for left < right && !(unicode.IsLetter(rune(str[left])) || unicode.IsDigit(rune(str[left])) ){
            left++
        }
        for left < right && !(unicode.IsLetter(rune(str[right])) || unicode.IsDigit(rune(str[right])) ){
            right--
        }
        if(str[left] != str[right]){
            return false
        }
        
        left++ 
        right--
    }
    
    return true
}
```
```go
//go
// strings.EqualFold
func isPalindrome(s string) bool {
    for left, right := 0, len(s)-1; left < right;{
        for left < right && !isValid(s[left]){
            left++
        }
        for left < right && !isValid(s[right]){
            right--
        }
        
        if !strings.EqualFold(string(s[left]), string(s[right])) {
            return false
        }
        
        left++ 
        right--
    }
    
    return true
}

func isValid(c byte) bool{
    return ( c >= 'a' && c <= 'z') || (c >= 'A' && c <= 'Z') || (c >= '0' && c <= '9')
}

```
