Q1. Longest Common Subsequence

Problem Description
Given two strings A and B. Find the longest common subsequence ( A sequence which does not need to be contiguous), which is common in both the strings.

You need to return the length of such longest common subsequence.



Problem Constraints
1 <= Length of A, B <= 1005



Input Format
First argument is a string A.
Second argument is a string B.



Output Format
Return an integer denoting the length of the longest common subsequence.



Example Input
Input 1:

 A = "abbcdgf"
 B = "bbadcgf"
Input 2:

 A = "aaaaaa"
 B = "ababab"


Example Output
Output 1:

 5
Output 2:

 3


Example Explanation
Explanation 1:

 The longest common subsequence is "bbcgf", which has a length of 5.
Explanation 2:

 The longest common subsequence is "aaa", which has a length of 3.


Solution ->

    public int LCSBottomUp(String s1, String s2) {
        int dp[][] = new int[s1.length() + 1][s2.length() + 1];

        for (int i = s1.length() - 1; i >= 0; i--) {
            for (int j = s2.length() - 1; j >= 0; j--) {
                if (s1.charAt(i) == s2.charAt(j)) {
                    dp[i][j] = dp[i + 1][j + 1] + 1;
                } else {
                    int op1 = dp[i + 1][j];
                    int op2 = dp[i][j + 1];
                    dp[i][j] = Math.max(op1, op2);
                }
            }
        }
        return dp[0][0];
    }

    
---------------------------------------------------------------------------------------------------------
Q2. Edit Distance

Problem Description
Given two strings A and B, find the minimum number of steps required to convert A to B. (each operation is counted as 1 step.)

You have the following 3 operations permitted on a word:

Insert a character
Delete a character
Replace a character


Problem Constraints
1 <= length(A), length(B) <= 450



Input Format
The first argument of input contains a string, A.
The second argument of input contains a string, B.



Output Format
Return an integer, representing the minimum number of steps required.



Example Input
Input 1:

 A = "abad"
 B = "abac"
Input 2:

 A = "Anshuman"
 B = "Antihuman


Example Output
Output 1:

 1
Output 2:

 2


Example Explanation
Exlanation 1:

 A = "abad" and B = "abac"
 After applying operation: Replace d with c. We get A = B.
 
Explanation 2:

 A = "Anshuman" and B = "Antihuman"
 After applying operations: Replace s with t and insert i before h. We get A = B.


Solution ->

    public static int s2Stringtos1BU(String s1, String s2) {

        int dp[][] = new int[s1.length() + 1][s2.length() + 1];
        for (int i = dp.length - 1; i >= 0; i--) {
            for (int j = dp[i].length - 1; j >= 0; j--) {
                if (i == dp.length - 1) {
                    dp[i][j] = s2.length() - j;
                } else if (j == dp[i].length - 1) {
                    dp[i][j] = s1.length() - i;
                } else {
                    char c1 = s1.charAt(i);
                    char c2 = s2.charAt(j);
                    if (c1 == c2) {
                        dp[i][j] = dp[i + 1][j + 1];
                    } else {
                        int op1 = dp[i][j + 1];
                        int op2 = dp[i + 1][j];
                        int op3 = dp[i + 1][j + 1];

                        dp[i][j] = Math.min(op1, Math.min(op2, op3)) + 1;
                    }
                }
            }
        }
        return dp[0][0];
    }

    
---------------------------------------------------------------------------------------------------------

Q3. Regular Expression Match

Problem Description
Implement wildcard pattern matching with support for ' ? ' and ' * ' for strings A and B.

' ? ' : Matches any single character.
' * ' : Matches any sequence of characters (including the empty sequence).
The matching should cover the entire input string (not partial).



Problem Constraints
1 <= length(A), length(B) <= 104



Input Format
The first argument of input contains a string A.
The second argument of input contains a string B.



Output Format
Return 1 if the patterns match else return 0.



Example Input
Input 1:

 A = "aaa"
 B = "a*"
Input 2:

 A = "acz"
 B = "a?a"


Example Output
Output 1:

 1
Output 2:

 0


Example Explanation
Explanation 1:

 Since '*' matches any sequence of characters. Last two 'a' in string A will be match by '*'.
 So, the pattern matches we return 1.
Explanation 2:

 '?' matches any single character. First two character in string A will be match. 
 But the last character i.e 'z' != 'a'. Return 0.


