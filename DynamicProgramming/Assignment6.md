Q1. Russian Doll Envelopes

Problem Description
Given a matrix of integers A of size N x 2 describing dimensions of N envelopes, where A[i][0] denotes the height of the ith envelope and A[i][1] denotes the width of the ith envelope.

One envelope can fit into another if and only if both the width and height of one envelope is greater than the width and height of the other envelope.

Find the maximum number of envelopes you can put one inside other.



Problem Constraints
1 <= N <= 1000
1 <= A[i][0], A[i][1] <= 109



Input Format
The only argument given is the integer matrix A.



Output Format
Return an integer denoting the maximum number of envelopes you can put one inside other.



Example Input
Input 1:

 A = [ 
         [5, 4]
         [6, 4]
         [6, 7]
         [2, 3]  
     ]
Input 2:

 A = [     '
         [8, 9]
         [8, 18]    
     ]


Example Output
Output 1:

 3
Output 2:

 1


Example Explanation
Explanation 1:

 Step 1: put [2, 3] inside [5, 4]
 Step 2: put [5, 4] inside [6, 7]
 3 envelopes can be put one inside other.
Explanation 2:

 No envelopes can be put inside any other so answer is 1.


Solution ->

public int maxEnvelopes(int[][] envelopes) {
    if(envelopes == null || envelopes.length == 0 
       || envelopes[0] == null || envelopes[0].length != 2)
        return 0;
    Arrays.sort(envelopes, new Comparator<int[]>(){
        public int compare(int[] arr1, int[] arr2){
            if(arr1[0] == arr2[0])
                return arr2[1] - arr1[1];
            else
                return arr1[0] - arr2[0];
       } 
    });
    int dp[] = new int[envelopes.length];
    int len = 0;
    for(int[] envelope : envelopes){
        int index = Arrays.binarySearch(dp, 0, len, envelope[1]);
        if(index < 0)
            index = -(index + 1);
        dp[index] = envelope[1];
        if(index == len)
            len++;
    }
    return len;
}

    
---------------------------------------------------------------------------------------------------------
Q2. Longest Increasing Subsequence

Problem Description
Find the longest increasing subsequence of a given array of integers, A.

In other words, find a subsequence of array in which the subsequence's elements are in strictly increasing order, and in which the subsequence is as long as possible.

In this case, return the length of the longest increasing subsequence.



Problem Constraints
1 <= length(A) <= 2500
0 <= A[i] <= 2500



Input Format
The first and the only argument is an integer array A.



Output Format
Return an integer representing the length of the longest increasing subsequence.



Example Input
Input 1:

 A = [1, 2, 1, 5]
Input 2:

 A = [0, 8, 4, 12, 2, 10, 6, 14, 1, 9, 5, 13, 3, 11, 7, 15]


Example Output
Output 1:

 3
Output 2:

 6


Example Explanation
Explanation 1:

 The longest increasing subsequence: [1, 2, 5]
Explanation 2:

 The possible longest increasing subsequences: [0, 2, 6, 9, 13, 15] or [0, 4, 6, 9, 11, 15] or [0, 4, 6, 9, 13, 15]


Solution ->

public int LIS(int[] liss) {
    if(liss == null || liss.length == 0){
        return 0;
    }
    int dp[] = new int[liss.length];
    int len = 0;
    for(int i = 0 ; i < liss.length ; i++){
        int index = Arrays.binarySearch(dp, 0, len, liss[i]);
        if(index < 0)
            index = -(index + 1);
        dp[index] = liss[i];
        if(index == len)
            len++;
    }
    return len;
}

    
---------------------------------------------------------------------------------------------------------

Q-> 


Solution ->

    
---------------------------------------------------------------------------------------------------------

Q-> 


Solution ->

    
---------------------------------------------------------------------------------------------------------

Q5. Matrix Chain Multiplication

Problem Description
Given an array of integers A representing chain of 2-D matices such that the dimensions of ith matrix is A[i-1] x A[i].

Find the most efficient way to multiply these matrices together. The problem is not actually to perform the multiplications, but merely to decide in which order to perform the multiplications.

Return the minimum number of multiplications needed to multiply the chain.



Problem Constraints
1 <= length of the array <= 1000
1 <= A[i] <= 100



Input Format
The only argument given is the integer array A.



Output Format
Return an integer denoting the minimum number of multiplications needed to multiply the chain.



Example Input
Input 1:

 A = [40, 20, 30, 10, 30]
Input 2:

 A = [10, 20, 30]


Example Output
Output 1:

 26000
Output 2:

 6000


Example Explanation
Explanation 1:

 Dimensions of A1 = 40 x 20
 Dimensions of A2 = 20 x 30
 Dimensions of A3 = 30 x 10
 Dimensions of A4 = 10 x 30
 First, multiply A2 and A3 ,cost = 20*30*10 = 6000
 Second, multilpy A1 and (Matrix obtained after multilying A2 and A3) =  40 * 20 * 10 = 8000
 Third, multiply (Matrix obtained after multiplying A1, A2 and A3) and A4 =  40 * 10 * 30 = 12000
 Total Cost = 12000 + 8000 + 6000 =26000
Explanation 2:

 Cost to multiply two matrices with dimensions 10 x 20 and 20 x 30 = 10 * 20 * 30 = 6000.


Solution ->

    public static int matrixMultiWaysBU(int arr[]) {
        int n = arr.length;

        int dp[][] = new int[n][n];

        for (int slide = 1; slide < n; slide++) {
            for (int si = 0; si < n - slide; si++) {
                int ei = si + slide;
                if (ei == si + 1) {
                    dp[si][ei] = 0;
                } else {
                    int min = Integer.MAX_VALUE;
                    for (int k = si + 1; k < ei; k++) {
                        int fp = dp[si][k];
                        int sp = dp[k][ei];
                        int togetherPair = arr[si] * arr[k] * arr[ei];
                        int totalPair = fp + sp + togetherPair;
                        if (totalPair < min) {
                            min = totalPair;
                        }
                    }
                    dp[si][ei] = min;
                }

            }
        }
        return dp[0][n - 1];
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


