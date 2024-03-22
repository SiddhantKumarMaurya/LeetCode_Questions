# [Two Sum - Input Array is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/?envType=study-plan-v2&envId=top-interview-150)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/037c244e-1535-4c4c-9254-2f66dfcaea13)
## Solution
```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int length = numbers.length;

        int index1 = 0;
        int index2 = 0;

        for (int i = 0; i < length; i++) {
            int left_operand = numbers[i];
            int right_operand = target - left_operand;
            if (right_operand >= left_operand) {
                index2 = binarySearch(numbers, i + 1, right_operand);
                if (index2 == -1) {
                    continue;
                }
                index1 = i;
                break;
            }
             
        }
        index1++;
        index2++;
        int[] result = {index1, index2};
        return result;
    }

    public int binarySearch(int arr[], int l, int target) {
        int u = arr.length - 1;

        while (l <= u) {
            int mid = (l + u) / 2;
            if(arr[mid] < target) {
                l = mid + 1;
            } else if (arr[mid] > target) {
                u = mid - 1;
            } else return mid;
        }
        return -1;
    }
}
```