Solution ->

    public boolean patterMatching(String src, String pat){
        boolean dp[][] = new boolean[src.length()+1][pat.length()+1];
        dp[src.length()][pat.length()] = true;
        for(int i = pat.length()-1 ; i >= 0  ; i--){
            if(pat.charAt(i) == '*'){
                dp[dp.length-1][i] = dp[dp.length-1][i+1];
            }else{
                dp[dp.length-1][i] = false;
            }
        }

        for(int row = dp.length - 2 ; row >= 0 ; row--){
            for(int col = dp[row].length-2 ; col >= 0 ; col--){
                char srcChar = src.charAt(row);
                char patChar = pat.charAt(col);
                boolean ans;
                if(srcChar == patChar || patChar == '?'){
                    ans = dp[row+1][col+1];
                }else if(patChar == '*'){
                    boolean withBlack = dp[row][col+1];
                    boolean withMulti = dp[row+1][col];
                    ans = withBlack || withMulti;
                }else{
                    ans = false;
                }
                dp[row][col] = ans;
            }
        }
        return dp[0][0];
    }

    
---------------------------------------------------------------------------------------------------------

Q4. Distinct Subsequences

Problem Description
Given two sequences A and B, count number of unique ways in sequence A, to form a subsequence that is identical to the sequence B.

Subsequence : A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, "ACE" is a subsequence of "ABCDE" while "AEC" is not).



Problem Constraints
1 <= length(A), length(B) <= 700



Input Format
The first argument of input contains a string A.
The second argument of input contains a string B.



Output Format
Return an integer representing the answer as described in the problem statement.



Example Input
Input 1:

 A = "abc"
 B = "abc"
Input 2:

 A = "rabbbit" 
 B = "rabbit" 


Example Output
Output 1:

 1
Output 2:

 3


Example Explanation
Explanation 1:

 Both the strings are equal.
Explanation 2:

 These are the possible removals of characters:
    => A = "ra_bbit" 
    => A = "rab_bit" 
    => A = "rabb_it"

 Note: "_" marks the removed character.


Solution ->

    public int ways(String str1 , String str2, int i , int j,int dp[][]){
        if(j == str2.length()){
            return 1;
        }
        if(i == str1.length()){
            return 0;
        }
        if(dp[i][j] != -1){
            return dp[i][j];
        }
        int ans = 0;
        if(str1.charAt(i) != str2.charAt(j)){
            ans = ways(str1,str2,i+1,j,dp);
        }else{
            int op1 = ways(str1,str2,i+1,j,dp);
            int op2 = ways(str1,str2,i+1,j+1,dp);

            ans = op1+op2;
        }
        return dp[i][j] = ans;
    }
    public int numDistinct(String A, String B) {
        int dp[][] = new int[A.length()+1][B.length()+1];
        for(int[]x : dp){
            Arrays.fill(x,-1);
        }
        return ways(A,B,0,0,dp);
    }

    
---------------------------------------------------------------------------------------------------------

Q5. Longest Palindromic Subsequence

Problem Description
Given a string A. Find the longest palindromic subsequence (A subsequence which does not need to be contiguous and is a palindrome).

You need to return the length of longest palindromic subsequence.



Problem Constraints
1 <= length of(A) <= 103



Input Format
First and only integer is a string A.



Output Format
Return an integer denoting the length of longest palindromic subsequence.



Example Input
Input 1:

 A = "bebeeed"
Input 2:

 A = "aedsead"


Example Output
Output 1:

 4
Output 2:

 5


Example Explanation
Explanation 1:

 The longest palindromic subsequence is "eeee", which has a length of 4.
Explanation 2:

 The longest palindromic subsequence is "aedea", which has a length of 5.


Solution ->

    public static int LPSBU(String str) {
        int n = str.length();
        int dp[][] = new int[n][n];

        for (int slide = 0; slide < n; slide++) {
            for (int si = 0; si < n - slide; si++) {
                int ei = si + slide;
                if (si == ei) {
                    dp[si][ei] = 1;
                }else{
                int ans = 0;
                if (str.charAt(si) == str.charAt(ei)) {
                    ans = dp[si + 1][ei - 1] + 2;
                } else {
                    int op1 = dp[si + 1][ei];
                    int op2 = dp[si][ei - 1];
                    ans = Math.max(op1, op2);
                }
                dp[si][ei] = ans;
                }

            }
        }
        return dp[0][n - 1];
    }

    
---------------------------------------------------------------------------------------------------------

H.W Q1. Longest Palindromic Substring

Problem Description
Given a string A of size N, find and return the longest palindromic substring in A.

Substring of string A is A[i...j] where 0 <= i <= j < len(A)

Palindrome string:
A string which reads the same backwards. More formally, A is palindrome if reverse(A) = A.

Incase of conflict, return the substring which occurs first ( with the least starting index).



Problem Constraints
1 <= N <= 6000



Input Format
First and only argument is a string A.



Output Format
Return a string denoting the longest palindromic substring of string A.



Example Input
A = "aaaabaaa"


Example Output
"aaabaaa"


Example Explanation
We can see that longest palindromic substring is of length 7 and the string is "aaabaaa".


