BackTracking 1 - > 
Q1. NQueens

Problem Description
The n-queens puzzle is the problem of placing n queens on an n×n chessboard such that no two queens attack each other.



Given an integer A, return all distinct solutions to the n-queens puzzle.

Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space respectively.
The final list should be generated in such a way that the indices of the queens in each list should be in reverse lexicographical order.


Problem Constraints
1 <= A <= 10



Input Format
First argument is an integer n denoting the size of chessboard



Output Format
Return an array consisting of all distinct solutions in which each element is a 2d char array representing a unique solution.



Example Input
Input 1:

A = 4
Input 2:

A = 1


Example Output
Output 1:

[
 [".Q..",  // Solution 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // Solution 2
  "Q...",
  "...Q",
  ".Q.."]
]
Output 1:

[
 [Q]
]


Example Explanation
Explanation 1:

There exist only two distinct solutions to the 4-queens puzzle:
Explanation 1:

There exist only one distinct solutions to the 1-queens puzzle:

Solution ->

    boolean[][] chessBoard;
    ArrayList<ArrayList<String>> mainlist;
    
    public void updateAns(int n)
    {
        ArrayList<String> list = new ArrayList<>();
        for(int i=0; i<n; i++)
        {
            StringBuilder sb=new StringBuilder();
            for(int j=0; j<n; j++)
            {
                if(chessBoard[i][j])
                {
                    sb.append("Q");
                }
                else
                {
                    sb.append(".");
                }
            }
            
            list.add(sb.toString());
        }
        
        mainlist.add(list);
    }

    public boolean isItSafe(int dangerRow, int dangerCol){
        int row = dangerRow -1;
        int col = dangerCol;
        while(row >=0){
            if(chessBoard[row][col]){
                return false;
            }
            row--;
        }
        row = dangerRow;
        col = dangerCol-1;
        while(col >= 0){
            if(chessBoard[row][col]){
                return false;
            }
            col--;
        }
        row = dangerRow-1;
        col = dangerCol-1;
        while(row >= 0 && col >= 0){
            if(chessBoard[row][col]){
                return false;
            }
            row--;
            col--;
        }
        row = dangerRow-1;
        col = dangerCol+1;
        while(row >= 0 && col < chessBoard[0].length){
            if(chessBoard[row][col]){
                return false;
            }
            row--;
            col++;
        }
        return true;
    }
    
    
    public void nQueens(int row, int col, int qpsf, int tq){
        if(qpsf == tq){
            updateAns(tq);
            return;
        }
        if(col == chessBoard[0].length){
            row = row+1;
            col = 0;
        }
        if(row >= chessBoard.length){
            return;
        }
        if(isItSafe(row,col)){
            chessBoard[row][col] = true;
            nQueens(row+1,0,qpsf+1,tq);
            chessBoard[row][col] = false;
        }
        nQueens(row,col+1,qpsf,tq);

    }
	public ArrayList<ArrayList<String>> solveNQueens(int A) {
        chessBoard = new boolean[A][A];
        mainlist = new ArrayList<>();
        nQueens(0,0,0,A);
        return mainlist;
	}
---------------------------------------------------------------------------------------------------------
Q2. Sudoku

Problem Description
Write a program to solve a Sudoku puzzle by filling the empty cells. Empty cells are indicated by the character '.' You may assume that there will be only one unique solution.



A sudoku puzzle,



and its solution numbers marked in red.



Problem Constraints
N = 9


Input Format
First argument is an array of array of characters representing the Sudoku puzzle.


Output Format
Modify the given input to the required answer.


Example Input
Input 1:

A = [[53..7....], [6..195...], [.98....6.], [8...6...3], [4..8.3..1], [7...2...6], [.6....28.], [...419..5], [....8..79]]


Example Output
Output 1:

[[534678912], [672195348], [198342567], [859761423], [426853791], [713924856], [961537284], [287419635], [345286179]]


Example Explanation
Explanation 1:

Look at the diagrams given in the question.

