Q1. Rotten Oranges

Problem Description
Given a matrix of integers A of size N x M consisting of 0, 1 or 2.

Each cell can have three values:

The value 0 representing an empty cell.

The value 1 representing a fresh orange.

The value 2 representing a rotten orange.

Every minute, any fresh orange that is adjacent (Left, Right, Top, or Bottom) to a rotten orange becomes rotten. Return the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return -1 instead.

Note: Your solution will run on multiple test cases. If you are using global variables, make sure to clear them.



Problem Constraints
1 <= N, M <= 1000

0 <= A[i][j] <= 2



Input Format
The first argument given is the integer matrix A.



Output Format
Return the minimum number of minutes that must elapse until no cell has a fresh orange.

If this is impossible, return -1 instead.



Example Input
Input 1:

A = [   [2, 1, 1]
        [1, 1, 0]
        [0, 1, 1]   ]
Input 2:

 
A = [   [2, 1, 1]
        [0, 1, 1]
        [1, 0, 1]   ]


Example Output
Output 1:

 4
Output 2:

 -1


Example Explanation
Explanation 1:

 Max of 4 using (0,0) , (0,1) , (1,1) , (1,2) , (2,2)
Explanation 2:

 Task is impossible


Solution ->

    public class Solution {
    class Triple {
        int row;
        int col;
        int time;
        Triple(int row, int col, int time) {
            this.row = row;
            this.col = col;
            this.time = time;
        }
    }
    public int solve(int[][] A) {
        int n = A.length;
        int m = A[0].length;
        
        int[][] dis = new int[n][m];
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < m; j++) {
                dis[i][j] = Integer.MAX_VALUE;
            }
        }
        
        Queue<Triple> q = new LinkedList<>();
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < m; j++) {
                if(A[i][j] == 2) {
                    q.add(new Triple(i, j, 0));
                }
            }
        }
        
        while(!q.isEmpty()) {
            Triple top = q.poll();
            int row = top.row;
            int col = top.col;
            int time = top.time;
            
            int[] dx = {0, 0, 1, -1};
            int[] dy = {1, -1, 0, 0};
                     
            for(int dir = 0; dir < 4; dir++) {
                int nx = row + dx[dir];
                int ny = col + dy[dir];
                
                if(nx >= 0 && nx < n && ny >= 0 && ny < m && A[nx][ny] == 1 && time + 1 < dis[nx][ny]) {
                    dis[nx][ny] = time + 1;
                    q.add(new Triple(nx, ny, time + 1));
                }
            }
        }
        
        int max = Integer.MIN_VALUE;
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < m; j++) {
                if(A[i][j] == 1) {
                    max = Math.max(max, dis[i][j]);
                }
            }
        }
        
        if(max == Integer.MIN_VALUE || max == Integer.MAX_VALUE)
            return -1;
        
        return max;
    }
    }



    
---------------------------------------------------------------------------------------------------------
Q2. Coloring a Cycle Graph

Given the number of vertices A in a Cyclic Graph.

Your task is to determine the minimum number of colors required to color the graph so that no two Adjacent vertices have the same color.


A cyclic graph with A vertices is a graph with A edges, such that it forms a loop. See example test case explanation for more details.



Problem Constraints
3 <= A <= 109



Input Format
First argument is an integer A denoting the number of vertices in the Cyclic Graph.



Output Format
Return an single integer denoting the minimum number of colors required to color the graph so that no two Adjacent vertices have the same color.



Example Input
Input 1:

 5
Input 2:

 4


Example Output
Output 1:

 3
Output 2:

 2



Solution ->

    public int solve(int A) {
      return A%2 == 0 ? 2 : 3;  
    }

    
---------------------------------------------------------------------------------------------------------

Q3. Check Bipartite Graph

Given a undirected graph having A nodes. A matrix B of size M x 2 is given which represents the edges such that there is an edge between B[i][0] and B[i][1].

Find whether the given graph is bipartite or not.

