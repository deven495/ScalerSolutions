Q1. Unique Paths in a Grid

Problem Description
Given a grid of size n * m, lets assume you are starting at (1,1) and your goal is to reach (n, m). At any instance, if you are on (x, y), you can either go to (x, y + 1) or (x + 1, y).

Now consider if some obstacles are added to the grids. How many unique paths would there be? An obstacle and empty space is marked as 1 and 0 respectively in the grid.



Problem Constraints
1 <= n, m <= 100
A[i][j] = 0 or 1



Input Format
Firts and only argument A is a 2D array of size n * m.



Output Format
Return an integer denoting the number of unique paths from (1, 1) to (n, m).



Example Input
Input 1:

 A = [
        [0, 0, 0]
        [0, 1, 0]
        [0, 0, 0]
     ]
Input 2:

 A = [
        [0, 0, 0]
        [1, 1, 1]
        [0, 0, 0]
     ]


Example Output
Output 1:

 2
Output 2:

 0


Example Explanation
Explanation 1:

 Possible paths to reach (n, m): {(1, 1), (1, 2), (1, 3), (2, 3), (3, 3)} and {(1 ,1), (2, 1), (3, 1), (3, 2), (3, 3)}  
 So, the total number of unique paths is 2. 
Explanation 2:

 It is not possible to reach (n, m) from (1, 1). So, ans is 0.


Solution -> Top Down Approach TC O(N^2) SC O(N^2)

    public int paths(int row, int col , int[][]q , int[][] dp){
        if(row >= q.length || col >= q[0].length || q[row][col] == 1){
            return 0;
        }
        if(row == q.length-1 && col == q[0].length-1){
            return 1;
        }
        if(dp[row][col] != 0){
            return dp[row][col];
        }
        int ch = paths(row,col+1,q,dp);
        int cv = paths(row+1,col,q,dp);

        return dp[row][col] = ch + cv;
    }
    public int uniquePathsWithObstacles(int[][] A) {
        int dp[][] = new int[A.length][A[0].length];
        return paths(0,0,A,dp);
    }


    
---------------------------------------------------------------------------------------------------------
Q2. N digit numbers

Problem Description
Find out the number of A digit positive numbers, whose digits on being added equals to a given number B.

Note that a valid number starts from digits 1-9 except the number 0 itself. i.e. leading zeroes are not allowed.

Since the answer can be large, output answer modulo 1000000007



Problem Constraints
1 <= A <= 1000

1 <= B <= 10000



Input Format
First argument is the integer A

Second argument is the integer B



Output Format
Return a single integer, the answer to the problem



Example Input
Input 1:

 A = 2
 B = 4
Input 2:

 A = 1
 B = 3


Example Output
Output 1:

 4
Output 2:

 1


Example Explanation
Explanation 1:

 Valid numbers are {22, 31, 13, 40}
 Hence output 4.
Explanation 2:

 Only valid number is 3


Solution ->

    int mod = 1000000007;
    public int countWays(int A,int B,int[][]dp){
        if(B < 0){
            return 0;
        }
        if(A == 0 && B == 0){
            return 1;
        }
        if(A == 0 && B != 0){
            return 0;
        }
        if(A != 0 && B == 0){
            return 0;
        }
        if(dp[A][B] != -1){
            return dp[A][B];
        }
        int count = 0;
        for(int i = 0 ; i <= 9 ; i++){
            count = (count%mod + countWays(A-1,B-i,dp)%mod)%mod;
        }
        return dp[A][B] = count;
    }
    public int solve(int A, int B) {
        int dp[][] = new int[A+1][B+1];
        for(int i = 0 ; i < dp.length ; i++){
            for(int j = 0 ; j < dp[0].length ; j++){
                dp[i][j] = -1;
            }
        }
        // Arrays.fill(dp,-1);
        return countWays(A,B,dp);
    }

    
---------------------------------------------------------------------------------------------------------

Q3. Min Sum Path in Triangle

Problem Description
Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

Adjacent numbers for jth column of ith row is jth and (j+1)th column of (i + 1)th row



Problem Constraints
|A| <= 1000

