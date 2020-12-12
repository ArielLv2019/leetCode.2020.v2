```
Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

 

Example 1:
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

Example 2:
Input: nums = [0,1]
Output: [[0,1],[1,0]]

Example 3:
Input: nums = [1]
Output: [[1]]
```

```cpp
class Solution {
public:
    // perm(a, b, c) = a + perm(b, c) -> perm(b,c) = b + perm(c)
    //                 b + perm(a, c)                c + perm(b)
    //                 c + perm(a, b)
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> result;
        permuteImpl(nums, result, 0, nums.size());
        return result;
    }
    
    void permuteImpl(vector<int>& nums, vector<vector<int>>& result, int pos, int len){
        if(pos == len){ // print/store a permutation
            result.emplace_back(nums);
            return ;
        }
        for(int i = pos; i < len; i++){
            swap(nums[i], nums[pos]); // swaping the head, e.g. abc -> bac
            permuteImpl(nums, result, pos+1, len); // then do b + perm(a, c)
            swap(nums[i], nums[pos]);  // swaping back, e.g. bac -> abc
        }
        return ;
    }
};
```