A graph is bipartite if we can split it's set of nodes into two independent subsets A and B such that every edge in the graph has one node in A and another node in B

Note:

There are no self-loops in the graph.

No multiple edges between two pair of vertices.

The graph may or may not be connected.

Nodes are Numbered from 0 to A-1.

Your solution will run on multiple testcases. If you are using global variables make sure to clear them.



Problem Constraints
1 <= A <= 100000

1 <= M <= min(A*(A-1)/2,200000)

0 <= B[i][0],B[i][1] < A



Input Format
The first argument given is an integer A.

The second argument given is the matrix B.



Output Format
Return 1 if the given graph is bipartide else return 0.



Example Input
Input 1:

A = 2
B = [ [0, 1] ]
Input 2:

A = 3
B = [ [0, 1], [0, 2], [1, 2] ]


Example Output
Output 1:

1
Output 2:

0


Example Explanation
Explanation 1:

Put 0 and 1 into 2 different subsets.
Explanation 2:

 
It is impossible to break the graph down to make two different subsets for bipartite matching


Solution ->

    public int bipartite(ArrayList<ArrayList<Integer>> graph){
        int n = graph.size();
        Queue<Integer> q = new LinkedList<>();
        int vis[] = new int[n];

        for(int i = 0 ; i < n ; i++){
            if(vis[i] != 0){
                continue;
            }
            q.add(i);
            vis[i]=1;
            while(!q.isEmpty()){
                int node = q.poll();
                for(int child : graph.get(node)){
                    if(vis[child] == 0){
                        q.add(child);
                        if(vis[node] == 1){
                            vis[child] = 2;
                        }else{
                            vis[child] = 1;
                        }
                    }else{
                        if(vis[child] == vis[node]){
                            return 0;
                        }
                    }
                }
            }
        }
        return 1;
    }
    public int solve(int A, int[][] B) {
        ArrayList<ArrayList<Integer>> graph = new ArrayList<>();
        for(int i = 0 ; i < A ; i++){
            graph.add(new ArrayList<>());
        }
        for(int[] x : B){
            graph.get(x[0]).add(x[1]);
            graph.get(x[1]).add(x[0]);
        }
        return bipartite(graph);
    }

    
---------------------------------------------------------------------------------------------------------

Q4. Construct Roads

A country consist of N cities connected by N - 1 roads. King of that country want to construct maximum number of roads such that the new country formed remains bipartite country.

Bipartite country is a country, whose cities can be partitioned into 2 sets in such a way, that for each road (u, v) that belongs to the country, u and v belong to different sets. Also, there should be no multiple roads between two cities and no self loops.

Return the maximum number of roads king can construct. Since the answer could be large return answer % 109 + 7.

NOTE: All cities can be visited from any city.



Problem Constraints
1 <= A <= 105

1 <= B[i][0], B[i][1] <= N



Input Format
First argument is an integer A denoting the number of cities, N.

Second argument is a 2D array B of size (N-1) x 2 denoting the initial roads i.e. there is a road between cities B[i][0] and B[1][1] .



Output Format
Return an integer denoting the maximum number of roads king can construct.



Example Input
Input 1:

 A = 3
 B = [
       [1, 2]
       [1, 3]
     ]
Input 2:

 A = 5
 B = [
       [1, 3]
       [1, 4]
       [3, 2]
       [3, 5]
     ]


Example Output
Output 1:

 0
Output 2:

 2


Example Explanation
Explanation 1:

 We can't construct any new roads such that the country remains bipartite.
Explanation 2:

 We can add two roads between cities (4, 2) and (4, 5).


