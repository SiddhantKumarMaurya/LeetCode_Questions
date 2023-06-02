# [Search Insert Position](https://leetcode.com/problems/search-insert-position/)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/vigilant-invention/assets/107787014/0c5f2d8e-0fe9-4849-ae18-9c3a424702d3)
## Solution
```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int len = nums.length;
        int low = 0;
        int high = len-1;
        int mid = (low + high) /  2;
        while(low < high) {
            mid = (low + high) / 2;
            if (target > nums[mid]) {
                low = mid + 1;
            }
            else if(target < nums[mid]) {
                high = mid - 1;
            }
            else {
                break;
            }
        }
        if (low == high) {
            if (target > nums[low]) {
                int index = low + 1;
                if (index >= 0) return index;
                else return 0;
            }
            else {
                int index = low;
                if (index >= 0) return index;
                else return 0;
            }
        }
        else return mid;
    }
}
```
