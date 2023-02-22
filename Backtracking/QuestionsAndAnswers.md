BackTracking 1 - > Q1-> Problem Description
Given a set of distinct integers A, return all possible subsets.

NOTE:

Elements in a subset must be in non-descending order.
The solution set must not contain duplicate subsets.
Also, the subsets should be sorted in ascending ( lexicographic ) order.
The list is not necessarily sorted.


Problem Constraints
1 <= |A| <= 16
INTMIN <= A[i] <= INTMAX


Input Format
First and only argument of input contains a single integer array A.



Output Format
Return a vector of vectors denoting the answer.



Example Input
Input 1:

A = [1]
Input 2:

A = [1, 2, 3]


Example Output
Output 1:

[
    []
    [1]
]
Output 2:

[
 []
 [1]
 [1, 2]
 [1, 2, 3]
 [1, 3]
 [2]
 [2, 3]
 [3]
]


Example Explanation
Explanation 1:

 You can see that these are all possible subsets.
Explanation 2:

You can see that these are all possible subsets.

Solution --------------------------------------------------------------------------------------------->

 static ArrayList<ArrayList<Integer>> mainList;
    static ArrayList<Integer> temp = new ArrayList<>();

    public void allSubsets(ArrayList<Integer> q, int lastInd) {
        if (lastInd == q.size()) {
            return;
        }
        temp.add(q.get(lastInd));// adding
        mainList.add(new ArrayList<>(temp));
        allSubsets(q, lastInd + 1);// For taking the element
        temp.remove(temp.size() - 1);// removing

        allSubsets(q, lastInd + 1); // Not taking the Element

    }

    public ArrayList<ArrayList<Integer>> subsets(ArrayList<Integer> A) {
        mainList = new ArrayList<>();
        Collections.sort(A);
        mainList.add(new ArrayList<>());
        allSubsets(A, 0);
        return mainList;
    }
---------------------------------------------------------------------------------------------------------
Q2. Permutations

Problem Description
Given an integer array A of size N denoting collection of numbers , return all possible permutations.

NOTE:

No two entries in the permutation sequence should be the same.
For the purpose of this problem, assume that all the numbers in the collection are unique.
Return the answer in any order
WARNING: DO NOT USE LIBRARY FUNCTION FOR GENERATING PERMUTATIONS. 
Example : next_permutations in C++ / itertools.permutations in python.
If you do, we will disqualify your submission retroactively and give you penalty points.


Problem Constraints
1 <= N <= 9



Input Format
Only argument is an integer array A of size N.



Output Format
Return a 2-D array denoting all possible permutation of the array.



Example Input
A = [1, 2, 3]


Example Output
[ [1, 2, 3]
  [1, 3, 2]
  [2, 1, 3] 
  [2, 3, 1] 
  [3, 1, 2] 
  [3, 2, 1] ]


Example Explanation
All the possible permutation of array [1, 2, 3].

Solution->


ArrayList<ArrayList<Integer>> list;
    ArrayList<Integer> temp;
    public void permutations(boolean[] arr,ArrayList<Integer> q){
        if(temp.size() == q.size()){
            list.add(new ArrayList<>(temp));
            return;
        }
        for(int i = 0 ; i < q.size() ; i++){
            if(arr[i] == false){
                arr[i] = true;
                temp.add(q.get(i));
                permutations(arr,q);
                temp.remove(temp.size()-1);
                arr[i] = false;
            }
        }
    }
    public ArrayList<ArrayList<Integer>> permute(ArrayList<Integer> A) {
        list = new ArrayList<>();
        temp = new ArrayList<>();
        boolean arr[] = new boolean[A.size()];
        permutations(arr,A);
        return list;
    }
---------------------------------------------------------------------------------------------------------
Q3. All Unique Permutations
Problem Description
Given an array A of size N denoting collection of numbers that might contain duplicates, return all possible unique permutations.

NOTE: No 2 entries in the permutation sequence should be the same.

WARNING: DO NOT USE LIBRARY FUNCTION FOR GENERATING PERMUTATIONS. 
Example : next_permutations in C++ / itertools.permutations in python.
If you do, we will disqualify your submission retroactively and give you penalty points.


Problem Constraints
1 <= |A| <= 9

0 <= A[i] <= 10



