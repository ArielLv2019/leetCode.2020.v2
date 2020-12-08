Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
getMin() -- Retrieve the minimum element in the stack.
 

Example 1:
Input
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

Output
[null,null,null,null,-3,null,0,-2]

Explanation
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2```
```
```
// go
type MinStack struct {
    cache []int
    minCache []int
}


/** initialize your data structure here. */
func Constructor() MinStack {
    return MinStack{
        cache : make([]int, 0),
        minCache: make([]int, 0),
    }
}


func (this *MinStack) Push(x int)  {
    this.cache = append(this.cache, x)
    if len(this.minCache) == 0 || this.minCache[len(this.minCache) - 1] >= x {
        this.minCache = append(this.minCache, x)
    }
}


func (this *MinStack) Pop()  {
    if len(this.cache) == 0 {
        return 
    }
    
    x := this.Top()
    if x == this.minCache[len(this.minCache)-1]{
        this.minCache = this.minCache[:len(this.minCache)-1]
    }
    this.cache = this.cache[:len(this.cache)-1]
}


func (this *MinStack) Top() int {
    if len(this.cache) == 0 {
        return -1
    }
    
    return this.cache[len(this.cache)-1]
}


func (this *MinStack) GetMin() int {
    if len(this.minCache) == 0 {
        return -1
    }
    
    return this.minCache[len(this.minCache)-1]
}


/**
 * Your MinStack object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Push(x);
 * obj.Pop();
 * param_3 := obj.Top();
 * param_4 := obj.GetMin();
 */
```
