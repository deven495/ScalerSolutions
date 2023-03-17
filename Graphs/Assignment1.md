Q1. Path in Directed Graph

Problem Description
Given an directed graph having A nodes labelled from 1 to A containing M edges given by matrix B of size M x 2such that there is a edge directed from node

B[i][0] to node B[i][1].

Find whether a path exists from node 1 to node A.

Return 1 if path exists else return 0.

NOTE:

There are no self-loops in the graph.
There are no multiple edges between two nodes.
The graph may or may not be connected.
Nodes are numbered from 1 to A.
Your solution will run on multiple test cases. If you are using global variables make sure to clear them.


Problem Constraints
2 <= A <= 105

1 <= M <= min(200000,A*(A-1))

1 <= B[i][0], B[i][1] <= A



Input Format
The first argument given is an integer A representing the number of nodes in the graph.

The second argument given a matrix B of size M x 2 which represents the M edges such that there is a edge directed from node B[i][0] to node B[i][1].



Output Format
Return 1 if path exists between node 1 to node A else return 0.



Example Input
Input 1:

 A = 5
 B = [  [1, 2] 
        [4, 1] 
        [2, 4] 
        [3, 4] 
        [5, 2] 
        [1, 3] ]
Input 2:

 A = 5
 B = [  [1, 2]
        [2, 3] 
        [3, 4] 
        [4, 5] ]


Example Output
Output 1:

 0
Output 2:

 1


Example Explanation
Explanation 1:

 The given doens't contain any path from node 1 to node 5 so we will return 0.
Explanation 2:

 Path from node1 to node 5 is ( 1 -> 2 -> 3 -> 4 -> 5 ) so we will return 1.


Solution ->

    public int findPath(HashMap<Integer,HashSet<Integer>> graph, int start, int end, HashMap<Integer,Boolean>   proc){
        Queue<Integer> q = new LinkedList<>();
        q.add(start);

        while(!q.isEmpty()){
            int parent = q.poll();
            proc.put(parent,true);
            if(graph.get(parent).contains(end)){
                return 1;
            }
            for(int x : graph.get(parent)){
                if(!proc.containsKey(x)){
                    q.add(x);
                }
            }
        }
        return 0;
    }
    public int solve(int A, int[][] B) {
        HashMap<Integer,HashSet<Integer>> graph = new HashMap<>();
        for(int i = 1 ; i <= A ; i++){
            graph.put(i , new HashSet<>());
        }
        for(int[] edge : B){
            graph.get(edge[0]).add(edge[1]);
        }
        return findPath(graph,1,A,new HashMap<Integer,Boolean>());
    }

    
---------------------------------------------------------------------------------------------------------
Q2. Shortest Distance in a Maze

Problem Description
Given a matrix of integers A of size N x M describing a maze. The maze consists of empty locations and walls.

1 represents a wall in a matrix and 0 represents an empty location in a wall.

There is a ball trapped in a maze. The ball can go through empty spaces by rolling up, down, left or right, but it won't stop rolling until hitting a wall (maze boundary is also considered as a wall). When the ball stops, it could choose the next direction.

Given two array of integers of size B and C of size 2 denoting the starting and destination position of the ball.

Find the shortest distance for the ball to stop at the destination. The distance is defined by the number of empty spaces traveled by the ball from the starting position (excluded) to the destination (included). If the ball cannot stop at the destination, return -1.



Problem Constraints
2 <= N, M <= 100

0 <= A[i] <= 1

0 <= B[i][0], C[i][0] < N

0 <= B[i][1], C[i][1] < M



Input Format
The first argument given is the integer matrix A.

The second argument given is an array of integer B.

The third argument if an array of integer C.



Output Format
Return a single integer, the minimum distance required to reach destination



Example Input
Input 1:

A = [ [0, 0], [0, 0] ]
B = [0, 0]
C = [0, 1]
Input 2:

A = [ [0, 0], [0, 1] ]
B = [0, 0]
C = [0, 1]


Example Output
Output 1:

 1
Output 2:

 1


Example Explanation
Explanation 1:

 Go directly from start to destination in distance 1.
Explanation 2:

 Go directly from start to destination in distance 1.


