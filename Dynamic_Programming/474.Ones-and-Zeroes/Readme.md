### 474.Ones-and-Zeroes

本题本质就是0-1背包问题，只不过cost变成了两个量。0-1背包问题已经有非常成熟的套路了。dp[i][j]表示用i个0和j个1最多可以拼出多少个完整的字符串。

```java
        class Solution {
    public int findMaxForm(String[] strs, int m, int n) {
        //max amount with m 0 and n 1
        int[][] dp = new int[m+1][n+1];
        for(String str : strs) {
            //check how many 0 and 1 in str
            int zeros = count(str);
            int ones = str.length() - zeros;
            //注意要从右下角开始
            for(int i=m; i>=zeros; i--) {
                for(int j=n; j>=ones; j--) {
                    //dp[i-zeros][j-ones] + 1
                    //dp[i][j]
                    dp[i][j] = Math.max(dp[i-zeros][j-ones] + 1, dp[i][j]);
                }
            }
            // print2D(dp);
            // System.out.println("");
        }
        return dp[m][n];
    }
    
    public static void print2D(int mat[][])
    {
        // Loop through all rows
        for (int[] row : mat)
 
            // converting each row as string
            // and then printing in a separate line
            System.out.println(Arrays.toString(row));
    }
    
    public int count(String str){
        int res = 0;
        for(char c : str.toCharArray()) {
            if(c == '0'){
                res++;
            }
        }
        return res;
    }
}
```

这里用temp的原因是方便起见，以免更新dp时使用了这一轮的新dp值。当然，也有取巧的办法省下temp的开辟，即在两个内存for循环里将i，j都按从大到小遍历，那么更新dp时就不会与新值冲突。


[Leetcode Link](https://leetcode.com/problems/ones-and-zeroes)
