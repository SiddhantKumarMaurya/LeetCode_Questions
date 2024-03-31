# [Rotate Array](https://leetcode.com/problems/rotate-array/description/?envType=study-plan-v2&envId=top-interview-150)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/cde674f5-9258-4874-a473-64f27eda06f1)
## Solution 1st (recursive approach):
`Does not work when the size of array and rotation step are both even.`
```java
class Solution {
    public void rotate(int[] nums, int k) {
        if (k == 0) return;
        int length = nums.length;
        rotateHelper(nums, k, 0, nums[0], new boolean[length]);
    }

    // this logic does not work when the size of array is even and the rotation step is even.
    public void rotateHelper(int[] nums, int k, int i, int temp, boolean[] visited){
        if(!visited[i]) {
            visited[i] = true;
            int nextIndex = (i + k) % nums.length;
            int nextTemp = nums[nextIndex];
            nums[nextIndex] = temp;
            rotateHelper(nums, k, nextIndex, nextTemp, visited);
        }
    }
}
```
## Solution 2nd (Iterative Approach)
`Right approach but time limit exceeds when the size of array is very large`
`Time Complexity: O(n*k)`
```java
class Solution {
    public void rotate(int[] nums, int k) {
        if (k == 0) return;
        for (int i = 0; i < k; i++) {
            rotateOnce(nums);
        }
    }

    public void rotateOnce(int[] nums) {
        int length = nums.length;
        int temp = nums[length - 1];
        for(int i = length - 1; i > 0; i--) {
            nums[i] = nums[i - 1];
        }
        nums[0] = temp;
    }
}
```
## Solution 3rd
`Time Complexity: O(n)` `Space Complexity: O(1)` `Time taken for execution on LeetCode: 0ms`
```java
class Solution {
    public static void rotate(int[] nums, int k) {
        int n = nums.length;
        k %= n; // in case k is greater than the length of the array
        
        reverse(nums, 0, n - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, n - 1);
    }

    public static void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
}
```
## Solution 4th (cyclic approach just like the first one but successful)
`Time Complexity: O(n)` `Space Complexity: O(1)` `Time taken for execution of LeetCode: 2ms`
```java
class Solution {
    public static void rotate(int[] nums, int k) {
        int n = nums.length;
        k %= n; // in case k is greater than the length of the array
        
        if (k == 0) return; // No need to rotate if k is 0
        
        int count = 0;
        for (int start = 0; count < n; start++) {
            int current = start;
            int prev = nums[start];
            do {
                int next = (current + k) % n;
                int temp = nums[next];
                nums[next] = prev;
                prev = temp;
                current = next;
                count++;
            } while (start != current);
        }
    }
}
```