Solution ->

    public void add(int[][] matrix,int newStart[], PriorityQueue<int[]> q,int[][]dp){
        //adding top
        int row = newStart[1]-1;
        int col = newStart[2];
        int count = 0;
        while(row >= 0 && matrix[row][col] == 0){
            row--;
            count++;
        }
        row++;
        if(count > 0 && dp[row][col] == -1){
            q.add(new int[]{newStart[0] + count,row,col});
        }

        //adding down
        row = newStart[1]+1;
        col = newStart[2];
        count = 0;
        while(row < matrix.length && matrix[row][col] == 0){
            row++;
            count++;
        }
        row--;

        if(count > 0 && dp[row][col] == -1){
            q.add(new int[]{newStart[0] + count,row,col});
        }

        //adding left
        row = newStart[1];
        col = newStart[2]-1;
        count = 0;
        while(col >= 0 && matrix[row][col] == 0){
            col--;
            count++;
        }
        col++;
        if(count > 0 && dp[row][col] == -1){
            q.add(new int[]{newStart[0] + count,row,col});
        }

         //adding right
        row = newStart[1];
        col = newStart[2]+1;
        count = 0;
        while(col < matrix[0].length && matrix[row][col] == 0){
            col++;
            count++;
        }
        col--;
        if(count > 0 && dp[row][col] == -1){
            q.add(new int[]{newStart[0] + count,row,col});
        }
    }
    public int solve(int[][] A, int[] B, int[] C) {
        PriorityQueue<int[]> q = new PriorityQueue<>((a,b) -> a[0]-b[0]);
        int dp[][] = new int[A.length][A[0].length];
        for(int[] x : dp){
            Arrays.fill(x,-1);
        }
        q.add(new int[]{0,B[0],B[1]});

        while(!q.isEmpty()){
            int[] newStart = q.poll();
            if(dp[newStart[1]][newStart[2]] != -1){
                continue;
            }
            dp[newStart[1]][newStart[2]] = newStart[0]; 
            if(newStart[1] == C[0] && newStart[2] == C[1]){
                return dp[newStart[1]][newStart[2]] ;
            }
            add(A,newStart,q,dp);
        }
        // System.out.print(Arrays.deepToString(dp));
        return -1;
    }   

    
---------------------------------------------------------------------------------------------------------

Q3. Cycle in Directed Graph

Problem Description
Given an directed graph having A nodes. A matrix B of size M x 2 is given which represents the M edges such that there is a edge directed from node B[i][0] to node B[i][1].

Find whether the graph contains a cycle or not, return 1 if cycle is present else return 0.

NOTE:

The cycle must contain atleast two nodes.
There are no self-loops in the graph.
There are no multiple edges between two nodes.
The graph may or may not be connected.
Nodes are numbered from 1 to A.
Your solution will run on multiple test cases. If you are using global variables make sure to clear them.


Problem Constraints
2 <= A <= 105

1 <= M <= min(200000,A*(A-1))

1 <= B[i][0], B[i][1] <= A



Input Format
The first argument given is an integer A representing the number of nodes in the graph.

The second argument given a matrix B of size M x 2 which represents the M edges such that there is a edge directed from node B[i][0] to node B[i][1].



Output Format
Return 1 if cycle is present else return 0.



Example Input
Input 1:

 A = 5
 B = [  [1, 2] 
        [4, 1] 
        [2, 4] 
        [3, 4] 
        [5, 2] 
        [1, 3] ]
Input 2:

 A = 5
 B = [  [1, 2]
        [2, 3] 
        [3, 4] 
        [4, 5] ]


Example Output
Output 1:

 1
Output 2:

 0


Example Explanation
Explanation 1:

 The given graph contain cycle 1 -> 3 -> 4 -> 1 or the cycle 1 -> 2 -> 4 -> 1
Explanation 2:

 The given graph doesn't contain any cycle.


