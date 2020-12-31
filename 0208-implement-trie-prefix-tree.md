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
// go
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
 ```cpp
 // cpp: vector
class TrieNode{
private:
    friend class Trie;
    std::vector<TrieNode*> child;
    bool isWord;
public:
    TrieNode():child(vector<TrieNode*>(26)), isWord(false){  
    }
};
class Trie {
private:
    TrieNode* root;
public:
    /** Initialize your data structure here. */
    Trie(): root(new TrieNode()) {
    }
    
    /** Inserts a word into the trie. */
    void insert(string word) {
        auto it = root;
        for ( auto w : word ) {
            if ( it->child[w-'a'] == nullptr ) {
                it->child[w-'a'] = new TrieNode();
            }
            it = it->child[ w - 'a'];
        }
        it->isWord = true;
    }
    
    /** Returns if the word is in the trie. */
    bool search(string word) {
        auto it = root;
        for ( auto w : word ) {
            if ( it->child[w - 'a'] == nullptr ){
                return false;
            }
            it = it->child[ w - 'a'];
        }
        
        return it->isWord;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
        auto it = root;
        for( auto p : prefix ){
            if( it->child[p - 'a'] == nullptr ){
                return false;
            }
            it = it->child[p - 'a'];
        }
        return true;
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
 ```
 
 ```cpp
 //cpp: set
class Trie {
private:
   std::set<string> all_words;
public:
    /** Initialize your data structure here. */
    Trie() {
    }
    
    /** Inserts a word into the trie. */
    void insert(string word) {
        all_words.emplace(word);
    }
    
    /** Returns if the word is in the trie. */
    bool search(string word) {
        return all_words.find(word) != all_words.end();
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
        auto itlow = all_words.lower_bound(prefix);
        return (*itlow).rfind(prefix, 0) == 0;
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
 ```
