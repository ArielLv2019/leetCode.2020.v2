```
Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).

Note:
Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.
```

```cpp
// 一维数组
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        vector<int> mini = triangle[triangle.size() - 1];
        for(int i = triangle.size() - 2; i >= 0; i--){
            for(int j = 0; j < triangle[i].size(); j++){
                mini[j] = min(mini[j], mini[j+1]) + triangle[i][j];
            }
        }
        
        return mini[0];
    }
};
```

```cpp
// dp用二维数组
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        vector<vector<int>> mini(triangle.size(), vector<int>(triangle[triangle.size()-1].size()));
        mini[triangle.size() - 1] = triangle[triangle.size() - 1];
        for(int i = triangle.size() - 2; i >= 0; i--){
            for(int j = 0; j < triangle[i].size(); j++){
                mini[i][j] = min(mini[i+1][j], mini[i+1][j+1]) + triangle[i][j];
            }
        }
        
        return mini[0][0];
    }
};
```
```go
// Go： dp + 一维数组
func minimumTotal(triangle [][]int) int {
    if len(triangle) == 0 || len(triangle[0]) == 0{
        return 0;
    }
    
    dp := triangle[len(triangle) - 1]
    for i := len(triangle) - 2; i >= 0; i--{
        for j := 0; j < len(triangle[i]); j++{
            dp[j] = triangle[i][j] + min(dp[j], dp[j+1])
        }
    }              
    return dp[0]
}

func min( a, b int) int{
    if a < b {
        return a
    }
    
    return b
}
```
