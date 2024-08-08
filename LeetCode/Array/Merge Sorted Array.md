# [Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/description/?envType=study-plan-v2&envId=top-interview-150)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/8aa67a76-3c95-40c0-8143-684d3a50c253)
## Solution
### Java
```java
// import java.util.Arrays;

class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int len = m + n;
        int j = m - 1;
        int k = n - 1;
        int p = 0;
        if (m == 0) {
            // nums1 = nums2;
            // System.out.println(Arrays.toString(nums1));

            // In case the first array is empty copy all the elements of second array into the first
            for (int i = 0; i < len; i++) {
                nums1[i] = nums2[p];
                p++;
            }
        } else if (n != 0) {
            // Begin from the last index and start comparing the elements of the two arrays
            // copy the larger at the end of the nums1 array
            for (int i = len - 1; i >= 0; i--) {
                if (j >= 0 && k >= 0) {
                    if (nums1[j] < nums2[k]) {
                        nums1[i] = nums2[k];
                        k--;
                    } else {
                        nums1[i] = nums1[j];
                        nums1[j] = 0;
                        j--;
                    }
                    // if the last element of nums1 is coppied then move the zeroes to left
                    // for example:
                    // lets suppose num1 = 456000
                    // num2 = 123
                    // then, in first iteration
                    // num1 = 450006
                    // num2 = 123
                    // then, in second iteration
                    // num1 = 400056
                    // num2 = 123
                    // iteration 3: 
                    // 000456
                    // 123
                    // 00345
                    // 123
                    // and so on
                } else if (k >= 0){
                    nums1[i] = nums2[k];
                    k--;
                }
            }
        }
    }
}
```

---

## Solution2
```java
import java.util.Arrays;
public class MergeSortedArray {
  
  public void mergeSort(int[] nums1, int[] nums2, int m, int n) {
    int i = m - 1;
    int j = n - 1;
    int k = m + n - 1;
    while(i >= 0 && j >= 0 && k >= 0) {
     if (nums1[i] > nums2[j]) {
        nums1[k] = nums1[i];
        nums1[i] = 0;
        k--;
        i--;
      } else {
        nums1[k] = nums2[j];
        k--;
        j--;
      }
    }

    while(i >= 0 && k >= 0) {
      nums1[k] = nums1[i];
      i--;
      k--;
    }

    while(j >= 0 && k >= 0) {
      nums1[k] = nums1[j];
      k--;
      j--;
    }
    
    // To pass the test case3 (Example3)
    // my initial thought was nums1 = nums2 but that would locally assign the reference of nums2 to nums1
    // but outside the class when num1 is accessed it has its original reference thus has to change to the follwing code.
    if (m < 1) {
      nums1[0] = nums2[0];
    }
  }

  public static void main(String[] args) {
    int[] nums1 = {1, 2, 3, 0, 0, 0};
    int[] nums2 = {2, 5, 6};
    int m = 3;
    int n = 3;
    int[] nums3 = {1};
    int[] nums4 = {};
    int p = 1;
    int q = 0;
    int[] nums5 = {0};
    int[] nums6 = {1};
    int r = 0;
    int s = 1;
    new MergeSortedArray().mergeSort(nums1, nums2, m, n);
    System.out.println(Arrays.toString(nums1));
    new MergeSortedArray().mergeSort(nums3, nums4, p, q);
    System.out.println(Arrays.toString(nums3));
    new MergeSortedArray().mergeSort(nums5, nums6, r, s);
    System.out.println(Arrays.toString(nums5));
  }
}
```

---
### Python
```python
class Solution:
    def merge(self, nums1, m, nums2, n):
        len_merge = m + n
        j = m - 1
        k = n - 1
        p = 0
        
        if m == 0:
            # In case the first array is empty, copy all elements of the second array into the first.
            for i in range(len_merge):
                nums1[i] = nums2[p]
                p += 1
        elif n != 0:
            # Begin from the last index and start comparing the elements of the two arrays,
            # copy the larger at the end of the nums1 array.
            for i in range(len_merge - 1, -1, -1):
                if j >= 0 and k >= 0:
                    if nums1[j] < nums2[k]:
                        nums1[i] = nums2[k]
                        k -= 1
                    else:
                        nums1[i] = nums1[j]
                        nums1[j] = 0
                        j -= 1
                elif k >= 0:
                    nums1[i] = nums2[k]
                    k -= 1
```
