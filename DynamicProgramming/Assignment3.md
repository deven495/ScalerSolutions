Q1. 0-1 Knapsack

Problem Description
Given two integer arrays A and B of size N each which represent values and weights associated with N items respectively.

Also given an integer C which represents knapsack capacity.

Find out the maximum value subset of A such that sum of the weights of this subset is smaller than or equal to C.

NOTE:

You cannot break an item, either pick the complete item, or don’t pick it (0-1 property).


Problem Constraints
1 <= N <= 103

1 <= C <= 103

1 <= A[i], B[i] <= 103



Input Format
First argument is an integer array A of size N denoting the values on N items.

Second argument is an integer array B of size N denoting the weights on N items.

Third argument is an integer C denoting the knapsack capacity.



Output Format
Return a single integer denoting the maximum value subset of A such that sum of the weights of this subset is smaller than or equal to C.



Example Input
Input 1:

 A = [60, 100, 120]
 B = [10, 20, 30]
 C = 50
Input 2:

 A = [10, 20, 30, 40]
 B = [12, 13, 15, 19]
 C = 10


Example Output
Output 1:

 220
Output 2:

 0


Example Explanation
Explanation 1:

 Taking items with weight 20 and 30 will give us the maximum value i.e 100 + 120 = 220
Explanation 2:

 Knapsack capacity is 10 but each item has weight greater than 10 so no items can be considered in the knapsack therefore answer is 0.


Solution ->

    public int knapSackBU(int wt[], int[]price,int cap){
        int n = wt.length;
        int dp[][] = new int[n+1][cap+1];

        for(int row = n-1 ; row >= 0 ; row--){
            for(int col = 1 ; col <= cap ; col++){
                int e = dp[row+1][col];
                int i = 0;
                if(col >= wt[row]){
                    i = dp[row+1][col-wt[row]] + price[row];
                }
                dp[row][col] = Math.max(e,i);
            }
        }
        return dp[0][cap];
    }
    public int solve(int[] A, int[] B, int C) {
        return knapSackBU(B,A,C);
    }

    
---------------------------------------------------------------------------------------------------------
Q2. Unbounded Knapsack

Problem Description
Given a knapsack weight A and a set of items with certain value B[i] and weight C[i], we need to calculate maximum amount that could fit in this quantity.

This is different from classical Knapsack problem, here we are allowed to use unlimited number of instances of an item.



Problem Constraints
1 <= A <= 1000

1 <= |B| <= 1000

1 <= B[i] <= 1000

1 <= C[i] <= 1000



Input Format
First argument is the Weight of knapsack A

Second argument is the vector of values B

Third argument is the vector of weights C



Output Format
Return the maximum value that fills the knapsack completely



Example Input
Input 1:

A = 10
B = [5]
C = [10]
Input 2:

A = 10
B = [6, 7]
C = [5, 5]


Example Output
Output 1:

 5
Output 2:

14


Example Explanation
Explanation 1:

Only valid possibility is to take the given item.
Explanation 2:

Take the second item twice.


Solution ->

    public int knapSackBU(int wt[], int[]price,int cap){
        int n = wt.length;
        int dp[][] = new int[n+1][cap+1];

        for(int row = n-1 ; row >= 0 ; row--){
            for(int col = 1 ; col <= cap ; col++){
                int e = dp[row+1][col];
                int i = 0;
                if(col >= wt[row]){
                    i = dp[row][col-wt[row]] + price[row];
                }
                dp[row][col] = Math.max(e,i);
            }
        }
        return dp[0][cap];
    }
    public int solve(int A, int[] B, int[] C) {
        return knapSackBU(C,B,A);
    }

    
---------------------------------------------------------------------------------------------------------

Q3. Flip Array

Problem Description

Given an array A of positive elements, you have to flip the sign of some of its elements such that the resultant sum of the elements of array should be minimum non-negative(as close to zero as possible).

Return the minimum number of elements whose sign needs to be flipped such that the resultant sum is minimum non-negative.



Problem Constraints

1 <= length of(A) <= 100

Sum of all the elements will not exceed 10,000.



Input Format

First and only argument is an integer array A.



Output Format

Return an integer denoting the minimum number of elements whose sign needs to be flipped.



Example Input

Input 1:

 A = [15, 10, 6]
Input 2:

 A = [14, 10, 4]


Example Output

Output 1:

 1
Output 2:

 1


Example Explanation

Explanation 1:

 Here, we will flip the sign of 15 and the resultant sum will be 1.
Explanation 2:

 Here, we will flip the sign of 14 and the resultant sum will be 0.
 Note that flipping the sign of 10 and 4 also gives the resultant sum 0 but flippings there sign are not minimum.


