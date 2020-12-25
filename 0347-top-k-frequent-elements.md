```
Given a non-empty array of integers, return the k most frequent elements.

Example 1:

Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
Example 2:

Input: nums = [1], k = 1
Output: [1]
Note:

You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
Your algorithm's time complexity must be better than O(n log n), where n is the array's size.
It's guaranteed that the answer is unique, in other words the set of the top k frequent elements is unique.
You can return the answer in any order.
```
```cpp
// cpp: map + priority_queue
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        map<int,int> m;
        for(auto& num : nums){
            m[num]++;
        }
        priority_queue<pair<int, int>, vector<pair<int,int>>, greater<pair<int,int>>> pq;
        for(auto& v : m){
            pq.emplace(pair{v.second, v.first});
            if(pq.size() > k){
                pq.pop();
            }
        }
        
        vector<int> res;
        while( !pq.empty() ){
            res.emplace_back(pq.top().second);
            pq.pop();
        }
        
        return res;
    }
};
```

```go
// go: sort
func topKFrequent(nums []int, k int) []int {
    m := make(map[int]int)
    for _, num := range nums{
        m[num]++
    }
    
    res := make([]int, 0)
    for key, _:= range m {
        res = append(res, key)
    }
    
    sort.Slice(res, func(i, j int) bool {
        return m[res[i]] > m[res[j]]
    })
    
    return res[:k]
}

```