Solution ->

    ArrayList<ArrayList<Character>> ans;
	boolean flag;
	public boolean isValid(char val,int row, int col, ArrayList<ArrayList<Character>> q){
		int startRow = row/3 * 3;
		int startCol = col/3 * 3;
		int r = row;
		int c = 0;
		while(c < q.get(0).size()){
			if(val == q.get(r).get(c)){
				return false;
			}
			c++;
		}
		r = 0;
		c = col;
		while(r < q.size()){
			if(val == q.get(r).get(c)){
				return false;
			}
			r++;
		}
		for(int i = startRow ; i < startRow + 3 ; i++){
			for(int j = startCol ; j < startCol + 3 ; j++){
				if(val == q.get(i).get(j)){
					return false;
				}
			}
		}
		return true;
	}
	public void sudokuSolver(int row , int col, ArrayList<ArrayList<Character>> q){
		if(flag){
			return;
		}
		if(col == q.get(0).size()){
			row = row + 1;
			col = 0;
		}
		if(row == q.size()){
			flag = true;
			for(int i = 0 ; i < q.size() ; i++){
				ans.add(new ArrayList<>());
				for(int j = 0 ; j < q.get(i).size() ; j++){
					ans.get(i).add(q.get(i).get(j));
				}
			}
			return;
		}
			if(q.get(row).get(col) == '.'){
				for(int i = 1 ; i < 10 ; i++){
				if(isValid((char)(i + '0'),row,col,q)){
					q.get(row).set(col,(char)(i + '0'));
					sudokuSolver(row,col+1,q);
					q.get(row).set(col,'.');
					}
				}
			}else{
				sudokuSolver(row,col+1,q);
			}
				
		}
	
	public void solveSudoku(ArrayList<ArrayList<Character>> a) {
		ans = new ArrayList<>();
		flag = false;
		sudokuSolver(0,0,a);
		for(int i = 0 ; i < a.size() ; i++){
				for(int j = 0 ; j < a.get(i).size() ; j++){
					a.get(i).set(j,ans.get(i).get(j));
			}
		}

		return;	
	}
---------------------------------------------------------------------------------------------------------
Q3. Word Break

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

    HashSet<String> set = new HashSet<>();
    public int wordBreak(String A, ArrayList<String> B) {
        String ans = "";
        for(String word: B){
            set.add(word);
        }
        return (generate(A, B, 0, new Boolean[A.length()]) ? 1 : 0);
    }
    public boolean generate(String str, ArrayList<String> B, int position, Boolean[] dp){
        if(str.length() == position){
            return true;
        }
        if(dp[position] != null){
            return dp[position];
        }
        for(int i=position; i<=str.length(); i++){
            if((set.contains(str.substring(position, i))) && (generate(str, B, i, dp))){
                return dp[position] = true;
            }  
        }
        return dp[position] = false;
    }

---------------------------------------------------------------------------------------------------------
Q1. Combination Sum

Problem Description
Given an array of candidate numbers A and a target number B, find all unique combinations in A where the candidate numbers sums to B.

The same repeated number may be chosen from A unlimited number of times.

Note:

1) All numbers (including target) will be positive integers.

2) Elements in a combination (a1, a2, … , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak).

3) The combinations themselves must be sorted in ascending order.

4) CombinationA > CombinationB iff (a1 > b1) OR (a1 = b1 AND a2 > b2) OR ... (a1 = b1 AND a2 = b2 AND ... ai = bi AND ai+1 > bi+1)

5) The solution set must not contain duplicate combinations.



Problem Constraints
1 <= |A| <= 20

1 <= A[i] <= 50

1 <= B <= 500



Input Format
The first argument is an integer array A.

The second argument is integer B.



Output Format
Return a vector of all combinations that sum up to B.



Example Input
Input 1:

A = [2, 3]
B = 2
Input 2:

A = [2, 3, 6, 7]
B = 7


Example Output
Output 1:

[ [2] ]
Output 2:

[ [2, 2, 3] , [7] ]


Example Explanation
Explanation 1:

All possible combinations are listed.
Explanation 2:

All possible combinations are listed.

Solution ->

    ArrayList<ArrayList<Integer>> list;
    public void combinations(int indx,ArrayList<Integer> q, int target,ArrayList<Integer> temp){
        if(target == 0){
            list.add(new ArrayList<>(temp));
            return;
        }
        if(target < 0 || indx == q.size()){
            return;
        }
        for(int i = indx ; i < q.size() ; i++){
            if(i != q.size()-1 && q.get(i) == q.get(i+1)){
                continue;
            }
                temp.add(q.get(i));
                combinations(i,q,target-q.get(i),temp);
                temp.remove(temp.size()-1);
            }

    }
    public ArrayList<ArrayList<Integer>> combinationSum(ArrayList<Integer> A, int B) {
        Collections.sort(A);
        list = new ArrayList<>();
        ArrayList<Integer> temp = new ArrayList<>();
        combinations(0,A,B,temp);
        return list;
    }     

---------------------------------------------------------------------------------------------------------
Q2. Combination Sum II