Solution ->

    public int solve(final int[] A) {
        int sum = Arrays.stream(A).sum();
        int capacity = sum/2;
        int n = A.length;
        int dp[] = new int[capacity+1];
        Arrays.fill(dp,Integer.MAX_VALUE);
        dp[0] = 0;
        for(int i = 0 ; i < A.length ; i++){
            for(int j = capacity ; j >= A[i] ; j--){
                if(dp[j-A[i]] != Integer.MAX_VALUE){
                    dp[j] = Math.min(dp[j],dp[j-A[i]]+1);
                }
            }
        }
        int k = dp.length-1;
        while(dp[k] == Integer.MAX_VALUE){
            k--;
        }
        return dp[k];
    }
    
---------------------------------------------------------------------------------------------------------

Q4. Fractional Knapsack

Problem Description
Given two integer arrays A and B of size N each which represent values and weights associated with N items respectively.

Also given an integer C which represents knapsack capacity.

Find out the maximum total value that we can fit in the knapsack. If the maximum total value is ans, then return ⌊ans × 100⌋ , i.e., floor of (ans × 100).

NOTE:

You can break an item for maximizing the total value of the knapsack


Problem Constraints
1 <= N <= 105

1 <= A[i], B[i] <= 103

1 <= C <= 103



Input Format
First argument is an integer array A of size N denoting the values on N items.

Second argument is an integer array B of size N denoting the weights on N items.

Third argument is an integer C denoting the knapsack capacity.



Output Format
Return a single integer denoting the maximum total value of A such that sum of the weights of this subset is smaller than or equal to C.



Example Input
Input 1:

 A = [60, 100, 120]
 B = [10, 20, 30]
 C = 50
Input 2:

 A = [10, 20, 30, 40]
 B = [12, 13, 15, 19]
 C = 10


Example Output
Output 1:

 24000
Output 2:

 2105


Example Explanation
Explanation 1:

Taking the full items with weight 10 and 20 and 2/3 of the item with weight 30 will give us 
the maximum value i.e 60 + 100 + 80 = 240. So we return 24000.
Explanation 2:

Taking 10/19 the fourth item gives us the maximum value i.e. 21.0526. So we return 2105.


Solution ->

    // Item value class
    class pair {
        int value, weight;
        // Item value function
        public pair(int val, int wt){
            this.weight = wt;
            this.value = val;
        }
    }
    // Function to get maximum value
    double getMaxValue(pair[] arr,int capacity){
        // Sorting items by value/weight ratio;
        Arrays.sort(arr, new Comparator<pair>() {
            @Override
            public int compare(pair item1,
                               pair item2)
            {
                double cpr1
                    = new Double((double)item1.value
                                 / (double)item1.weight);
                double cpr2
                    = new Double((double)item2.value
                                 / (double)item2.weight);
 
                if (cpr1 < cpr2)
                    return 1;
                else
                    return -1;
            }
        });
        double totalValue = 0d;
        for (pair i : arr) {
            int curWt = (int)i.weight;
            int curVal = (int)i.value;
            if (capacity - curWt >= 0) {
                // this weight can be picked while
                capacity = capacity - curWt;
                totalValue += curVal;
            } else {
                // Item cant be picked whole
                double fraction = ((double) capacity / (double)curWt);
                totalValue += (curVal * fraction);
                capacity = (int)(capacity - (curWt * fraction));
                break;
            }
        }
        // System.out.print(totalValue);
        return totalValue*100;
    }
    public int solve(int[] A, int[] B, int C) {
        pair one[] = new pair[A.length];
        int ind = 0;
        for(int i : A){
            one[ind] = new pair(A[ind],B[ind]);
            ind++;
        }

        return (int) getMaxValue(one,C);
    }
    
---------------------------------------------------------------------------------------------------------

Q1. Buying Candies

Problem Description
Rishik likes candies a lot. So, he went to a candy-shop to buy candies.

The shopkeeper showed him N packets each containg A[i] candies for cost of C[i] nibbles, each candy in that packet has a sweetness B[i]. The shopkeeper puts the condition that Rishik can buy as many complete candy-packets as he wants but he can't buy a part of the packet.

Rishik has D nibbles, can you tell him the maximum amount of sweetness he can get from candy-packets he will buy?


Problem Constraints
1 <= N <= 700

1 <= A[i] <= 1000

1 <= B[i] <= 1000

1 <= C[i],D <= 1000



Input Format
First argument of input is an integer array A
Second argument of input is an integer array B
Third argument of input is an integer array C
Fourth argument of input is an integer D


Output Format
Return a single integer denoting maximum sweetness of the candies that he can buy


Example Input
Input 1:

 A = [1, 2, 3]
 B = [2, 2, 10]
 C = [2, 3, 9]
 D = 8
Input 2:

 A = [2]
 B = [5]
 C = [10]
 D = 99


Example Output
Output 1:

 10
Output 2:

 90


Example Explanation
Explanation 1:

 Choose 1 Packet of kind 1 = 1 Candy of 2 Sweetness = 2 Sweetness
 Choose 2 Packet of kind 2 = 2 Candy of 2 Sweetness = 8 Sweetness
Explanation 2:

 Buy 9 Packet of kind 1. 18 Candy each of 5 Sweetness = 90 Sweetness


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


