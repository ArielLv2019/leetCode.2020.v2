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
```cpp
// quick sort
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        if(nums.size() < 2){
            return nums;
        }
        sortArray(nums, 0, nums.size() - 1);
        return nums;
    }
    
    void sortArray(vector<int>& nums, int left, int right) {
        if(left >= right){
            return ;
        }
        int idx = partation(nums, left, right);
        sortArray(nums, left, idx-1);
        sortArray(nums, idx+1, right);
    }
    
    int partation(vector<int>& nums, int left, int right){
        if(left >= right){
            return left;
        }
        int pivotIdx = left + (right - left) / 2;
        int tag = nums[pivotIdx]; //防止退化成最坏情况
        swap(nums[right], nums[pivotIdx]);
        while(left < right){
            while(left < right && nums[left] <= tag){
                left++;
            }
            swap(nums[right], nums[left]);
            while(left < right && nums[right] >= tag){
                right--;
            }
            swap(nums[left],nums[right]);
        }
        
        return left;
    }
};
```
