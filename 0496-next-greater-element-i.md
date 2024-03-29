```
You are given two arrays (without duplicates) nums1 and nums2 where nums1’s elements are subset of nums2. 
Find all the next greater numbers for nums1's elements in the corresponding places of nums2.

The Next Greater Number of a number x in nums1 is the first greater number to its right in nums2. 
If it does not exist, output -1 for this number.

Example 1:
Input: nums1 = [4,1,2], nums2 = [1,3,4,2].
Output: [-1,3,-1]
Explanation:
    For number 4 in the first array, you cannot find the next greater number for it in the second array, so output -1.
    For number 1 in the first array, the next greater number for it in the second array is 3.
    For number 2 in the first array, there is no next greater number for it in the second array, so output -1.

Example 2:
Input: nums1 = [2,4], nums2 = [1,2,3,4].
Output: [3,-1]
Explanation:
    For number 2 in the first array, the next greater number for it in the second array is 3.
    For number 4 in the first array, there is no next greater number for it in the second array, so output -1.
```

```cpp
// cpp: Start -> End with Stack
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2) {
        stack<int> sta;
        map<int,int> m;
        
        for ( auto& num : nums2 ) {
            while( !sta.empty() && sta.top() < num){
                m[sta.top()] = num;
                sta.pop();
            }
            sta.emplace(num);
        }
        
        vector<int> res;
        for( auto& num : nums1 ) {
            res.emplace_back( m.find(num)!= m.end()? m[num] : -1);
        }
        
        return res;
    }
};
```
