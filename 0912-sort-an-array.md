```
Given an array of integers nums, sort the array in ascending order.

Example 1:
Input: nums = [5,2,3,1]
Output: [1,2,3,5]

Example 2:
Input: nums = [5,1,1,2,0,0]
Output: [0,0,1,1,2,5]
```
```cpp
// merge sort
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        if(nums.size() < 2){
            return nums;
        }
        vector<int> result(nums);
        merge_sort(result, 0, result.size() -1);
        return result;
    }
    
    void merge_sort(vector<int>& nums, int beg,int end){
        if(beg >= end){
            return ;
        }
        int mid = beg + (end - beg) / 2;
        merge_sort(nums, beg, mid);
        merge_sort(nums, mid+1, end);
        merge(nums, beg, mid, end);
        return ;
    }
    
    void merge(vector<int>& nums, int beg, int mid, int end){ //[beg, ...mid] [mid+1,..., end]
        int i = beg,  j = mid+1, k = 0;
        vector<int> tmp(end-beg+1);
        while( i <= mid && j <= end ) {
            if( nums[i] < nums[j] ) {
                tmp[k++] = nums[i++];
            }else{
                tmp[k++] = nums[j++];
            }
        }
        
        while(i <= mid){
            tmp[k++] = nums[i++];
        }
        while(j <= end){
            tmp[k++] = nums[j++];  
        }
        
        for(int i = 0; i < tmp.size(); i++){
            nums[beg+i] = tmp[i];
        }
    }
};
```
