```
Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

 

Example 1:

Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
Example 2:

Input: nums = [2,0,1]
Output: [0,1,2]
Example 3:

Input: nums = [0]
Output: [0]
Example 4:

Input: nums = [1]
Output: [1]
 

Constraints:

n == nums.length
1 <= n <= 300
nums[i] is 0, 1, or 2.
```
## 方法总结
+ 法一：排序
+ 法二：统计0，1，2的个数，将0， 1， 2重新插入数组
+ 法三：双指针
++ zero和second指针分别指向下一个0/2要放的位置，用one指针遍历整个数组，
```cpp
while(one <= second){
 if(nums[one]==0){
  if(one==zero){one++, zero++}
  else{swap(nums[one], nums[zero]); zero++;}
 }else{
  if(nums[one] == 2){swap(nums[one], nums[second--]);}
  else{one++;} //nums[one] == 1;
 }
}
```

```cpp
//双指针
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int zero = 0,one = 0, second = nums.size()-1;
        
        while(one <= second){
            if(nums[one] == 0){
                if(one == zero){
                    one++;
                }else{
                    swap(nums[zero], nums[one]);
                }               
                zero++;               
            }else{
                if(nums[one] == 2){
                    swap(nums[one], nums[second--]);
                }else{
                    one++;
                }
            }
        }
    }
};
```
