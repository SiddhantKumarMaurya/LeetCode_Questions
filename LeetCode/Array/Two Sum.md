# [Two Sum](https://leetcode.com/problems/two-sum/)
   ## Code:
      ```java
      class Solution {
    public int[] twoSum(int[] nums, int target) {
        int len = nums.length;
        int res[] = new int[2];
        int sum = 0;
        boolean found = false;
        for (int i = 0; i < len; i++) {
            res[0] = i;
            sum = sum + nums[i];
            for(int j = i + 1; j < len; j++) {
                sum = sum + nums[j];
                if (sum == target) {
                    res[1] = j;
                    found = true;
                    break;
                }
                sum = sum - nums[j];
            }
            sum = sum - nums[i];
            if (found) {
                break;
            }
            
        }
        return res;
    }
}
```