Solution ->

    public int isCyclic(ArrayList<ArrayList<Integer>> adjList, int totalV){
        int helper[] = new int[totalV+1];
        for(int i = 1 ; i <= totalV ; i++){
            if(helper[i] == 0){
                if(DFS(adjList,helper,i)){
                    return 1;
                }
            }
        }
        return 0;
    }
    public boolean DFS(ArrayList<ArrayList<Integer>> adjList, int[] helper, int Vertex){
        helper[Vertex] = 1;
        for(int child : adjList.get(Vertex)){
            if(helper[child] == 0){
                if(DFS(adjList,helper,child)){
                    return true;
                }
            }else if(helper[child] == 1){
                return true;
            }
        }
        helper[Vertex] = 2;
        return false;
    }
    public int solve(int A, int[][] B) {
        ArrayList<ArrayList<Integer>> graph = new ArrayList<>();
        for(int i = 0 ; i <= A ; i++){
            graph.add(new ArrayList<>());
        }
        for(int i = 0 ; i < B.length ; i++){
            graph.get(B[i][0]).add(B[i][1]);
        }
        return isCyclic(graph,A);
    }

    
---------------------------------------------------------------------------------------------------------

Q4. Number of islands

Problem Description
Given a matrix of integers A of size N x M consisting of 0 and 1. A group of connected 1's forms an island. From a cell (i, j) such that A[i][j] = 1 you can visit any cell that shares a corner with (i, j) and value in that cell is 1.

More formally, from any cell (i, j) if A[i][j] = 1 you can visit:

(i-1, j) if (i-1, j) is inside the matrix and A[i-1][j] = 1.
(i, j-1) if (i, j-1) is inside the matrix and A[i][j-1] = 1.
(i+1, j) if (i+1, j) is inside the matrix and A[i+1][j] = 1.
(i, j+1) if (i, j+1) is inside the matrix and A[i][j+1] = 1.
(i-1, j-1) if (i-1, j-1) is inside the matrix and A[i-1][j-1] = 1.
(i+1, j+1) if (i+1, j+1) is inside the matrix and A[i+1][j+1] = 1.
(i-1, j+1) if (i-1, j+1) is inside the matrix and A[i-1][j+1] = 1.
(i+1, j-1) if (i+1, j-1) is inside the matrix and A[i+1][j-1] = 1.
Return the number of islands.

NOTE: Rows are numbered from top to bottom and columns are numbered from left to right.



Problem Constraints
1 <= N, M <= 100

0 <= A[i] <= 1



Input Format
The only argument given is the integer matrix A.



Output Format
Return the number of islands.



Example Input
Input 1:

 A = [ 
       [0, 1, 0]
       [0, 0, 1]
       [1, 0, 0]
     ]
Input 2:

 A = [   
       [1, 1, 0, 0, 0]
       [0, 1, 0, 0, 0]
       [1, 0, 0, 1, 1]
       [0, 0, 0, 0, 0]
       [1, 0, 1, 0, 1]    
     ]


Example Output
Output 1:

 2
Output 2:

 5


Example Explanation
Explanation 1:

 The 1's at position A[0][1] and A[1][2] forms one island.
 Other is formed by A[2][0].
Explanation 2:

 There 5 island in total.


Solution ->

    boolean[][] visited;

    public void DFS(int[][] matrix, int row, int col) {
        if (row < 0 || row >= matrix.length || col < 0 || col >= matrix[0].length || matrix[row][col] == 0) {
            return;
        }
        // System.out.println(row +"-"+ col);
        if (!visited[row][col]) {
            visited[row][col] = true;
            DFS(matrix, row + 1, col);
            DFS(matrix, row - 1, col);
            DFS(matrix, row, col - 1);
            DFS(matrix, row, col + 1);
            DFS(matrix, row - 1, col - 1);
            DFS(matrix, row - 1, col + 1);
            DFS(matrix, row + 1, col + 1);
            DFS(matrix, row + 1, col - 1);
        }

    }

    public int solve(int[][] A) {
        int count = 0;
        visited = new boolean[A.length][A[0].length];

        for (int row = 0; row < A.length; row++) {
            for (int col = 0; col < A[0].length; col++) {
                if (visited[row][col] == false && A[row][col] != 0) {
                    DFS(A, row, col);
                    // System.out.println(Arrays.deepToString(visited));
                    count++;
                }

            }
        }
        return count;
    }

    
---------------------------------------------------------------------------------------------------------

H.W Q1. First Depth First Search

Problem Description
You are given N towns (1 to N). All towns are connected via unique directed path as mentioned in the input.

