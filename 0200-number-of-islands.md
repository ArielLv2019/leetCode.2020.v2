```
Given an m x n 2d grid map of '1's (land) and '0's (water), return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.
 

Example 1:
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1

Example 2:
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
 
Constraints:
m == grid.length
n == grid[i].length
1 <= m, n <= 300
grid[i][j] is '0' or '1'.
```
```cpp
// 染色法 + DFS
class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        vector<vector<bool>> visited(grid.size(), vector<bool>(grid[0].size()));
        int result = 0;
        for( int i = 0; i < grid.size(); i++){
            for(int j = 0; j < grid[0].size(); j++){
                if(grid[i][j] == '1' && visited[i][j] == false){
                    result++;
                    dfs(grid, visited, i, j);
                }
            }
        }
        return result;      
    }
private:
    void dfs(vector<vector<char>>& grid, vector<vector<bool>>& visited, int i, int j){
        if( !isValid(grid, visited, i, j) ){
            return ;
        }
        visited[i][j] = true;
        vector<vector<int>> dirt{{0, 1},{0, -1},{1, 0},{-1,0}};
        for(int k = 0; k < 4; k++){
            dfs(grid, visited, i+dirt[k][0], j+dirt[k][1]);
        }
    }
    
    bool isValid(vector<vector<char>>& grid, vector<vector<bool>>& visited, int i, int j){
        if( i < 0 || i >= grid.size() || j < 0 || j >= grid[0].size()){
            return false;
        }
        if(grid[i][j] == '0' || visited[i][j]){
            return false;
        }
        
        return true;
    }
};
```
