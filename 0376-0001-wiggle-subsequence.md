```
给定一个数组，要求里面的元素为摆动序列，
如果数组满足摆动元素的要求，直接返回0； {1, 3, 2, 5, 4} -> 0
否则，如果删除一个元素，数组仍不能满足摆动序列的要求，则返回-1；{1,2,3,4,5} -> -1
否则，返回删除一个元素后数组满足摆动序列要求的删除方法。 {1, 5, 4, 3, 4, 2} -> 2, 因为删除5， 或者第一个4可以使序列满足摆动要求。
```
```
// 思路：
S1: 先判断该序列满足摆动要求的最长序列个数len，同时引用传递一个wrongIdx（初始为-1），
if(len == nums.size()) ---> 0
if(len < nums.size()-1) -----> -1
求有多少种方法删除元素的方法，并返回方法的个数. 
   方法一： 暴力求解删除每一个元素判断是不是满足摆动序列，如果满足就将res++
   方法二： 只需要对wrongIdx的前后三个元素做判断就可以，注意边界条件的处理，用min，max函数
```
```cpp
int validArrayMaxSize(vector<int>& nums, int& wrongIdx){
    if(nums.size() == 0 || nums.size() == 1){
        return nums.size();
    }
    
    wrongIdx = -1;
    int res = 1, pre = 0;
    for(int i = 1; i < nums.size(); i++){
        int diff = nums[i] - nums[i-1];
        if( (diff > 0 && pre <= 0) || (diff < 0 && pre >= 0)){
            res++;
            pre = diff;
        }else{
            wrongIdx = wrongIdx == -1 ? i : wrongIdx;
        }
    }
    return res;
}

bool validAfterDelete(vector<int>& arr, int idx){
    int iBeg = max(0, idx-3), iEnd = min(int(arr.size()), idx+4);
    vector<int> tmp(iEnd-iBeg-1, 0);
    for(int k = 0, i = iBeg; i < iEnd; i++){
        if( i == idx){
            continue ;
        }
        tmp[k++] = arr[i];
    }
    
    int wrongIdx = -1;
    validArrayMaxSize(tmp, wrongIdx);
    return wrongIdx == -1;
}

// 方法二： 对前后三个元素做判断
int validArray(vector<int>& arr){
    int wrongIdx = -1;
    int validLen = validArrayMaxSize(arr,wrongIdx);
    if(validLen == arr.size()){
        return 0;
    }
    if (validLen < arr.size() - 1){
        return -1;
    }
    
    int res = 0;
    
    //只需要对元素的前后三个元素做判断就可以了
    for(int i = wrongIdx, iEnd = max(0, wrongIdx - 3); i >= iEnd; i--){
        if(validAfterDelete(arr, i) == true){
            res++;
        }
    }
    
    return res;
}

// 方法一：暴力求解
int bruceArray(vector<int>& arr){
    int wrongIdx = -1;
    int validLen = validArrayMaxSize(arr,wrongIdx);
    if(validLen == arr.size()){
        return 0;
    }
    if (validLen < arr.size() - 1){
        return -1;
    }
    
    int res = 0;
    
    // 暴力删除每一个元素后对整个数组做判断
    for(int i = 0; i < arr.size(); i++){
        vector<int> tmp(arr.size()-1, 0);
        for(int m = 0, n = 0; m < arr.size(); m++){
            if(m == i){
                continue;
            }
            tmp[n++]=arr[m];
        }
        validArrayMaxSize(tmp,wrongIdx);
        if(wrongIdx == -1){
            res++;
        }
    }
    cout<<endl;
    return res;
}
        
int main(){
    vector<int> vec{1, 2, 3, 4, 5};
    vector<int> arr{1, 3, 2, 4, 3};
    vector<int> arr2{1, 3, 2, 1, 3};
    vector<int> arr3{1, 5, 4, 3, 4, 2};
//    cout<<validArray(vec) <<endl;
//    cout<<validArray(arr) <<endl;
    cout<<validArray(arr3) <<endl;
    cout<<bruceArray(arr3) << endl;
    
    //vector<int> vec{1, 99, 1, 99, 98, 2, 2};
    
    return 0;
}
```
