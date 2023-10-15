# [Remove Element](https://leetcode.com/problems/remove-element/description/?envType=study-plan-v2&envId=top-interview-150)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/eb9e4a83-0ae6-4274-a44e-31b1c92b6aa9)
## Solution
### Java
```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int len = nums.length;
        int j = len - 1;
        int notValCount = 0;

        for (int i = 0; i <= j; i++) {
            if (nums[i] == val) {
                notValCount++;
                while(j > i && nums[j] == val) {
                    notValCount++;
                    j--;
                }
                int temp = nums[i];
                nums[i] = nums[j];
                j--;
            }
        }

        return len - notValCount;
    }
}
```
### Java
```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int index = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != val) {
                nums[index] = nums[i];
                index++;
            }
        }
        return index;
    }
}
```

### Python
``` python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        index = 0
        for i in range(len(nums)):
            if nums[i] != val:
                nums[index] = nums[i]
                index += 1
        return index
```
