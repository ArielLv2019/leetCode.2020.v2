```
Design a data structure that follows the constraints of a Least Recently Used (LRU) cache.

Implement the LRUCache class:
LRUCache(int capacity) Initialize the LRU cache with positive size capacity.
int get(int key) Return the value of the key if the key exists, otherwise return -1.
void put(int key, int value) Update the value of the key if the key exists. Otherwise, add the key-value pair to the cache. If the number of keys exceeds the capacity from this operation, evict the least recently used key.
Follow up:
Could you do get and put in O(1) time complexity?

Example 1:
Input
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
Output
[null, null, null, 1, null, -1, null, -1, 3, 4]

Explanation
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4
```

```cpp
// hash table + linked list
// list: key
// hashTable: <key, <value, list::iterator>
class LRUCache {
private:
    void touch(map<int, pair<int, list<int>::iterator>>::iterator it){
        used.erase(it->second.second);
        used.push_front(it->first); // save key->list
        it->second.second = used.begin();
    }
    
public:
    LRUCache(int capacity) : _capacity(capacity){
        
    }
    
    int get(int key) {
        auto it = cache.find(key);
        if(it == cache.end()){
            return -1;
        }
        touch(it);
        return it->second.first;
    }
    
    void put(int key, int value) {
        auto it = cache.find(key);
        if( it != cache.end()){
            touch(it);
        }else{
            if(cache.size() == _capacity){
                cache.erase(used.back());
                used.pop_back();
            }
            used.push_front(key);
        }
        cache[key] = {value, used.begin()};
    }
private:
    int _capacity;
    list<int> used;
    map<int, pair<int, list<int>::iterator>> cache;    
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
 ```
 
 ```cpp
// hash table + linked list + list.splice()
// list: <key, value>
// hashTable: <key, list::iterator>
class LRUCache {  
public:
    LRUCache(int capacity) : _capacity(capacity){
        
    }
    
    int get(int key) {
        auto it = cache.find(key);
        if(it == cache.end()){
            return -1;
        }
        if(it->second.second != used.begin()){
            used.splice(used.begin(), used, it->second.second);
        }
        return it->second.first;
    }
    
    void put(int key, int value) {
        auto it = cache.find(key);
        if( it != cache.end()){
            if(it->second.second != used.begin()){
                used.splice(used.begin(), used, it->second.second);
            }
        }else{
            if(cache.size() == _capacity){
                cache.erase(used.back());
                used.pop_back();
            }
            used.push_front(key);
        }
        cache[key] = {value, used.begin()};
    }
private:
    int _capacity;
    list<int> used;
    map<int, pair<int, list<int>::iterator>> cache;    
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```
