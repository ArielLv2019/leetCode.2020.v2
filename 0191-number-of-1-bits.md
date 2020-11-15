```
Write a function that takes an unsigned integer and returns the number of '1' bits it has (also known as the Hamming weight).

Note:
Note that in some languages such as Java, there is no unsigned integer type. In this case, the input will be given as a signed integer type. It should not affect your implementation, as the integer's internal binary representation is the same, whether it is signed or unsigned.
In Java, the compiler represents the signed integers using 2's complement notation. Therefore, in Example 3 above, the input represents the signed integer. -3.

Follow up:
If this function is called many times, how would you optimize it?
```

```cpp
// mask
class Solution {
public:
    int hammingWeight(uint32_t n) {
        uint32_t mask = 1;
        
        int result = 0;
        for(int i = 0; i < 32; i++){
            if( n & mask){
                result++;
            }
            mask <<= 1;
        }
        return result;
    }
};
```

```cpp
// n = n&(n-1)
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int result = 0;
        for(; n != 0;  n = n & ( n - 1 ) ){
            result++;
        }
        
        return result;
    }
};
```

```cpp
// bitset
class Solution {
public:
    int hammingWeight(uint32_t n) {
        std::bitset<32> b(n);
        
        return b.count();
    }
};
```
