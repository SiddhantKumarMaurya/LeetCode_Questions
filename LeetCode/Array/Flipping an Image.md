# [Flipping an Image](https://leetcode.com/problems/flipping-an-image/description/)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/vigilant-invention/assets/107787014/6fd06fa8-0925-4a72-b54f-dd82001cd02f)
## Solution
```java
class Solution {
    public int[][] flipAndInvertImage(int[][] image) {
        int rows = image.length;
        int columns = image[0].length;
        int temp = 0;
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < columns / 2; j++) {
                temp = image[i][j];
                image[i][j] = image[i][columns - j - 1];
                image[i][columns - j - 1] = temp;
            }
        }

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < columns; j++) {
                if(image[i][j] == 0) {
                    image[i][j] = 1;
                } else {
                    image[i][j] = 0;
                }
            }
        }
        return image;
    }
}
```
