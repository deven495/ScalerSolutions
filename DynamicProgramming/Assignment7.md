
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

Q3. Box Stacking Problem

Problem Description

Given a matrix of integers A of size N x 3 representing the dimensions of N rectangular 3-D boxes, where A[i][0] represents the height of the ith box, A[i][1] represents the widht of the ith box and A[i][2] represents the length of the ith box.
You want to create a stack of boxes which is as tall as possible, but you can only stack a box on top of another box if the dimensions of the 2-D base of the lower box are each strictly larger than those of the 2-D base of the higher box. You can rotate a box so that any side functions as its base. It is also allowable to use multiple instances of the same type of box.

Find and return the maximum height of stack achievable.



Problem Constraints

1 <= N <= 1000
1 <= A[i][0], A[i][1], A[i][2] <= 1e6


Input Format

The only argument given is the integer matrix A.


Output Format

Return a single integer, the maximum height of stack achievable.


Example Input

Input 1:
A = [   [4, 6, 7]
        [1, 2, 3]
        [4, 5, 6]
        [1, 2, 3]   ]
Input 2:

A = [   [4, 5, 6]
        [10, 12, 14]    ]


Example Output

Output 1:
60
Output 2:

34


Example Explanation

Explanation 1:
Following are all rotations of the boxes in decreasing order of base area:
        10 x 12 x 32
        12 x 10 x 32
        32 x 10 x 12
        4 x 6 x 7
        4 x 5 x 6
        6 x 4 x 7
        5 x 4 x 6
        7 x 4 x 6
        6 x 4 x 5
        1 x 2 x 3
        2 x 1 x 3
        3 x 1 x 2

        The height 60 is obtained by boxes
        [ [3, 1, 2], [1, 2, 3], [6, 4, 5], [4, 5, 6], [4, 6, 7], [32, 10, 12], [10, 12, 32] ]
Explanation 2:

Similarly, the answer for this case would be 34


Solution ->

    static ArrayList<int[]> list;
    public void addOneArea(int[] x){
        if(x[0] >= x[1]){
            list.add(new int[]{x[0],x[1],x[2]});
        }
        if(x[0] >= x[2]){
            list.add(new int[]{x[0],x[2],x[1]});
        }
        if(x[1] >= x[0]){
            list.add(new int[]{x[1],x[0],x[2]});
        }
        if(x[1] >= x[2]){
            list.add(new int[]{x[1],x[2],x[0]});
        }
        if(x[2] >= x[0]){
            list.add(new int[]{x[2],x[0],x[1]});
        }
        if(x[2] >= x[1]){
            list.add(new int[]{x[2],x[1],x[0]});
        }  
    }
    public int solve(int[][] A) {
        list = new ArrayList<int[]>();
        for(int[] x : A){
            addOneArea(x);
        }
        Collections.sort(list, new Comparator<int[]>() {
            public int compare(int a[], int[] b) {
                return (1l)*a[0] * a[1] - b[0]* (1l)* b[1] > 0 ? -1 : 1;
            }
        });

        int dp[] = new int[list.size()];
        int max = Integer.MIN_VALUE;
        for(int i = list.size()-1 ; i >=0  ; i--){
            dp[i] = list.get(i)[2];
            for(int j = i+1 ; j < list.size() ; j++){
                int []bde = list.get(i);
                int []chote = list.get(j);
                if(chote[0] < bde[0] && chote[1] < bde[1]){
                    dp[i] = Math.max(dp[i], dp[j] + bde[2]);
                    max = Math.max(max,dp[i]);
                }
            }
        }
        return max;
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


