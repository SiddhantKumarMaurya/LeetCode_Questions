# [Remove Duplicates from Sorted Array II](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/description/?envType=study-plan-v2&envId=top-interview-150)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/b65f2fc1-1519-4103-bd23-138e2b180b1d)
## Solution
### Java
```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int len = nums.length;
        int currentNumber = 0;
        int currentNumberCount = 0;
        int k = 0;

        // Handles Corner Case: if length of array is one
        if (len == 1) {
            return 1;
        }

        // Iterate through entire array untill you reach len - 2
        // To avoid index of bound error: iterate till len - 2
        for (int i = 0; i < len - 1; i++) {

            // keep track of current number and its frequency
            currentNumber = nums[i];
            currentNumberCount += 1;

            // As soon as you find an unidentical number arrange the current number in the array
            if (nums[i] != nums[i + 1]) {
                if (currentNumberCount >= 2) {
                    nums[k++] = currentNumber;
                    nums[k++] = currentNumber;
                    currentNumberCount = 0;
                } else {
                    nums[k++] = currentNumber;
                    currentNumberCount = 0;
                }
            }
            
            // To access the last two elements of the array
            if (i == len - 2 && nums[i] == nums[i + 1]) {
                nums[k++] = currentNumber;
                nums[k++] = currentNumber;
                currentNumberCount = 0;
            }
            
            // To access the last element of the array
            if (i == len - 2 && nums[i] != nums[i + 1]) {
                nums[k++] = nums[i + 1];
            }
        }
        return k;
    }
}
```

### Python
``` python
class Solution:
    def removeDuplicates(self, nums):
        length = len(nums)
        current_number = 0
        current_number_count = 0
        k = 0

        # Handles Corner Case: if the length of the array is one
        if length == 1:
            return 1

        # Iterate through the entire array until you reach length - 2
        # To avoid an index out of bounds error, iterate until length - 2
        for i in range(length - 1):
            # Keep track of the current number and its frequency
            current_number = nums[i]
            current_number_count += 1

            # As soon as you find an unidentical number, arrange the current number in the array
            if nums[i] != nums[i + 1]:
                if current_number_count >= 2:
                    nums[k] = current_number
                    nums[k + 1] = current_number
                    k += 2
                    current_number_count = 0
                else:
                    nums[k] = current_number
                    k += 1
                    current_number_count = 0

            # To access the last two elements of the array
            if i == length - 2 and nums[i] == nums[i + 1]:
                nums[k] = current_number
                nums[k + 1] = current_number
                k += 2
                current_number_count = 0

            # To access the last element of the array
            if i == length - 2 and nums[i] != nums[i + 1]:
                nums[k] = nums[i + 1]
                k += 1

        return k

```
