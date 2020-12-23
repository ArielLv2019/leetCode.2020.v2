## 函数
```
make, len, cap, new, append, copy, close, delete
complex, real, img
panic, recover
```
## 零值
```
数字: 0
布尔: false
字符串: ""
接口，引用类型（指针，slice，map, 通道，函数): nil
数组，结构体：这样的复合类型，零值是所有元素或成员的零值。
```
## init()函数 && 包的初始化
```
https://blog.csdn.net/benben_2015/article/details/79486077
包的初始化：
为了使用导入的包，首先必须将其初始化。初始化总是以单线程执行，并且按照包的依赖关系顺序执行，每次初始化一个包。
这通过Golang的运行时系统控制。初始化的过程是自下向上的，main包最后初始化。

初始化导入的包（递归导入）
对包块中声明的变量进行计算和分配初始值
执行包中的init函数
```
## 数组
```
1） 数组长度是数组类型的一部分，[3]int与[4]int是不同的数组类型。
a := [2]int{1, 2}
d := [3]int{1,2}
fmt.Println(a == d) //编译错误，无法比较[2]int与[3]int

2） 如果一个数组的元素是可比较的，则这个数组也是可比较的，结果是两个数组的元素值是否完全相同
a := [2]int{1, 2}
b := [...]int{1,2}
c := [2]{1, 3}
fmt.Println(a == b, a==c, b==c) // true, false, false 

3) 数组指针
var ptr *[32]byte
```
