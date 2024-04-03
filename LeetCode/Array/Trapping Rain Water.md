# [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/description/?envType=study-plan-v2&envId=top-interview-150)
## Topics: `Array`, `Two Pointers`, `Dynamic Programming`, `Stack`, `Monotonic Stack`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/4c246752-1e2b-487e-9176-c38b409e5cba)
## Solution `Monotonic Stack`
```java
// Using monotonic decreasing stack
import java.util.Stack;
class Solution {
    public int trap(int[] height) {
        int length = height.length;
        Stack<Integer> stack = new Stack<>();
        int trappedWater = 0;
        for (int i = 0; i < length; i++) {
            while (!stack.isEmpty() && height[i] > height[stack.peek()]) {
                int top = stack.pop();
                if (stack.isEmpty()) break;
                int distance = i - stack.peek() - 1;
                int boundHeight = Math.min(height[i], height[stack.peek()]) - height[top];
                trappedWater += boundHeight * distance;
            }
            stack.push(i);
        }
        return trappedWater;
    }
}
```
***
## Solution `Two Pointers`
`Time Complexity less than stack method`
```java
// Using two pointers
import java.util.Stack;
class Solution {
    public int trap(int[] height) {
        int length = height.length;
        int left = 0;
        int right = length - 1;
        int leftMax = 0;
        int rightMax = 0;
        int trappedWater = 0;
        while (left < right) {
            if (height[left] <= height[right]) {
                if (height[left] >= leftMax) leftMax = height[left];
                else trappedWater += leftMax - height[left];
                left++;
            } else {
                if (height[right] >= rightMax) rightMax = height[right];
                else trappedWater += rightMax - height[right];
                right--;
            }
        }
        return trappedWater;
    }
}
```