Given 2 towns find whether you can reach the first town from the second without repeating any edge.

B C : query to find whether B is reachable from C.

Input contains an integer array A of size N and 2 integers B and C ( 1 <= B, C <= N ).

There exist a directed edge from A[i] to i+1 for every 1 <= i < N. Also, it's guaranteed that A[i] <= i for every 1 <= i < N.

NOTE: Array A is 0-indexed. A[0] = 1 which you can ignore as it doesn't represent any edge.



Problem Constraints
1 <= N <= 100000



Input Format
First argument is vector A

Second argument is integer B

Third argument is integer C



Output Format
Return 1 if reachable, 0 otherwise.



Example Input
Input 1:

 A = [1, 1, 2]
 B = 1
 C = 2
Input 2:

 A = [1, 1, 2]
 B = 2
 C = 1


Example Output
Output 1:

 0
Output 2:

 1


Example Explanation
Explanation 1:

 Tree is 1--> 2--> 3 and hence 1 is not reachable from 2.
Explanation 2:

 Tree is 1--> 2--> 3 and hence 2 is reachable from 1.


Solution ->

    public int findPath(HashMap<Integer,HashSet<Integer>> graph, int start, int end, HashMap<Integer,Boolean>   proc){
        Queue<Integer> q = new LinkedList<>();
        q.add(start);

        while(!q.isEmpty()){
            int parent = q.poll();
            proc.put(parent,true);
            if(graph.get(parent).contains(end)){
                return 1;
            }
            for(int x : graph.get(parent)){
                if(!proc.containsKey(x)){
                    q.add(x);
                }
            }
        }
        return 0;
    }
    public int solve(int[] A, final int B, final int C) {
        if(B == C) return 1;
        HashMap<Integer,HashSet<Integer>> graph = new HashMap<>();
        for(int i = 0 ; i <= A.length ; i++){
            graph.put(i , new HashSet<>());
        }
        for(int i = 0 ; i < A.length ; i++){
            graph.get(A[i]).add(i+1);
        }
        // System.out.print(graph);
        return findPath(graph,C,B,new HashMap<Integer,Boolean>());
    }

    
---------------------------------------------------------------------------------------------------------
Q2. Clone Graph

Problem Description
Clone an undirected graph. Each node in the graph contains a label and a list of its neighbors.

Note: The test cases are generated in the following format (use the following format to use See Expected Output option):
First integer N is the number of nodes.
Then, N intgers follow denoting the label (or hash) of the N nodes.
Then, N2 integers following denoting the adjacency matrix of a graph, where Adj[i][j] = 1 denotes presence of an undirected edge between the ith and jth node, O otherwise.



Problem Constraints
1 <= Number of nodes <= 105



Input Format
First and only argument is a node A denoting the root of the undirected graph.



Output Format
Return the node denoting the root of the new clone graph.



Example Input
Input 1:

      1
    / | \
   3  2  4
        / \
       5   6
Input 2:

      1
     / \
    3   4
   /   /|\
  2   5 7 6


Example Output
Output 1:

 Output will the same graph but with new pointers:
      1
    / | \
   3  2  4
        / \
       5   6
Output 2:

      1
     / \
    3   4
   /   /|\
  2   5 7 6


Example Explanation
Explanation 1:

 We need to return the same graph, but the pointers to the node should be different.



Solution ->

    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        HashMap<UndirectedGraphNode,UndirectedGraphNode> cloning= new HashMap<>();
        Queue<UndirectedGraphNode> q = new LinkedList<>();
        
        cloning.put(node,new UndirectedGraphNode(node.label));
        q.add(node);
        while(!q.isEmpty()){
            UndirectedGraphNode parent = q.poll();
            for(UndirectedGraphNode child : parent.neighbors){
                if(!cloning.containsKey(child)){
                    UndirectedGraphNode newNode = new UndirectedGraphNode(child.label);
                    cloning.put(child,newNode);
                    cloning.get(parent).neighbors.add(newNode);
                    q.add(child);
                }else{
                    cloning.get(parent).neighbors.add(cloning.get(child));
                }
            }
        }
        return cloning.get(node);
    }

    
---------------------------------------------------------------------------------------------------------

