```
Given an unsorted array of integers, find the length of longest increasing subsequence.

Example:
Input: [10,9,2,5,3,7,101,18]
Output: 4 
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 

Note:
There may be more than one LIS combination, it is only necessary for you to return the length.
Your algorithm should run in O(n2) complexity.
Follow up: Could you improve it to O(n log n) time complexity?
```
```cpp
// DP
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
       if(nums.size() <= 0){
           return 0;
       } 
        
       int result = 1;
       vector<int> lis(nums.size(), 1);
       for(int i = 1; i < nums.size(); i++){
           for(int j = 0; j < i; j++){
               if(nums[j] < nums[i]){
                   lis[i] = max(lis[i], lis[j]+1);
               }
           }
           result = max(result, lis[i]);
       }
       return result;
    }
};
```
```cpp
// binary search
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
       if(nums.size() <= 0){
           return 0;
       } 
        
       vector<int> lis;
       for(int i = 0; i < nums.size(); i++){
          auto it = std::lower_bound(lis.begin(),lis.end(), nums[i]);
          if(it == lis.end()){//增加数组元素
              lis.emplace_back(nums[i]); 
          }else{ // 替换
              *it = nums[i];
          }
       }
       return lis.size();
    }
};
```
```cpp
// binary search + lower_bound
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
       if(nums.size() <= 0){
           return 0;
       } 
        
       vector<int> lis;
       for(int i = 0; i < nums.size(); i++){
          int idx = lower_bound(lis, nums[i]);
          if(idx == lis.size()){
              lis.emplace_back(nums[i]); 
          }else{ // 替换
              lis[idx]=nums[i];
          }
       }
       return lis.size();
    }
private:
    int lower_bound(vector<int>& nums, int target){
        if(nums.size() <= 0){
            return nums.size();
        }
        int left = 0, right = nums.size() - 1;
        while(left <= right){
            int mid = left + (right - left) / 2;
            if(nums[mid] < target){
                left = mid+1;
            }else{
                right = mid - 1;
            }
        }
        
        return left;
    }
};
```