Solution ->

    public String longestPalindrome(String A) {
        String maxString="";
        String oddLen=""; // storing substring when string length is odd;
        String evenLen=""; // storing substring when string length is even;
        for(int i=0; i<A.length(); i++){
            oddLen=checkPalindrome(A,i,i);
            if(oddLen.length() >maxString.length()){
                maxString=oddLen;
            }
            evenLen=checkPalindrome(A,i,i+1);
            if(evenLen.length()>maxString.length()){
                maxString=evenLen;
            }
        }
        return maxString;
    }
    public String checkPalindrome(String s,int p1,int p2){
        while(p1>=0 && p2<s.length() && s.charAt(p1)==s.charAt(p2)){
            p1--;
            p2++;
        }
        return s.substring(p1+1,p2); // it is going one further step thats why p1+1, p2 is excluding in substring(basic knowledge of substring).
    }

    
---------------------------------------------------------------------------------------------------------

Q2. Regular Expression II

Problem Description
Implement wildcard pattern matching with support for ' ? ' and ' * ' for strings A and B.

' . ' : Matches any single character.
' * ' : Matches zero or more of the preceding element.
The matching should cover the entire input string (not partial).



Problem Constraints
1 <= length(A), length(B) <= 104



Input Format
The first argument of input contains a string A.
The second argument of input contains a string B denoting the pattern.



Output Format
Return 1 if the patterns match else return 0.



Example Input
Input 1:

 A = "aab"
 B = "c*a*b"
Input 2:

 A = "acz"
 B = "a.a"


Example Output
Output 1:

 1
Output 2:

 0


Example Explanation
Explanation 1:

 'c' can be repeated 0 times, 'a' can be repeated 1 time. Therefore, it matches "aab".
 So, return 1.
Explanation 2:

 '.' matches any single character. First two character in string A will be match. 
 But the last character i.e 'z' != 'a'. Return 0.


Solution ->

    public int isMatch(final String A, final String B) {
        return helper(A, B, A.length(), B.length()) ? 1 : 0;
    }

    public boolean helper(String A, String B, int N, int M) {
        if (N==0 && M==0) { //1}
            return true;
        }
        if (M==0) { //2}
            return false;
        }
        if (N <= 0) { //3}
            for (int i = M-1; i >= 0; i -= 2) {
                if (B.charAt(i) != '*') {
                    return false;
                }
            }
            return true;
        }

        if (B.charAt(M-1) == '.') { //4}
            return helper(A, B, N-1, M-1);
        }
        else if (B.charAt(M-1) == '*') {    //5}
            if (B.charAt(M-2) == A.charAt(N-1) || B.charAt(M-2) == '.') {
                return helper(A, B, N, M-2) || helper(A, B, N-1, M);
            }
            else {
                return helper(A, B, N, M-2);
            }
        }
        else {  //6}
            if (A.charAt(N-1) != B.charAt(M-1)) {
                return false;
            }
            else {
                return helper(A, B, N-1, M-1);
            }
        }
    }

    
---------------------------------------------------------------------------------------------------------

Q4. Repeating Subsequence

Problem Description
Given a string A, find if there is any subsequence that repeats itself.

A subsequence of a string is defined as a sequence of characters generated by deleting some characters in the string without changing the order of the remaining characters.

NOTE:
1. Subsequence length should be greater than or equal to 2.
2. The repeating subsequence should be disjoint that is in both the sequence no character in the same order and position should be taken from the same index of the original string.



Problem Constraints
1 <= length(A) <= 100



Input Format
The first and the only argument of input contains a string A.



Output Format
Return an integer, 1 if there is any subsequence which repeat itself else return 0.



Example Input
Input 1:

 A = "abab"
Input 2:

 A = "abba"


Example Output
Output 1:

 1
Output 2:

 0


Example Explanation
Explanation 1:

 "ab" is repeated.
Explanation 2:

 There is no repeating subsequence.


Solution ->

    public int LCSBottomUp(String s1, String s2) {
        int dp[][] = new int[s1.length() + 1][s2.length() + 1];

        for (int i = s1.length() - 1; i >= 0; i--) {
            for (int j = s2.length() - 1; j >= 0; j--) {
                if (s1.charAt(i) == s2.charAt(j) && i != j) {
                    dp[i][j] = dp[i + 1][j + 1] + 1;
                } else {
                    int op1 = dp[i + 1][j];
                    int op2 = dp[i][j + 1];
                    dp[i][j] = Math.max(op1, op2);
                }
            }
        }
        return dp[0][0];
    }
    public int anytwo(String A) {
        return LCSBottomUp(A,A) > 1 ? 1 : 0 ;
    }

    
---------------------------------------------------------------------------------------------------------

Q-> 


Solution ->

    
---------------------------------------------------------------------------------------------------------