Q3. Valid Path
Unsolved
character backgroundcharacter
Stuck somewhere?
Ask for help from a TA and get it resolved.
Get help from TA.
Problem Description
There is a rectangle with left bottom as (0, 0) and right up as (x, y).

There are N circles such that their centers are inside the rectangle.

Radius of each circle is R. Now we need to find out if it is possible that we can move from (0, 0) to (x, y) without touching any circle.

Note : We can move from any cell to any of its 8 adjecent neighbours and we cannot move outside the boundary of the rectangle at any point of time.



Problem Constraints
0 <= x , y, R <= 100

1 <= N <= 1000

Center of each circle would lie within the grid



Input Format
1st argument given is an Integer x , denoted by A in input.

2nd argument given is an Integer y, denoted by B in input.

3rd argument given is an Integer N, number of circles, denoted by C in input.

4th argument given is an Integer R, radius of each circle, denoted by D in input.

5th argument given is an Array A of size N, denoted by E in input, where A[i] = x cordinate of ith circle

6th argument given is an Array B of size N, denoted by F in input, where B[i] = y cordinate of ith circle



Output Format
Return YES or NO depending on weather it is possible to reach cell (x,y) or not starting from (0,0).



Example Input
Input 1:

 x = 2
 y = 3
 N = 1
 R = 1
 A = [2]
 B = [3]
Input 2:

 x = 1
 y = 1
 N = 1
 R = 1
 A = [1]
 B = [1]


Example Output
Output 1:

 NO
Output 2:

 NO


Example Explanation
Explanation 1:

 There is NO valid path in this case
Explanation 2:

 There is NO valid path in this case


Solution ->

    
---------------------------------------------------------------------------------------------------------

Q4. Black Shapes

Problem Description

Given character matrix A of O's and X's, where O = white, X = black.

Return the number of black shapes. A black shape consists of one or more adjacent X's (diagonals not included)



Problem Constraints

1 <= |A|,|A[0]| <= 1000

A[i][j] = 'X' or 'O'



Input Format

The First and only argument is character matrix A.



Output Format

Return a single integer denoting number of black shapes.



Example Input

Input 1:

 A = [ [X, X, X], [X, X, X], [X, X, X] ]
Input 2:

 A = [ [X, O], [O, X] ]


Example Output

Output 1:

 1
Output 2:

 2


Example Explanation

Explanation 1:

 All X's belong to single shapes
Explanation 2:

 Both X's belong to different shapes


Solution ->

boolean[][] visited;

    public void DFS(ArrayList<ArrayList<Character>> matrix, int row, int col) {
        if (row < 0 || row >= matrix.size() || col < 0 || col >= matrix.get(0).size() || matrix.get(row).get(col) == 'O') {
            return;
        }
        if (!visited[row][col]) {
            visited[row][col] = true;
            DFS(matrix, row + 1, col);
            DFS(matrix, row - 1, col);
            DFS(matrix, row, col - 1);
            DFS(matrix, row, col + 1);
        }

    }

    public int solve(ArrayList<ArrayList<Character>> A) {
        int count = 0;
        visited = new boolean[A.size()][A.get(0).size()];
        for (int row = 0; row < A.size(); row++) {
            for (int col = 0; col < A.get(0).size(); col++) {
                if (visited[row][col] == false && A.get(row).get(col) != 'O') {
                    DFS(A, row, col);
                    count++;
                }

            }
        }
        return count;
    }
    public ArrayList<ArrayList<Character>> listMaking(String[] A){
         ArrayList<ArrayList<Character>> matrix = new ArrayList<>();
        for(int j = 0 ; j < A.length ; j++){
             String a = A[j];
            ArrayList<Character> list = new ArrayList<>();
            for (int i = 0; i < a.length(); i++) {
                if (a.charAt(i) == 'X' || a.charAt(i) == 'O') {
                    list.add(a.charAt(i));
                }
            }
            matrix.add(list);
        }
        // System.out.print(matrix);
        return matrix;
    }
    public int black(String[] A) {
    ArrayList<ArrayList<Character>> matrix = listMaking(A);
    return solve(matrix);
    }

    
---------------------------------------------------------------------------------------------------------

Q-> 


Solution ->

    
---------------------------------------------------------------------------------------------------------


