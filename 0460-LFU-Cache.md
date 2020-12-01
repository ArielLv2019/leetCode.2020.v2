```
Design and implement a data structure for Least Frequently Used (LFU) cache.

Implement the LFUCache class:

LFUCache(int capacity) Initializes the object with the capacity of the data structure.
int get(int key) Gets the value of the key if the key exists in the cache. Otherwise, returns -1.
void put(int key, int value) Sets or inserts the value if the key is not already present. When the cache reaches its capacity, it should invalidate the least frequently used item before inserting a new item. For this problem, when there is a tie (i.e., two or more keys with the same frequency), the least recently used key would be evicted.
Notice that the number of times an item is used is the number of calls to the get and put functions for that item since it was inserted. This number is set to zero when the item is removed.

 

Example 1:

Input
["LFUCache", "put", "put", "get", "put", "get", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [3], [4, 4], [1], [3], [4]]
Output
[null, null, null, 1, null, -1, 3, null, -1, 3, 4]

Explanation
LFUCache lfu = new LFUCache(2);
lfu.put(1, 1);
lfu.put(2, 2);
lfu.get(1);      // return 1
lfu.put(3, 3);   // evicts key 2
lfu.get(2);      // return -1 (not found)
lfu.get(3);      // return 3
lfu.put(4, 4);   // evicts key 1.
lfu.get(1);      // return -1 (not found)
lfu.get(3);      // return 3
lfu.get(4);      // return 4
```

```cpp
class LFUCache {
private:
    void update(map<int, pair<int, int>>::iterator iter){
        freqMap[iter->second.second].erase(keyMap[iter->first]);
        if( freqMap[iter->second.second].size() == 0 ){
            freqMap.erase(iter->second.second);
        }
        ++iter->second.second;
        freqMap[iter->second.second].push_back(iter->first);
        keyMap[iter->first] = --freqMap[iter->second.second].end();
    }
    
public:
    LFUCache(int capacity):_capacity(capacity) {
        
    }
    
    int get(int key) {
        auto iter = cache.find(key);
        if(iter == cache.end()){
            return -1;
        }
        
        update(iter);
        return iter->second.first;
    }
    
    void put(int key, int value) {
        // ["LFUCache","put","get"]
        // [[0],[0,0],[0]]
        if(_capacity <= 0){ 
            return ;
        }
        
        auto iter = cache.find(key);
        if(iter != cache.end()){
            update(iter);
            cache[key].first = value;
            return ;
        }
        
        if(cache.size() >= _capacity){
            int delKey = freqMap.begin()->second.front();
            cache.erase(delKey);
            keyMap.erase(delKey);
            freqMap.begin()->second.pop_front();
            if(freqMap.begin()->second.size() == 0){ // 这一段可以省略，但是freqMap里面就会有不用的key碎片
                freqMap.erase(freqMap.begin());
            }
        }
        
        cache[key] = make_pair(value, 1);
        freqMap[1].push_back(key);
        keyMap[key] = --freqMap[1].end();     
    }
    
private:
    int _capacity;
    map<int, pair<int, int>> cache; // <key, <value, freq>>
    map<int, list<int>::iterator> keyMap; // <key, list::iterator>
    map<int, list<int>> freqMap; //<freq, list<key1, key2,...>
};

/**
 * Your LFUCache object will be instantiated and called as such:
 * LFUCache* obj = new LFUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```
