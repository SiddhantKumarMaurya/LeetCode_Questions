# [Student Attendance Record II](https://leetcode.com/problems/student-attendance-record-ii/description/)
## Topics: `Dynamic Programming`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/8edfe3c8-7a77-4d11-9004-63390432cafb)
## Solution
```java
public class Solution {
    private static final int MOD = 1000000007;

    public int checkRecord(int n) {
        // dp[i][j][k] represents the number of sequences of length i with j 'A's and ending with k 'L's
        int[][][] dp = new int[n + 1][2][3];
        dp[0][0][0] = 1;  // Base case: empty sequence

        for (int i = 1; i <= n; i++) {
            for (int a = 0; a < 2; a++) {  // 0 or 1 'A's
                for (int l = 0; l < 3; l++) {  // 0, 1, or 2 'L's
                
                    // If we add 'P'
                    dp[i][a][0] = (dp[i][a][0] + dp[i - 1][a][l]) % MOD;
                    
                    // If we add 'A'
                    if (a > 0) {
                        dp[i][a][0] = (dp[i][a][0] + dp[i - 1][a - 1][l]) % MOD;
                    }
                    
                    // If we add 'L'
                    if (l > 0) {
                        dp[i][a][l] = (dp[i][a][l] + dp[i - 1][a][l - 1]) % MOD;
                    }
                }
            }
        }
        
        int result = 0;
        for (int a = 0; a < 2; a++) {
            for (int l = 0; l < 3; l++) {
                result = (result + dp[n][a][l]) % MOD;
            }
        }
        
        return result;
    }

    public static void main(String[] args) {
        Solution sol = new Solution();
        System.out.println(sol.checkRecord(2));  // Output: 8
        System.out.println(sol.checkRecord(1));  // Output: 3
        System.out.println(sol.checkRecord(10101));  // Output: 183236316
    }
}
```
---
## Solution
```java
class Solution {
    static final int M = 1000000007;

  public int checkRecord(int n) {
      long[] PorL = new long[n + 1]; // ending with P or L, no A
      long[] P = new long[n + 1]; // ending with P, no A
      PorL[0] = P[0] = 1; PorL[1] = 2; P[1] = 1;
  
      for (int i = 2; i <= n; i++) {
          P[i] = PorL[i - 1];
          PorL[i] = (P[i] + P[i - 1] + P[i - 2]) % M;
      }
      
      long res = PorL[n];
      for (int i = 0; i < n; i++) { // inserting A into (n-1)-length strings
      	long s = (PorL[i] * PorL[n - i - 1]) % M;
          res = (res + s) % M;
      }
      
      return (int) res;
    }
}
```
---
## Solution
```java
class Solution {
    static final int mod = 1000000007;

    public int checkRecord(int n) {
        long[][] mat = new long[][]{
            {1, 1, 1, 0, 0, 0},
            {1, 0, 0, 0, 0, 0},
            {0, 1, 0, 0, 0, 0},
            {1, 1, 1, 1, 1, 1},
            {0, 0, 0, 1, 0, 0},
            {0, 0, 0, 0, 1, 0}
        };

        long[][] res = pow(mat, n);
        long ans = 0;

        long[] initial = {1, 0, 0, 0, 0, 0};
        for(int i=0; i<=5; i++){
            long sum = 0;
            for(int j=0; j<=5; j++){
                sum = (sum + res[i][j] * initial[j]) % mod;
            }
            ans = (ans + sum) % mod;
        }
        return (int) (ans);
    }

    public long[][] pow(long[][] mat, int n) {
        long[][] ret = {{1, 0, 0, 0, 0, 0}, {0, 1, 0, 0, 0, 0}, {0, 0, 1, 0, 0, 0}, {0, 0, 0, 1, 0, 0}, {0, 0, 0, 0, 1, 0}, {0, 0, 0, 0, 0, 1}};
        while (n > 0) {
            if ((n % 2) == 1) {
                ret = multiply(ret, mat);
            }
            n /= 2;
            mat = multiply(mat, mat);
        }
        return ret;
    }

    public long[][] multiply(long[][] a, long[][] b) {
        long[][] c = new long[6][6];
        for (int i = 0; i <= 5; i++) {
            for (int j = 0; j <= 5; j++) {
                c[i][j] = 0; 
                for (int k = 0; k <= 5; k++) {
                    c[i][j] = (c[i][j] + a[i][k] * b[k][j]) % mod;
                }
            }
        }
        return c;    
    }
}
```