Input Format
Only argument is an integer array A of size N.



Output Format
Return a 2-D array denoting all possible unique permutation of the array.



Example Input
Input 1:

A = [1, 1, 2]
Input 2:

A = [1, 2]


Example Output
Output 1:

[ [1,1,2]
  [1,2,1]
  [2,1,1] ]
Output 2:

[ [1, 2]
  [2, 1] ]


Example Explanation
Explanation 1:

 All the possible unique permutation of array [1, 1, 2].
Explanation 2:

 All the possible unique permutation of array [1, 2].

 Solution->
  ArrayList<ArrayList<Integer>> MainList;
    ArrayList<Integer> list;
    public void permutations(ArrayList<Integer> q ,int n, int index){
        if(index == n){
            MainList.add(new ArrayList<>(list));
        }
        for(int i = 0 ; i < q.size() ;i++){
            if(i!= q.size()-1 && (int)q.get(i) == (int)q.get(i+1)){
                continue;
            }
            list.add(q.get(i));
            q.remove(i);
            permutations(q,n,index+1);
            q.add(i,list.get(list.size()-1));
            list.remove(list.size()-1);
        }
    }
    public ArrayList<ArrayList<Integer>> permute(ArrayList<Integer> A) {
        Collections.sort(A);
        list = new ArrayList<>();
        MainList = new ArrayList<>();
        int n = A.size();
        permutations(A,n,0);
        return MainList;
    }

---------------------------------------------------------------------------------------------------------
Q4. Unique Paths III

Problem Description
Given a matrix of integers A of size N x M . There are 4 types of squares in it:

1. 1 represents the starting square.  There is exactly one starting square.
2. 2 represents the ending square.  There is exactly one ending square.
3. 0 represents empty squares we can walk over.
4. -1 represents obstacles that we cannot walk over.
Find and return the number of 4-directional walks from the starting square to the ending square, that walk over every non-obstacle square exactly once.

Note: Rows are numbered from top to bottom and columns are numbered from left to right.



Problem Constraints
2 <= N * M <= 20
-1 <= A[i] <= 2



Input Format
The first argument given is the integer matrix A.



Output Format
Return the number of 4-directional walks from the starting square to the ending square, that walk over every non-obstacle square exactly once.



Example Input
Input 1:

A = [   [1, 0, 0, 0]
        [0, 0, 0, 0]
        [0, 0, 2, -1]   ]
Input 2:

A = [   [0, 1]
        [2, 0]    ]


Example Output
Output 1:

2
Output 2:

0


Example Explanation
Explanation 1:

We have the following two paths: 
1. (0,0),(0,1),(0,2),(0,3),(1,3),(1,2),(1,1),(1,0),(2,0),(2,1),(2,2)
2. (0,0),(1,0),(2,0),(2,1),(1,1),(0,1),(0,2),(0,3),(1,3),(1,2),(2,2)
Explanation 1:

Answer is evident here.

Solution->

 public int paths(ArrayList<ArrayList<Integer>> field,boolean[][] visited,int row,int col,int zeros){
        if(row < 0 || col < 0 || row >= field.size() || col >= field.get(0).size() || visited[row][col]
        || field.get(row).get(col) == -1){
            return 0;
        }
        if(field.get(row).get(col) == 2){
            if(zeros == 0){
                return 1;
            }else{
                return 0;
            }
        }
            int totalPaths = 0;
            visited[row][col] = true;
            if(field.get(row).get(col) == 0){
                zeros--;
            }
                totalPaths += paths(field,visited,row+1,col,zeros);
                totalPaths += paths(field,visited,row,col+1,zeros);
                totalPaths += paths(field,visited,row-1,col,zeros);
                totalPaths += paths(field,visited,row,col-1,zeros);
                visited[row][col] = false;
            if(field.get(row).get(col) == 0){
                zeros++;
            }
        return totalPaths;
        
    }
    public int solve(ArrayList<ArrayList<Integer>> A) {

        boolean visited[][] = new boolean[A.size()][A.get(0).size()];
        int zeros = 0;
        int startRow = 0;
        int startCol = 0;
        for(int i = 0 ; i < A.size() ; i++){
            for(int j = 0 ; j < A.get(i).size() ; j++){
                if(A.get(i).get(j) == 0){
                    zeros++;
                }
                if(A.get(i).get(j) == 1){
                    startRow = i;
                    startCol = j;
                }
            }
        }
        return paths(A,visited,startRow,startCol,zeros);
    }

