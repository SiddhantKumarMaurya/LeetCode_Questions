# Search Insert Position
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
