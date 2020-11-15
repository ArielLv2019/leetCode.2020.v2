```
Given an m x n board of characters and a list of strings words, return all words on the board.

Each word must be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. 
The same letter cell may not be used more than once in a word.


Example 1:
Input: board = [["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]], words = ["oath","pea","eat","rain"]
Output: ["eat","oath"]
Example 2:


Input: board = [["a","b"],["c","d"]], words = ["abcb"]
Output: []
 
Constraints:
m == board.length
n == board[i].length
1 <= m, n <= 12
board[i][j] is a lowercase English letter.
1 <= words.length <= 3 * 104
1 <= words[i].length <= 10
words[i] consists of lowercase English letters.
All the strings of words are unique.
```
```cpp
// DFS: 速度最快
class Solution {
public:
    vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
        if(words.size() <= 0 || board.size() <= 0 || board[0].size() <= 0){
            return {};
        }
        
        set<string> s;
        for(auto word : words){
            for(int i = 0; i < board.size(); i++){
                for(int j = 0; j < board[0].size(); j++){
                    if( dfs(board, word, 0, i, j)){
                        s.emplace(word);
                    }
                }
            }
        }
        
        vector<string> res;
        for(auto str : s){
            res.emplace_back(str);
        }
        return res;
    }
    
private:
    bool dfs(vector<vector<char>>& board, string& word, int idx, int i, int j){
        if(i < 0 || i >= board.size() || j < 0 || j >= board[0].size() || idx >= word.size() || board[i][j] ==  ' ' || board[i][j] != word[idx]){
            return false;
        }       
    
        if(idx == word.size() -1){
            return true;
        }
            
        board[i][j] = ' ';
        vector<vector<int>> dirt{{0, 1}, {0, -1}, {1, 0},{-1, 0}};
        for(int k = 0; k < dirt.size(); k++){ //用循环会使速度变慢
            if(dfs(board, word, idx+1, i+dirt[k][0], j+dirt[k][1])){
                board[i][j] = word[idx];
                return true;
            }
        }
        // if( dfs(board, word, idx+1, i+1, j) ) {
        //     board[i][j] = word[idx];
        //     return true;
        // }
        // if( dfs(board, word, idx+1, i-1, j) ) {
        //     board[i][j] = word[idx];
        //     return true;}
        // if( dfs(board, word, idx+1, i, j+1) ) {
        //     board[i][j] = word[idx];
        //     return true;}
        // if( dfs(board, word, idx+1, i, j-1) ){
        //     board[i][j] = word[idx];
        //     return true;
        // }  
        board[i][j] = word[idx];        
        return false;
    }
};
```
```cpp
// Trie + DFS
struct TrieNode{
   std::vector<TrieNode*> child;
   string word;

   TrieNode():child(vector<TrieNode*>(26, nullptr)), word(""){  
   }
};

/** Inserts a word into the trie. */
TrieNode* buildTrie(vector<string>& words) {
   TrieNode* root = new TrieNode();  
   for( auto word : words ){
       auto it = root;
       for ( auto w : word ) {
           if ( it->child[w - 'a'] == nullptr ) {
               it->child[w - 'a'] = new TrieNode();
            }
            it = it->child[w - 'a'];
       }
       it->word = word;  
   } 
    
   return root;
}

class Solution {
public:
    vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
        if( board.size() == 0 || board[0].size() == 0 || words.size() == 0 ) {
            return {};
        }
        
        TrieNode* root = buildTrie(words);
       
        vector<vector<bool>> visited(board.size(), vector<bool>(board[0].size(), false));
        vector<string> res;
        for(int i = 0; i < board.size(); i++){
            for(int j = 0; j < board[0].size(); j++){
               dfs(board, visited, res, root, i, j);
               //dfs(board, res, root, i, j );
            }
        }
        
        return res;
    }
//     void dfs(vector<vector<char>>& board, vector<string>& res, TrieNode* root, int i, int j){
//         if( i < 0 || i >= board.size() || j < 0 || j >= board[0].size() || board[i][j] == '#'){
//              return ;
//         }
        
//         if(root->child[board[i][j] - 'a'] != nullptr){
//             root = root->child[board[i][j] - 'a'];
//             if ( root->word != ""){
//                 res.emplace_back(root->word);
//                 root->word = "";
//             }
            
//             char tmp = board[i][j];
//             board[i][j] = '#';
//             dfs(board, res, root, i+1, j); 
//             dfs(board, res, root, i-1, j); 
//             dfs(board, res, root, i, j+1); 
//             dfs(board, res, root, i, j-1); 
//             board[i][j] = tmp;
//         }
//     }
    void dfs(vector<vector<char>>& board,vector<vector<bool>>& visited, vector<string>& result,TrieNode* root, int i, int j ){
        if( i < 0 || i >= board.size() || j < 0 || j >= board[0].size() || visited[i][j]){
            return ;
        }
        
        if(root->child[board[i][j] - 'a'] == nullptr){
            return ;
        }
        
        root = root->child[board[i][j] - 'a'];
        if(root->word != ""){
            result.emplace_back(root->word);
            root->word = "";
        }
        
        visited[i][j] = true;        
        dfs(board, visited, result, root, i+1, j);
        dfs(board, visited, result, root, i-1, j);
        dfs(board, visited, result, root, i, j+1);
        dfs(board, visited, result, root, i, j-1);
          
        visited[i][j] = false;
    }  
};
```
