# [Min Stack](https://leetcode.com/problems/min-stack/description/?envType=study-plan-v2&envId=top-interview-150)
## Problem Statment
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/4e71c899-3883-4ea4-901c-3cf34b2d96d9)
## Solution
```java
import java.util.Stack;
class MinStack {
    Stack<Integer> mainStack;
    Stack<Integer> minStack;
    public MinStack() {
        mainStack = new Stack<>();
        minStack = new Stack<>();
    }
    
    public void push(int val) {
        mainStack.push(val);
        // There can be more than one value of min that's why  val <= minStack.peek()
        if (minStack.isEmpty() || val <= minStack.peek()) {
            minStack.push(val);
        }
    }
    
    public void pop() {
        if (!mainStack.isEmpty()) {
            int popped = mainStack.pop();
            if (minStack.peek() == popped) {
                minStack.pop();
            }
        }
    }
    
    public int top() {
        return mainStack.peek();
    }
    
    public int getMin() {
        return minStack.peek();
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(val);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```

## Solution
```java
class MinStack {

    private Deque<int[]> stack;

    public MinStack() {
        stack = new LinkedList<>();
    }
    
    public void push(int val) {
        int[] topItem = stack.peekFirst();
        int min = val;
        if (null != topItem) {
            min = Math.min(min, topItem[1]);   
        }
        stack.offerFirst(new int[] {val, min});
    }
    
    public void pop() {
        stack.pollFirst();
    }
    
    public int top() {
        return stack.peekFirst()[0];
    }
    
    public int getMin() {
        return stack.peekFirst()[1];
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(val);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```