---------------------------------------------------------------------------------------------------------
HomeWork -> Q1. Number of Squareful Arrays

Problem Description
Given an array of integers A, the array is squareful if for every pair of adjacent elements, their sum is a perfect square.

Find and return the number of permutations of A that are squareful. Two permutations A1 and A2 differ if and only if there is some index i such that A1[i] != A2[i].



Problem Constraints
1 <= length of the array <= 12

1 <= A[i] <= 109



Input Format
The only argument given is the integer array A.



Output Format
Return the number of permutations of A that are squareful.



Example Input
Input 1:

 A = [2, 2, 2]
Input 2:

 A = [1, 17, 8]


Example Output
Output 1:

 1
Output 2:

 2


Example Explanation
Explanation 1:

 Only permutation is [2, 2, 2], the sum of adjacent element is 4 and 4 and both are perfect square.
Explanation 2:

 Permutation are [1, 8, 17] and [17, 8, 1].

 Solution->

   ArrayList<ArrayList<Integer>> list;
    ArrayList<Integer> temp;
    HashSet<Integer> x;
    public void permutations(ArrayList<Integer> q,int idx){
        if(temp.size() > 1){
            int sq = temp.get(temp.size()-1) + temp.get(temp.size()-2);
            if(!(Math.ceil((double)Math.sqrt(sq)) == Math.floor((double)Math.sqrt(sq)))){
                return;
            }
        }
        if(temp.size() == q.size()){
           list.add(new ArrayList<>(temp));
            return;
        }
        int y = -1;
        for(int i = 0 ; i < q.size() ; i++){
            if(!x.contains(i) &&  y != q.get(i)){
                y = q.get(i);
                temp.add(q.get(i));
                x.add(i);

                permutations(q,idx+1);
                
                temp.remove(temp.size()-1);
                x.remove(i);
            }
        }
    }
    public ArrayList<ArrayList<Integer>> permute(ArrayList<Integer> A) {
        Collections.sort(A);
        list = new ArrayList<>();
        temp = new ArrayList<>();
        x = new HashSet<>();
        permutations(A,0);
        return list;
    }
    public int solve(ArrayList<Integer> A) {
        if(A.size() == 1) return 0;
        return permute(A).size();
    }

---------------------------------------------------------------------------------------------------------
Q2. Letter Phone

Problem Description
Given a digit string A, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below.



The digit 0 maps to 0 itself. The digit 1 maps to 1 itself.

NOTE: Make sure the returned strings are lexicographically sorted.



Problem Constraints
1 <= |A| <= 10



Input Format
The only argument is a digit string A.



Output Format
Return a string array denoting the possible letter combinations.



Example Input
Input 1:

 A = "23"
Input 2:

 A = "012"


Example Output
Output 1:

 ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]
Output 2:

 ["01a", "01b", "01c"]


Example Explanation
Explanation 1:

 There are 9 possible letter combinations.
Explanation 2:

 Only 3 possible letter combinations.

 Solutions ->


  HashMap<Integer,String> charMap;
    ArrayList<String> list;
    String temp = "";
    public void allCombinations(String q, int idx){
        if(idx == q.length()){
            list.add(temp);
            return;
        }
        String str = charMap.get(Integer.parseInt("" + q.charAt(idx)));

        for(int i = 0 ; i < str.length() ; i++){
            temp += str.charAt(i);
            allCombinations(q,idx + 1);
            temp = temp.substring(0,temp.length()-1);
        }

    }
    public ArrayList<String> letterCombinations(String A) {
        charMap = new HashMap<>();
        list = new ArrayList<>();
        charMap.put(0,"0");
        charMap.put(1,"1");
        charMap.put(2,"abc");
        charMap.put(3,"def");
        charMap.put(4,"ghi");
        charMap.put(5,"jkl");
        charMap.put(6,"mno");
        charMap.put(7,"pqrs");
        charMap.put(8,"tuv");
        charMap.put(9,"wxyz");

        allCombinations(A,0);
        return list;
    }
---------------------------------------------------------------------------------------------------------
Q3. Remove Invalid Parentheses