Problem Description
Given an array of size N of candidate numbers A and a target number B. Return all unique combinations in A where the candidate numbers sums to B.

Each number in A may only be used once in the combination.

Note:

All numbers (including target) will be positive integers.
Elements in a combination (a1, a2, … , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak).
The solution set must not contain duplicate combinations.
Warning:

DO NOT USE LIBRARY FUNCTION FOR GENERATING COMBINATIONS.

Example : itertools.combinations in python. If you do, we will disqualify your submission and give you penalty points.



Problem Constraints
1 <= N <= 20



Input Format
First argument is an integer array A denoting the collection of candidate numbers.
Second argument is an integer which represents the target number.



Output Format
Return all unique combinations in A where the candidate numbers sums to B.



Example Input
Input 1:

 A = [10, 1, 2, 7, 6, 1, 5]
 B = 8
Input 2:

 A = [2, 1, 3]
 B = 3


Example Output
Output 1:

 [ 
  [1, 1, 6 ],
  [1, 2, 5 ],
  [1, 7 ], 
  [2, 6 ] 
 ]
Output 2:

 [
  [1, 2 ],
  [3 ]
 ]


Example Explanation
Explanation 1:

 1 + 1 + 6 = 8
 1 + 2 + 5 = 8
 1 + 7 = 8
 2 + 6 = 8
 All the above combinations sum to 8 and are arranged in ascending order.
Explanation 2:

 1 + 2 = 3
 3 = 3
 All the above combinations sum to 3 and are arranged in ascending order.
 Solution->

    ArrayList<ArrayList<Integer>> list;
    public void combinations(int indx,ArrayList<Integer> q, int target,ArrayList<Integer> temp){
        if(target == 0){
            list.add(new ArrayList<>(temp));
            return;
        }
        if(target < 0 || indx == q.size()){
            return;
        }
        for(int i = indx+1 ; i < q.size() ; i++){
                temp.add(q.get(i));
                combinations(i,q,target-q.get(i),temp);
                while(i!= q.size()-1 && q.get(i) == q.get(i+1)){
                    i++;
                }
                temp.remove(temp.size()-1);
            }

    }
    public ArrayList<ArrayList<Integer>> combinationSum(ArrayList<Integer> A, int B) {
        Collections.sort(A);
        list = new ArrayList<>();
        ArrayList<Integer> temp = new ArrayList<>();
        combinations(-1,A,B,temp);
        return list;
    }

---------------------------------------------------------------------------------------------------------
Q3. Palindrome Partitioning

Problem Description
Given a string A, partition A such that every string of the partition is a palindrome.

Return all possible palindrome partitioning of A.

Ordering the results in the answer : Entry i will come before Entry j if :
len(Entryi[0]) < len(Entryj[0]) OR
(len(Entryi[0]) == len(Entryj[0]) AND len(Entryi[1]) < len(Entryj[1])) OR * * *
(len(Entryi[0]) == len(Entryj[0]) AND ... len(Entryi[k] < len(Entryj[k]))


Problem Constraints
1 <= len(A) <= 15



Input Format
First argument is a string A of lowercase characters.



Output Format
Return a list of all possible palindrome partitioning of s.



Example Input
Input 1:

A = "aab"
Input 2:

A = "a"


Example Output
Output 1:

 [
    ["a","a","b"]
    ["aa","b"],
  ]
Output 2:

 [
    ["a"]
  ]


Example Explanation
Explanation 1:

In the given example, ["a", "a", "b"] comes before ["aa", "b"] because len("a") < len("aa").
Explanation 2:

In the given example, only partition possible is "a" .
 Solutions ->

    ArrayList<ArrayList<String>> list;
    public boolean isValid(String q){
        int start = 0;
        int end = q.length()-1;
        while(start <= end){
            if(q.charAt(start) != q.charAt(end)){
                return false;
            }
            start++;
            end--;
        }
        return true;
    }
    public void check(int position,String q,ArrayList<String> temp){
        if(position == q.length()){
            list.add(new ArrayList<>(temp));
            return;
        }
        for(int i = position ; i < q.length() ; i++){
            if(isValid(q.substring(position,i+1))){
                temp.add(q.substring(position,i+1));
                check(i+1,q,temp);
                temp.remove(temp.size()-1);
            }
        }
    }
	public ArrayList<ArrayList<String>> partition(String a) {
        list = new ArrayList<>();
        ArrayList<String> temp = new ArrayList<>();
        check(0,a,temp);
        return list;
	}
---------------------------------------------------------------------------------------------------------