A[i] <= 1000



Input Format
First and only argument is the vector of vector A defining the given triangle



Output Format
Return the minimum sum



Example Input
Input 1:

 
A = [ 
         [2],
        [3, 4],
       [6, 5, 7],
      [4, 1, 8, 3]
    ]
Input 2:

 A = [ [1] ]


Example Output
Output 1:

 11
Output 2:

 1


Example Explanation
Explanation 1:

 The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).
Explanation 2:

 Only 2 can be collected.


Solution ->

    public int sastaPath(int row, int col,ArrayList<ArrayList<Integer>> q, int[][]dp){
        if(row == q.size()){
            return 0;
        }
        if(dp[row][col] != 0){
            return dp[row][col];
        }
        int ans = 0;
        ans += Math.min(sastaPath(row+1,col+1,q,dp),sastaPath(row+1,col,q,dp));
        ans += q.get(row).get(col);
        return  dp[row][col] = ans;
    }
	public int minimumTotal(ArrayList<ArrayList<Integer>> a) {
        int dp[][] = new int[a.size()][];
        for(int i = 0 ; i < a.size() ; i++){
            ArrayList<Integer> list = a.get(i);
            dp[i] = new int[list.size()];
        }
        
        return sastaPath(0,0,a,dp);
	}

    
---------------------------------------------------------------------------------------------------------

Q4. Dungeon Princess

Problem Description
The demons had captured the princess and imprisoned her in the bottom-right corner of a dungeon. The dungeon consists of M x N rooms laid out in a 2D grid. Our valiant knight was initially positioned in the top-left room and must fight his way through the dungeon to rescue the princess.

The knight has an initial health point represented by a positive integer. If at any point his health point drops to 0 or below, he dies immediately.

Some of the rooms are guarded by demons, so the knight loses health (negative integers) upon entering these rooms; other rooms are either empty (0's) or contain magic orbs that increase the knight's health (positive integers).

In order to reach the princess as quickly as possible, the knight decides to move only rightward or downward in each step.

Given a 2D array of integers A of size M x N. Find and return the knight's minimum initial health so that he is able to rescue the princess.



Problem Constraints
1 <= M, N <= 500

-100 <= A[i] <= 100



Input Format
First and only argument is a 2D integer array A denoting the grid of size M x N.



Output Format
Return an integer denoting the knight's minimum initial health so that he is able to rescue the princess.



Example Input
Input 1:

 A = [ 
       [-2, -3, 3],
       [-5, -10, 1],
       [10, 30, -5]
     ]
Input 2:

 A = [ 
       [1, -1, 0],
       [-1, 1, -1],
       [1, 0, -1]
     ]


Example Output
Output 1:

 7
Output 2:

 1


Example Explanation
Explanation 1:

 Initially knight is at A[0][0].
 If he takes the path RIGHT -> RIGHT -> DOWN -> DOWN, the minimum health required will be 7.
 At (0,0) he looses 2 health, so health becomes 5.
 At (0,1) he looses 3 health, so health becomes 2.
 At (0,2) he gains 3 health, so health becomes 5.
 At (1,2) he gains 1 health, so health becomes 6.
 At (2,2) he looses 5 health, so health becomes 1.
 At any point, the health point doesn't drop to 0 or below. So he can rescue the princess with minimum health 7.
 
Explanation 2:

 Take the path DOWN -> DOWN ->RIGHT -> RIGHT, the minimum health required will be 1.


Solution ->

    public int calculateMinimumHP(int[][] A) {
    int row = A.length;
    int col = A[0].length;
    int dp[][] = new int[row+1][col+1];
    for(int i = 0 ; i < dp.length ; i++){
        for(int j = 0 ; j < dp[0].length ; j++){
            dp[i][j] = Integer.MAX_VALUE;
        }
    }
    dp[row][col-1] = 1;
    dp[row-1][col] = 1;

    for(int i=row-1; i>=0; i--)
        for(int j=col-1; j>=0; j--)
            dp[i][j] = Math.max(1, Math.min(dp[i+1][j], dp[i][j+1]) - A[i][j]);
   
    return dp[0][0];
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