Problem Description
Given a string A consisting of lowercase English alphabets and parentheses '(' and ')'. Remove the minimum number of invalid parentheses in order to make the input string valid.

Return all possible results.

You can return the results in any order.



Problem Constraints
1 <= length of the string <= 20



Input Format
The only argument given is string A.



Output Format
Return all possible strings after removing the minimum number of invalid parentheses.



Example Input
Input 1:

 A = "()())()"
Input 2:

 A = "(a)())()"


Example Output
Output 1:

 ["()()()", "(())()"]
Output 2:

 ["(a)()()", "(a())()"]


Example Explanation
Explanation 1:

 By removing 1 parentheses we can make the string valid.
        1. Remove the parentheses at index 4 then string becomes : "()()()"
        2. Remove the parentheses at index 2 then string becomes : "(())()"
Explanation 2:

 By removing 1 parentheses we can make the string valid.
        1. Remove the parentheses at index 5 then string becomes : "(a)()()"
        2. Remove the parentheses at index 2 then string becomes : "(a())()"

Solution->


HashMap<Integer,HashSet<String>> map;
    int ans;
    public boolean checkValid(String q){
        int left = 0;
        int right = 0;
        for(int i = 0 ; i < q.length() ; i++){
            char x = q.charAt(i);
            if(right > left){
                return false;
            }else if(x == '('){
                left++;
            }else if(x == ')'){
                right++;
            }
        }
        return left ==right ;
    }

    public void func(int i, String A, StringBuilder temp){
        if(i == A.length() && checkValid(temp.toString()) == true && temp.length() >= ans){
            if(map.containsKey(temp.length()) != false){
                map.get(temp.length()).add(temp.toString());
                
            }else{
                HashSet<String> list = new HashSet<>();
                list.add(temp.toString());
                map.put(temp.length(),list);
            }
            ans = Math.max(ans,temp.length());
            return;
        }
        if(i == A.length()){
            return;
        }
        func(i+1,A,temp);
    
        temp.append(A.charAt(i));
        func(i+1,A,temp);
        temp.deleteCharAt(temp.length()-1);
    }
    
    public ArrayList<String> solve(String A) {
        map = new HashMap<>();
        ans = 0;
        
        StringBuilder temp = new StringBuilder();
        func(0,A,temp);
        if(ans == 0) {
            ArrayList<String> z = new ArrayList<>();
            z.add("");
            return z;
        }
        ArrayList<String> list = new ArrayList<>();
        for(String x : map.get(ans)){
            list.add(x);
        }
        return list;
    }
---------------------------------------------------------------------------------------------------------
Q4. Subsets II

Problem Description
Given a collection of integers denoted by array A of size N that might contain duplicates, return all possible subsets.

NOTE:

Elements in a subset must be in non-descending order.
The solution set must not contain duplicate subsets.
The subsets must be sorted lexicographically.


Problem Constraints
0 <= N <= 16



Input Format
Only argument is an integer array A of size N.



Output Format
Return a 2-D vector denoting all the possible subsets.



Example Input
Input 1:

 A = [1, 2, 2]
Input 2:

 A = [1, 1]


Example Output
Output 1:

 [
    [],
    [1],
    [1, 2],
    [1, 2, 2],
    [2],
    [2, 2]
 ]
Output 2:

 [
    [],
    [1],
    [1, 1]
 ]


Example Explanation
Explanation 1:

All the subsets of the array [1, 2, 2] in lexicographically sorted order.

Solution->


  ArrayList<ArrayList<Integer>> list;
    ArrayList<Integer> temp;
    public void subsets(ArrayList<Integer> q , int index){
        if(index == q.size()){
            return;
        }
        
            temp.add(q.get(index));
            list.add(new ArrayList<>(temp));
            subsets(q,index+1);
            temp.remove(temp.size()-1);//4 5
        while(index+1<q.size() && q.get(index)==q.get(index+1)){
            index++;
        }
            subsets(q,index+1);               
    }
    public ArrayList<ArrayList<Integer>> subsetsWithDup(ArrayList<Integer> A) {
        Collections.sort(A);
        list = new ArrayList<>();
        temp = new ArrayList<>();
        list.add(new ArrayList<>());
        subsets(A,0);
        return list;
    }
---------------------------------------------------------------------------------------------------------
