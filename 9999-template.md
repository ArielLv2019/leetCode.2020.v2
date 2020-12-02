```python
# recursion
def recursion(level, param1, param2,...):
  # recursion terminator
  if level > MAX_LEVEL:
    print_result
    return
  
  # process logic in current level
  process_data(level, data,...)
  
  # drill down
  self.recursion(level + 1, p1, ...)
  
  # reverse the current level status if needed
  reverse_state(level)
```

```python
# divide and conquer

def divide_conquer(problem, param1, param2, ...):
  # recursion terminatior
  if problem is None:
    print_result
    return
  
  # prepare data
  data = prepare_data(problem)
  subProblems = split_problem(problem, data)
  
  # conquer subProblems
  subResult1 = self.divide_conquer(subProblems[0], p1, ...)
  subResult2 = self.divide_conquer(subProblems[1], p1, ...)
  subResult3 = self.divide_conquer(subProblems[2], p1, ...)
  ...
  
  # process and generate the final result
  result = process_result(subResult1, subResult2, subResult3, ...)
```

```python
// BFS
def BFS(graph, start, end):
  queue = []
  queue.append(start)
  visited.add(start)// 树不需要记录visited，但是图需要
  
  while queue:
    node = queue.pop()
    visited.add(node)
    
    process(node)
    nodes = generate_related_nodes(node)//做两件事： 1）找node的后继节点； 2）判断node的后继节点没有被访问过
    queue.push(nodes)
    
  # other processing work
  # ...
```
```python
// DFS + 递归
visited = set()
def DFS(node, visited):
  visited.add(node)
  # process current node here.
  ...
  for next_node in node.children():
    if not nex_node in visited:
      dfs(next_node, visited)
```

```python 
// DFS + stack
def DFS(self, tree):
  if tree.root is None:
    return []
  
  visited, stack = [], [tree.root]
  while stack:
    node = stack.pop()
    visited.add(node)
    
    process(node)
    nodes = generate_related_nodes(node)
    stack.push(nodes)
    
  # other processing work
  ...
```
```python
// 二分查找
left, right = 0, len(array) - 1
while left <= right:
  mid = left + (right - left)/2
  if array[mid] == target:
    // find the target
    break or return result
  elif array[mid] < target:
    left = mid+1
  else:
    right = mid-1
 ``` 
 ```python
 // DP
 
 //状态定义
 dp = new int [m+1][n+1];
 
 //初始状态
 dp[0][0] = x;
 dp[0][1] = y;
 ...
 
 // DP状态的推到
 for i = 0; i <= n; i++{
  for j = 0; j <= m; j++ {
    ...
    dp[i][j] = min{dp[i-1][j], dp[i][j-1], etc.}
  }
 }
 
 return dp[m][n]; //最优解
 ```
  
 ```java
 // Trie
 static final int ALPHABET_SIZE = 256; // 如果都是小写字母，直接用26就可以
 
 static class TrieNode{
  TrieNode[] children = new TireNode[ALPHABET_SIZE];
  boolean isEndOfWord = false;
  TireNode() {
    isEndOfWord = false;
    for (int i = 0; i < ALPHABET_SIZE; i++) {
      children[i] = null;
    }
  }
};
```

```python
class TrieNode:
  # Trie node class
  def __init__(self):
    self.children = [None] * ALPHABET_SIZE
    
    # isEndOfWord is True if node represent the end of the word
    self.isEndOfWord = False
```
  
```python
// 并查集伪代码
function MakeSet(x)
  x.parent := x

function Find(x)
  if x.parent == x
    return
  else
    return Find(x.parent)
    
function Uinon(x,y)
  xRoot := Find(x)
  yRoot := Find(y)
  xRoot.Parent := yRoot
  
// union优化一： 对并查集进行合并 && 将rank低的合并到rank高的
function Uinon(x,y)
  xRoot := Find(x)
  yRoot := Find(y)
  if xRoot == yRoot //x,y 在同一个集合，直接返回
    return
  
  if xRoot.Rank < yRoot.Rank
    xRoot.parent := yRoot
  else if xRoot.Rank > yRoot.Rank
    yRoot.parent := xRoot
  else //xRoot和yRoot的rank相等
    yRoot.parent := xRoot
    xRoot.rank := xRoot.rank + 1  
```

```java
//并查集的java实现
public class QuickUnionUF{
  private int[] roots;
  
  //初始化
  public QuickUnionUF(int N){
    roots = new int[N]l
    for( int i = 0; i < N; i++){
      roots[i] = i;
    }
  }
  
  // 查找
  private int findRoot(int i){
    int root = i;
    while(root != roots[root]){ //查找i的最上面的root
      root = roots[root];
    }
    
    while( i != roots[i]){ //union优化二：路径压缩，将root->i路径上所有元素指向最上面的root
      int tmp = roots[i];
      roots[i] = root;
      i = tmp;
    }
    return root;
  }
  
  public boolean connected(int p, int q){
    return findRoot(p) == findRoot(q);
  }
  
  public void union(int p, int q){
    int pRoot = findRoot(p);
    int qRoot = findRoot(q);
    roots[pRoot] = qRoot;
  }
}
```

```
位运算操作
1) X & 1 == 1 OR == 0 判断奇偶 ( X % 2 == 1)
2) X = X & (X-1): 清零最低位的1
3) X & -X : 得到最低位的1
```
  
