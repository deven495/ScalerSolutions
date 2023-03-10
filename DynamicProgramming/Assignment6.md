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

Q3. Palindrome Partitioning II

Problem Description
Given a string A, partition A such that every substring of the partition is a palindrome.

Return the minimum cuts needed for a palindrome partitioning of A.



Problem Constraints
1 <= length(A) <= 501



Input Format
The first and the only argument contains the string A.



Output Format
Return an integer, representing the minimum cuts needed.



Example Input
Input 1:

 A = "aba"
Input 2:

 A = "aab"


Example Output
Output 1:

 0
Output 2:

 1


Example Explanation
Explanation 1:

 "aba" is already a palindrome, so no cuts are needed.
Explanation 2:

 Return 1 since the palindrome partitioning ["aa","b"] could be produced using 1 cut.


Solution ->

    public static boolean[][] palli(String str) {
        boolean[][] palliChachu = new boolean[str.length()][str.length()];
        for (boolean[] x : palliChachu) {
            Arrays.fill(x, true);
        }
        for (int row = str.length() - 2; row >= 0; row--) {
            for (int col = row + 1; col < str.length(); col++) {
                if (str.charAt(row) == str.charAt(col)) {
                    palliChachu[row][col] = palliChachu[row + 1][col - 1];
                } else {
                    palliChachu[row][col] = false;
                }
            }
        }
        return palliChachu;
    }
    public static int partyBU(String str) {
        int dp[][] = new int[str.length()][str.length()];
        boolean[][] palliChachu = palli(str);
        for (int k = 0; k <= str.length() - 1; k++) {
            for (int si = 0; si <= str.length() - k - 1; si++) {
                int ei = si + k;
                if (palliChachu[si][ei]) {
                    dp[si][ei] = 0;
                } else {
                    int min = Integer.MAX_VALUE;
                    for (int i = si; i < ei; i++) {
                        int fp = dp[si][i];
                        int bp = dp[i + 1][ei];
                        min = Math.min(min, fp + bp + 1);
                    }
                    dp[si][ei] = min;
                }
            }
        }
        return dp[0][str.length() - 1];
    }

    
---------------------------------------------------------------------------------------------------------

Q4. Palindromic Substrings Count

Given a string A consisting of lowercase English alphabets. Your task is to find how many substrings of A are palindrome.

The substrings with different start indexes or end indexes are counted as different substrings even if they consist of same characters.

Return the count of palindromic substrings.

Note: A string is palindrome if it reads the same from backward and forward.


Input Format

The only argument given is string A.
Output Format

Return the count of palindromic substrings.
Constraints

1 <= length of the array <= 1000
For Example

Input 1:
    A = "abab"
Output 1:
    6
Explanation 1:
    6 palindromic substrings are:
    "a", "aba", "b", "bab", "a" and "b".

Input 2:
    A = "ababa"
Output 2:
    9
Explanation 9:
    9 palindromic substrings are:
    "a", "a", "a", "b", "b" , "aba" ,"bab", "aba" and "ababa".


Solution ->

    public int PaliCount(String q){
        boolean dp[][] = new boolean[q.length()][q.length()];
        int ans = 0;
        for(int k = 0 ; k < q.length() ; k++){
            for(int si = 0 ; si < q.length()-k ; si++){
                int ei = si + k;
                if(si == ei){
                    dp[si][ei] = true;
                    ans++;
                }else{
                    if(q.charAt(si) != q.charAt(ei)){
                        dp[si][ei] = false;
                    }else{
                        if(si + 1 > ei - 1 || dp[si+1][ei-1] == true){
                            dp[si][ei] = true;
                            ans++;
                        }else{
                            dp[si][ei] = false;
                        }
                    }
                }
            }
        }
        return ans;
    }

    
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

Q6. Word Break

Given a string A and a dictionary of words B, determine if A can be segmented into a space-separated sequence of one or more dictionary words.

Input Format:

The first argument is a string, A.
The second argument is an array of strings, B.
Output Format:

Return 0 / 1 ( 0 for false, 1 for true ) for this problem.
Constraints:

1 <= len(A) <= 6500
1 <= len(B) <= 10000
1 <= len(B[i]) <= 20
Examples:

Input 1:
    A = "myinterviewtrainer",
    B = ["trainer", "my", "interview"]

Output 1:
    1

Explanation 1:
    Return 1 ( corresponding to true ) because "myinterviewtrainer" can be segmented as "my interview trainer".

Input 2:
    A = "a"
    B = ["aaa"]

Output 2:
    0

Explanation 2:
    Return 0 ( corresponding to false ) because "a" cannot be segmented as "aaa".


Solution ->

    public int breaks(int idx , String A, HashSet<String> set , int dp[]){
        if(idx == A.length()) return 1;

        String temp = "";
        if(dp[idx] != -1) return dp[idx];
        for(int i = idx ; i < A.length() ; i++){
            temp += A.charAt(i);
            if(set.contains(temp)){
                if(breaks(i+1,A,set,dp) == 1) return dp[idx] = 1;
            }
        }
        return dp[idx] = 0;
    }
    public int wordBreak(String A, String[] B) {
        int dp[] = new int[A.length()+1];
        for(int x : dp){
            Arrays.fill(dp,-1);
        }
        HashSet<String> set = new HashSet<>();
        for(String x : B){
            set.add(x);
        }
        return breaks(0,A,set,dp);
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


