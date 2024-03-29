```
Given an array of integers nums sorted in ascending order, find the starting and ending position of a given target value.

If target is not found in the array, return [-1, -1].

Follow up: Could you write an algorithm with O(log n) runtime complexity?

 

Example 1:

Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
Example 2:

Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
Example 3:

Input: nums = [], target = 0
Output: [-1,-1]
```

```cpp
//查找某个等于target的值，找到之后从mid往两边找边界，注意判断条件
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int l = 0, r = nums.size()-1;
        while( l <= r ){
            int mid = l + ( ( r - l ) >> 2 );
            if( nums[mid] < target ){
                l = mid + 1;
            }else if( nums[mid] > target ){
                r = mid - 1;
            }else{ //找到之后从mid往两边找边界，注意判断条件
                l = mid, r = mid;
                while(l-1 >= 0 && nums[l-1] == target){
                    --l;
                }
                while( r+1 < nums.size() && nums[r+1] == target){
                    ++r;
                }
                
                return {l, r};
            }
        }
        return {-1,-1};;
    }
};
```
```cpp
// 实现一个查找最后一个<=target的函数，返回值就是[findFirst(target-1)+1, findFirst(target)]
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int r = searchLastEqualOrSmall(nums, target);       
        if (r != -1 && nums[r] == target){
            return {searchLastEqualOrSmall(nums, target-1)+1, r};
        }  
        return {-1, -1};
    }
    
    int searchLastEqualOrSmall(vector<int>& nums, int target) {
        int l = 0, r = nums.size() - 1;      
        while(l <= r){            
            int mid = l + (r-l)/2;
            if(nums[mid] > target){
                r = mid -1 ;
            }else{
                if(mid == nums.size() -1 || nums[mid+1] > target ){
                    return mid;
                }
                l = mid+1;
            }
        }
        return -1;
    }
};
```
```cpp
//查找第一个>=target的函数，返回值就是[findFirst(target), findFirst(target+1)-1]
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        return {searchFirstEqualOrLarge(nums, target), searchFirstEqualOrLarge(nums, target+1)-1};
    }
    int searchFirstEqualOrLarge(vector<int>& nums, int target) {
        int l = 0, r = nums.size() - 1;
        while(l <= r){
            int mid = l + (r-l)/2;
            if(nums[mid] < target){
                l = mid+1;                
            }else{
                if(mid == 0 || nums[mid-1] < target ){
                    return mid;
                }
                r = mid -1;                
            }
        }
        return -1;
    }
};
```
