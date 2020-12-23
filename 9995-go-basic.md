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
## make和new的区别
```
https://www.cnblogs.com/ghj1976/archive/2013/02/12/2910384.html
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
## slice
```
1) slice操作符s[i:j](其中0<=i<=j<=cap(s))创建了一个新的slice，这个新的slice引用了序列s中从[i,j-1]索引位置的所有元素，s可以是数组，指向数组的指针或者slice。
2）如果slice的引用超出了被引用对象的容量，即cap(s): 导致程序当机；
  如果slice的引用超出了被引用对象的长度，即len(s): 最终slice会比原slice长。
3）与数组不同，slice无法比较，不能用==来判断两个slice是否拥有相同的元素。
标准库提供了极度优化的函数bytes.Equal来比较两个字节slice([]byte),但是对于其他类型的slice，需要自己写函数来进行比较。
```
