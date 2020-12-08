```
Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (push, peek, pop, and empty).

Implement the MyQueue class:

    void push(int x) Pushes element x to the back of the queue.
    int pop() Removes the element from the front of the queue and returns it.
    int peek() Returns the element at the front of the queue.
    boolean empty() Returns true if the queue is empty, false otherwise.

Notes:

    You must use only standard operations of a stack, which means only push to top, peek/pop from top, size, and is empty operations are valid.
    Depending on your language, the stack may not be supported natively. You may simulate a stack using a list or deque (double-ended queue) as long as you use only a stack's standard operations.

Follow-up: Can you implement the queue such that each operation is amortized O(1) time complexity? In other words, performing n operations will take overall O(n) time even if one of those operations may take longer.

 

Example 1:

Input
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]
Output
[null, null, null, 1, 1, false]

Explanation
MyQueue myQueue = new MyQueue();
myQueue.push(1); // queue is: [1]
myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
myQueue.peek(); // return 1
myQueue.pop(); // return 1, queue is [2]
myQueue.empty(); // return false 

Constraints:

    1 <= x <= 9
    At most 100 calls will be made to push, pop, peek, and empty.
    All the calls to pop and peek are valid.
```
```cpp
class MyQueue {
private:
    std::stack<int> sIn, sOut;
    
public:
    /** Initialize your data structure here. */
    MyQueue() {
        
    }
    
    /** Push element x to the back of queue. */
    void push(int x) {
        sIn.emplace(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    int pop() {
       if (sOut.empty()){
           move();
       } 

       int result = sOut.top();
       sOut.pop();

       return result;
    }
    
    /** Get the front element. */
    int peek() {
       if (sOut.empty()){
          move();
       } 
       return sOut.top();
    }
    
    /** Returns whether the queue is empty. */
    bool empty() {
        return sIn.empty() && sOut.empty();
    }
    
    void move(){
        while(!sIn.empty()){
            sOut.emplace(sIn.top());
            sIn.pop();
        }
    }
};

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue* obj = new MyQueue();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->peek();
 * bool param_4 = obj->empty();
 */
 ```
 ```
 // push的时候处理顺序
class MyQueue {
public:
    /** Initialize your data structure here. */
    MyQueue() {
    }
    
    /** Push element x to the back of queue. */
    void push(int x) {
        // Pushing all elements of s1 into s2 to push x at the end
        while( !outStack.empty() ){
            inStack.emplace(outStack.top());
            outStack.pop();
        }
        inStack.emplace(x);// pushing x at top.
		// now again reversing the stack into s1.
        while( !inStack.empty() ){
            outStack.emplace(inStack.top());
            inStack.pop();
        }
    }
    
    /** Removes the element from in front of queue and returns that element. */
    int pop() {
        int result = peek();
        outStack.pop();
        return result;
    }
    
    /** Get the front element. */
    int peek() {
        return outStack.top();
    }
    
    /** Returns whether the queue is empty. */
    bool empty() {
        return inStack.empty() && outStack.empty();
    }

private:
    std::stack<int> inStack;
    std::stack<int> outStack;
};

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue* obj = new MyQueue();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->peek();
 * bool param_4 = obj->empty();
 */
 ```
