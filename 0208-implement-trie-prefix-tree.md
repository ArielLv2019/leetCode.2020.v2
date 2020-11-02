```
Implement a trie with insert, search, and startsWith methods.

Example:

Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // returns true
trie.search("app");     // returns false
trie.startsWith("app"); // returns true
trie.insert("app");   
trie.search("app");     // returns true

Note:

    You may assume that all inputs are consist of lowercase letters a-z.
    All inputs are guaranteed to be non-empty strings.

```
```go
type Trie struct {
    Val char
    Childrens []TrieNode
    IsWork bool
}


/** Initialize your data structure here. */
func Constructor() Trie {
    return Trie{
      
    }
}


/** Inserts a word into the trie. */
func (this *Trie) Insert(word string)  {
    
}


/** Returns if the word is in the trie. */
func (this *Trie) Search(word string) bool {
    
}


/** Returns if there is any word in the trie that starts with the given prefix. */
func (this *Trie) StartsWith(prefix string) bool {
    
}


/**
 * Your Trie object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Insert(word);
 * param_2 := obj.Search(word);
 * param_3 := obj.StartsWith(prefix);
 */
```
```go
type TrieNode struct{
    Val rune
    Children []*TrieNode
    IsWord bool
}

type Trie struct {
    root *TrieNode
}


/** Initialize your data structure here. */
func Constructor() Trie {
    return Trie{
        root: &TrieNode{
            Children: make([]*TrieNode, 26),
        },
    }
}


/** Inserts a word into the trie. */
func (this *Trie) Insert(word string)  {
    root := this.root
    
    for _, w := range word{
        if root.Children[w-'a'] == nil{
            root.Children[w-'a'] = &TrieNode{
                Val: w,
                Children: make([]*TrieNode, 26),
            }
        }
        root = root.Children[w-'a']
    }
    
    root.IsWord = true
}


/** Returns if the word is in the trie. */
func (this *Trie) Search(word string) bool {
    root := this.root
    for _, w := range word{
        if root.Children[w-'a'] == nil{
            return false
        }
        root = root.Children[w-'a']
    }
    
    return root.IsWord
}


/** Returns if there is any word in the trie that starts with the given prefix. */
func (this *Trie) StartsWith(prefix string) bool {
    root := this.root
    for _, w := range prefix{
        if root.Children[w-'a'] == nil{
            return false
        }
        root = root.Children[w-'a']
    }
    
    return true
}
 ```
