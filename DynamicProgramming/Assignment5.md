Q4. Max Wine Profit

Problem Description

Given n wines in a row, with integers denoting the cost of each wine respectively. Each year you can sell the first or the last wine in the row. However, the price of wines increases over time. Let the initial profits from the wines be A1, A2, A3…An. In the Yth year, the profit from the ith wine will be Y*Ai. Calculate the maximum possible profit that can be obtained if you sell exactly one wine each year.

You are given an integer array A where A[i] denotes the cost of the ith wine.



Problem Constraints

1 <= n <= 1000
1 <= A[i] <= 1000


Input Format

The first and only argument is the integer array A.


Output Format

Return a single integer, the answer to the problem.


Example Input

Input 1:
A = [1 2 4 3 1]
Input 2:

A = [1]


Example Output

Output 1:
41
Output 2:

1


Example Explanation

Explanation 1:
The wines can be chosen in the following order - 1(1), 1(2), 2(6), 3(12), 4(20). The values in the brackets denote the values they were sold at.
Explanation 2:

Only 1 way exists.


Solution ->

    public static int WineProblemBU(int wines[]) {
        int n = wines.length;

        int dp[][] = new int[n][n];

        for (int slide = 0; slide < n; slide++) {
            for (int si = 0; si < n - slide; si++) {
                int ei = si + slide;
                int year = (wines.length - (ei - si + 1) + 1);
                if (si == ei) {
                    dp[si][ei] = wines[si] * year;
                } else {
                    int start = dp[si + 1][ei] + wines[si] * year;
                    int end = dp[si][ei - 1] + wines[ei] * year;

                    dp[si][ei] = Math.max(start, end);
                }
            }
        }
        return dp[0][n - 1];
    }

    
---------------------------------------------------------------------------------------------------------
H.W Q1. 0-1 Knapsack II

Problem Description
Given two integer arrays A and B of size N each which represent values and weights associated with N items respectively.

Also given an integer C which represents knapsack capacity.

Find out the maximum value subset of A such that sum of the weights of this subset is smaller than or equal to C.

NOTE: You cannot break an item, either pick the complete item, or don’t pick it (0-1 property).



Problem Constraints
1 <= N <= 500

1 <= C, B[i] <= 106

1 <= A[i] <= 50



Input Format
First argument is an integer array A of size N denoting the values on N items.

Second argument is an integer array B of size N denoting the weights on N items.

Third argument is an integer C denoting the knapsack capacity.



Output Format
Return a single integer denoting the maximum value subset of A such that sum of the weights of this subset is smaller than or equal to C.



Example Input
Input 1:

 A = [6, 10, 12]
 B = [10, 20, 30]
 C = 50
Input 2:

 A = [1, 3, 2, 4]
 B = [12, 13, 15, 19]
 C = 10


Example Output
Output 1:

 22
Output 2:

 0


Example Explanation
Explanation 1:

 Taking items with weight 20 and 30 will give us the maximum value i.e 10 + 12 = 22
Explanation 2:

 Knapsack capacity is 10 but each item has weight greater than 10 so no items can be considered in the knapsack therefore answer is 0. 


Solution ->

    public int func(int n,int val[], int wt[] ,int val_left,int[][]dp){
        if(val_left == 0){
            return 0;
        }
        if(n < 0){
            return 100000000;
        }
        if(dp[n][val_left] != -1){
            return dp[n][val_left];
        }
        int ans = func(n-1,val,wt,val_left,dp);
        if(val_left - val[n] >= 0){
            ans = Math.min(ans, func(n-1,val,wt,val_left-val[n],dp) + wt[n]);
        }
        return dp[n][val_left] = ans;
    }
    public int solve(int[] A, int[] B, int C) {
        int max = 25000;
        int dp[][] = new int[A.length+1][max+1];
        for(int[]x : dp){
            Arrays.fill(x,-1);
        }
        for(int i = max ; i > 0 ; i--){
            if(func(A.length-1,A,B,i,dp) <= C){
                return i;
            }
        }
        return 0;
    }

    
---------------------------------------------------------------------------------------------------------

Q2. Coin Sum Infinite

Problem Description
You are given a set of coins A. In how many ways can you make sum B assuming you have infinite amount of each coin in the set.

NOTE:

Coins in set A will be unique. Expected space complexity of this problem is O(B).
The answer can overflow. So, return the answer % (106 + 7).


Problem Constraints
1 <= A <= 500
1 <= A[i] <= 1000
1 <= B <= 50000



Input Format
First argument is an integer array A representing the set.
Second argument is an integer B.



Output Format
Return an integer denoting the number of ways.



Example Input
Input 1:

 A = [1, 2, 3]
 B = 4
Input 2:

 A = [10]
 B = 10


Example Output
Output 1:

 4
Output 2:

 1


Example Explanation
Explanation 1:

 The 4 possible ways are:
 {1, 1, 1, 1}
 {1, 1, 2}
 {2, 2}
 {1, 3} 
Explanation 2:

 There is only 1 way to make sum 10.


Solution ->

    public int coinChange(int[] A, int B) {
        long[] dp=new long[B+1];
        long m=(1000*1000)+7;
            dp[0]=1;
        for(int a:A){
        for(int i=a;i<=B;i++){
            dp[i]+=(dp[i-a])%m;
        }
    }
    return (int)(dp[B]%m);
    }

    
---------------------------------------------------------------------------------------------------------

Q-> 


Solution ->

    
---------------------------------------------------------------------------------------------------------

Q-> 


Solution ->

    
---------------------------------------------------------------------------------------------------------

Q-> 


Solution ->

    
---------------------------------------------------------------------------------------------------------

Q-> 


Solution ->

    
---------------------------------------------------------------------------------------------------------

Q-> 


Solution ->

    
---------------------------------------------------------------------------------------------------------

Q-> 


Solution ->

    
---------------------------------------------------------------------------------------------------------


