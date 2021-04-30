```
Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

 

Example 1:

Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
Example 2:

Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.

```
```cpp
// cpp: sort
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        if(intervals.size() < 2){
            return intervals;
        }
        std::sort(begin(intervals), end(intervals), [](vector<int>& a, vector<int>b){
            return a.front() < b.front();
        });
        vector<vector<int>> res;
        res.emplace_back(intervals[0]);
        for(int i = 1; i < intervals.size(); i++){
            if(intervals[i].front() > res.back().back()){
                res.emplace_back(intervals[i]);
            }else{
                res.back().back() = max(res.back().back(), intervals[i].back());
            }
        }
        
        return res;
    }
};
```
