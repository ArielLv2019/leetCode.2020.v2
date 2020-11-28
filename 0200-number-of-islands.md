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
```cpp
// 染色法 + BFS
class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        vector<vector<bool>> visited(grid.size(), vector<bool>(grid[0].size()));
        int result = 0;
        for( int i = 0; i < grid.size(); i++){
            for(int j = 0; j < grid[0].size(); j++){
                if(grid[i][j] == '1' && visited[i][j] == false){
                    result++;
                    bfs(grid, visited, i, j);
                }
            }
        }
        return result;      
    }
private:
    void bfs(vector<vector<char>>& grid, vector<vector<bool>>& visited, int i, int j){
        if( !isValid(grid, visited, i, j) ){
            return ;
        }
        
        visited[i][j] = true;
        deque<pair<int, int>> q;
        q.emplace_back(make_pair(i,j)); 
        vector<vector<int>> dirt{{0, 1},{0, -1},{1, 0},{-1,0}};
        while ( !q.empty() ) {
            int curX = q.front().first, curY = q.front().second;
            q.pop_front();
            for(int i = 0; i < dirt.size(); i++){
                int newX = curX+dirt[i][0], newY = curY+dirt[i][1];
                if (isValid(grid, visited, newX, newY)){
                    visited[newX][newY] = true;
                    q.emplace_back(make_pair(newX, newY));
                }
            }
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
```
//并查集
class UnionFind{
private:
    vector<int> parent;
    vector<int> rank;
    int count;
    
public:
    UnionFind(vector<vector<char>>& grid):count(0){
        int m = grid.size(), n = grid[0].size();
        parent = vector<int>(m*n, -1);
        rank = vector<int>(m*n, 0);
        for ( int i = 0; i < m; i++ ) {
            for ( int j = 0; j < n; j++ ){
                if ( grid[i][j] == '1' ) {
                    parent[i*n+j] = i*n+j;
                    count++;
                }
            }
        }
    }
    
    int Find(int i){
        if( parent[i] == i) {
            return i;
        }
        return Find(parent[i]);
    }
    
    void unionUF(int x, int y){
        int rootX = Find(x), rootY = Find(y);
        if(rootX != rootY){
            if( rank[rootX] < rank[rootY] ){
                parent[rootY] = rootX;
            }else {
                if ( rank[rootX] > rank[rootY] ){
                    parent[rootX] = rootY;
                }else{
                    parent[rootX] = rootY;
                    rank[rootY]++;
                }
            }
            count--;
        }
    } 
    
    int getCount(){
        return count;
    }
};

class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        if(grid.size() == 0 || grid[0].size() == 0){
            return 0;
        }
        
        UnionFind uf(grid);
        vector<vector<int>> dirt{{0, 1},{0, -1},{1, 0},{-1,0}};
        for( int i = 0; i < grid.size(); i++){
            for(int j = 0; j < grid[0].size(); j++){
                if(grid[i][j] == '1'){
                    for(int k = 0; k < 4; k++){
                        int newX = i + dirt[k][0], newY = j + dirt[k][1];
                        if( newX >= 0 && newX < grid.size() && newY >= 0 && newY < grid[0].size() && grid[newX][newY] == '1'){
                            uf.unionUF(i * grid[0].size() + j, newX * grid[0].size() + newY);
                        }
                    }
                }
            }
        }
        return uf.getCount();    
    }
};

```