Solution ->

    public int maximum(ArrayList<ArrayList<Integer>> graph){
        int n = graph.size();
        int mod = 1000000007;
        Queue<Integer> q = new LinkedList<>();
        int one = 0;
        int two = 0;
        int vis[] = new int[n];
        for(int i = 1 ; i < n ; i++){
            if(vis[i] != 0){
                continue;
            }
            vis[i] = 1 ;
            q.add(i);
            while(!q.isEmpty()){
                int node = q.poll();
                for(int x : graph.get(node)){
                    if(vis[x] == 0){
                        q.add(x);
                        if(vis[node] == 1){
                            vis[x] = 2;
                        }else{
                            vis[x] = 1;
                        }
                    }
                }
            }
        }
        for(int j = 1 ; j < n ; j++){
            if(vis[j] == 1){
                one++;
            }else if(vis[j] == 2){
                two++;
            }
        }
        long y = (one * two)%mod;
        return (int)((one*1l*two - (n-2))%mod);

    }
    public int solve(int A, int[][] B) {
        ArrayList<ArrayList<Integer>> graph = new ArrayList<>();
        for(int i = 0 ; i <= A ; i++){
            graph.add(new ArrayList<>());
        }
        for(int[]x : B){
            graph.get(x[0]).add(x[1]);
            graph.get(x[1]).add(x[0]);
        }
        return maximum(graph);
    }

    
---------------------------------------------------------------------------------------------------------

H.W Q1. Distance of nearest cell

Given a matrix of integers A of size N x M consisting of 0 or 1.

For each cell of the matrix find the distance of nearest 1 in the matrix.

Distance between two cells (x1, y1) and (x2, y2) is defined as |x1 - x2| + |y1 - y2|.

Find and return a matrix B of size N x M which defines for each cell in A distance of nearest 1 in the matrix A.

NOTE: There is atleast one 1 is present in the matrix.



Problem Constraints
1 <= N, M <= 1000

0 <= A[i][j] <= 1



Input Format
The first argument given is the integer matrix A.



Output Format
Return the matrix B.



Example Input
Input 1:

 A = [
       [0, 0, 0, 1]
       [0, 0, 1, 1] 
       [0, 1, 1, 0]
     ]
Input 2:

 A = [
       [1, 0, 0]
       [0, 0, 0]
       [0, 0, 0]  
     ]


Example Output
Output 1:

 [ 
   [3, 2, 1, 0]
   [2, 1, 0, 0]
   [1, 0, 0, 1]   
 ]
Output 2:

 [
   [0, 1, 2]
   [1, 2, 3]
   [2, 3, 4] 
 ]


Example Explanation
Explanation 1:

 A[0][0], A[0][1], A[0][2] will be nearest to A[0][3].
 A[1][0], A[1][1] will be nearest to A[1][2].
 A[2][0] will be nearest to A[2][1] and A[2][3] will be nearest to A[2][2].
Explanation 2:

 There is only a single 1. Fill the distance from that 1. 


Solution ->

    class pair{
        int row;
        int col;
        int time;
        pair(int row,int col,int time){
            this.row = row;
            this.col = col;
            this.time = time;
        }
    }
    public int[][] solve(int[][] A) {
        Queue<pair> q = new LinkedList<>();
        for(int i = 0 ; i < A.length ; i++){
            for(int j = 0 ; j < A[0].length ; j++){
               if(A[i][j] == 1){
                   q.add(new pair(i,j,0));
               } 
            }
        }
        int dist[][] = new int[A.length][A[0].length];
        for(int i = 0 ; i < A.length ; i++){
            for(int j = 0 ; j < A[0].length ; j++){
                if(A[i][j] == 0){
                    dist[i][j] = Integer.MAX_VALUE;
                }
            }
        }
        
        while(!q.isEmpty()){
            pair curr = q.poll();
            int r = curr.row;
            int c = curr.col;
            int t = curr.time;

            int[]dx = {-1,0,0,1};
            int[]dy = {0,-1,1,0};

            for(int k = 0 ; k < 4 ; k++){
                int roww = r + dx[k];
                int coll = c + dy[k];
                if(roww >= 0 && roww < A.length && coll >= 0 && coll < A[0].length && A[roww][coll] == 0 && t+1 < dist[roww][coll]){
                    dist[roww][coll] = t+1;
                    q.add(new pair(roww,coll,t+1));
                }
            }
        }
        return dist;
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


