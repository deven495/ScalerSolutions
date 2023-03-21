Q1. Topological Sort

Given an directed acyclic graph having A nodes. A matrix B of size M x 2 is given which represents the M edges such that there is a edge directed from node B[i][0] to node B[i][1].

Topological sorting for Directed Acyclic Graph (DAG) is a linear ordering of vertices such that for every directed edge uv, vertex u comes before v in the ordering. Topological Sorting for a graph is not possible if the graph is not a DAG.

Return the topological ordering of the graph and if it doesn't exist then return an empty array.

If there is a solution return the correct ordering. If there are multiple solutions print the lexographically smallest one.

Ordering (a, b, c) is said to be lexographically smaller than ordering (e, f, g) if a < e or if(a==e) then b < f and so on.

NOTE:

There are no self-loops in the graph.
There are no multiple edges between two nodes.
The graph may or may not be connected.
Nodes are numbered from 1 to A.
Your solution will run on multiple test cases. If you are using global variables make sure to clear them.


Problem Constraints
2 <= A <= 104

1 <= M <= min(100000,A*(A-1))

1 <= B[i][0], B[i][1] <= A



Input Format
The first argument given is an integer A representing the number of nodes in the graph.

The second argument given a matrix B of size M x 2 which represents the M edges such that there is a edge directed from node B[i][0] to node B[i][1].



Output Format
Return a one-dimensional array denoting the topological ordering of the graph and it it doesn't exist then return empty array.



Example Input
Input 1:

 A = 6
 B = [  [6, 3] 
        [6, 1] 
        [5, 1] 
        [5, 2] 
        [3, 4] 
        [4, 2] ]
Input 2:

 A = 3
 B = [  [1, 2]
        [2, 3] 
        [3, 1] ]


Example Output
Output 1:

 [5, 6, 1, 3, 4, 2]
Output 2:

 []


Example Explanation
Explanation 1:

 The given graph contain no cycle so topological ordering exists which is [5, 6, 1, 3, 4, 2]
Explanation 2:

 The given graph contain cycle so topological ordering not possible we will return empty array.


Solution ->

    public void makeGraph(int A , int B[][],int inCount[],ArrayList<ArrayList<Integer>> graph){
        for(int i = 0 ; i <= A ; i++){
            graph.add(new ArrayList<>());
        }
        for(int[]x : B){
            graph.get(x[0]).add(x[1]);
            inCount[x[1]]++;
        }
    }
    public int[] solve(int A, int[][] B) {
        ArrayList<ArrayList<Integer>> graph = new ArrayList<>();
        PriorityQueue<Integer> q = new PriorityQueue<>();
        int[] ans = new int[A];
        int[] inCount = new int[A+1];
        int index = 0;

        makeGraph(A,B,inCount,graph);
        for(int i = 1 ; i < inCount.length; i++){
            if(inCount[i] == 0){
               q.add(i);
            }
        }
        while(!q.isEmpty()){
            int polled = q.poll();
            ans[index++] = polled;
            for(int child : graph.get(polled)){
                inCount[child]--;
                if(inCount[child] == 0){
                    q.add(child);
                }
            }
        }
    return (index == A) ? ans : new int[]{}; 
    }

    
---------------------------------------------------------------------------------------------------------
Q2. Possibility of Finishing

There are a total of A courses you have to take, labeled from 1 to A.

Some courses may have prerequisites, for example to take course 2 you have to first take course 1, which is expressed as a pair: [1,2].

So you are given two integer array B and C of same size where for each i (B[i], C[i]) denotes a pair.

Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

Return 1 if it is possible to finish all the courses, or 0 if it is not possible to finish all the courses.



Problem Constraints
1 <= A <= 6*104

1 <= length(B) = length(C) <= 105

1 <= B[i], C[i] <= A



Input Format
The first argument of input contains an integer A, representing the number of courses.

The second argument of input contains an integer array, B.

The third argument of input contains an integer array, C.



Output Format
Return 1 if it is possible to finish all the courses, or 0 if it is not possible to finish all the courses.



Example Input
Input 1:

 A = 3
 B = [1, 2]
 C = [2, 3]
Input 2:

 A = 2
 B = [1, 2]
 C = [2, 1]


Example Output
Output 1:

 1
Output 2:

 0


Example Explanation
Explanation 1:

 It is possible to complete the courses in the following order:
    1 -> 2 -> 3
Explanation 2:

 It is not possible to complete all the courses.


Solution ->

    public int solve2(int A, ArrayList<ArrayList<Integer>> graph,int[] inCount) {
        PriorityQueue<Integer> q = new PriorityQueue<>();
        int[] ans = new int[A];
        int index = 0;
        for(int i = 1 ; i < inCount.length; i++){
            if(inCount[i] == 0){
               q.add(i);
            }
        }
        while(!q.isEmpty()){
            int polled = q.poll();
            ans[index++] = polled;
            for(int child : graph.get(polled)){
                inCount[child]--;
                if(inCount[child] == 0){
                    q.add(child);
                }
            }
        }
    return (index == A) ? 1 : 0; 
    }
    public int solve(int A, int[] B, int[] C) {
        int[] inCount = new int[A+1];
        ArrayList<ArrayList<Integer>> graph = new ArrayList<>();
        for(int i = 0 ; i <= A; i++){
            graph.add(new ArrayList<>());
        }
        for(int i = 0 ; i < B.length ; i++){
            graph.get(B[i]).add(C[i]);
            inCount[C[i]]++;
        }
        // System.out.print(graph);
        return solve2(A,graph,inCount);
    }       

    
---------------------------------------------------------------------------------------------------------

Q3. Batches

Problem Description

A students applied for admission in IB Academy. An array of integers B is given representing the strengths of A people i.e. B[i] represents the strength of ith student.

Among the A students some of them knew each other. A matrix C of size M x 2 is given which represents relations where ith relations depicts that C[i][0] and C[i][1] knew each other.

All students who know each other are placed in one batch.

Strength of a batch is equal to sum of the strength of all the students in it.

Now the number of batches are formed are very much, it is impossible for IB to handle them. So IB set criteria for selection: All those batches having strength at least D are selected.

Find the number of batches selected.

NOTE: If student x and student y know each other, student y and z know each other then student x and student z will also know each other.



Problem Constraints

1 <= A <= 105

1 <= M <= 2*105

1 <= B[i] <= 104

1 <= C[i][0], C[i][1] <= A

1 <= D <= 109



Input Format

The first argument given is an integer A.
The second argument given is an integer array B.
The third argument given is a matrix C.
The fourth argument given is an integer D.



Output Format

Return the number of batches selected in IB.



Example Input

Input 1:

 A = 7
 B = [1, 6, 7, 2, 9, 4, 5]
 C = [  [1, 2]
        [2, 3] 
       `[5, 6]
        [5, 7]  ]
 D = 12
Input 2:

 A = 5
 B = [1, 2, 3, 4, 5]
 C = [  [1, 5]
        [2, 3]  ]
 D = 6


Example Output

Output 1:

 2
Output 2:

 1


Example Explanation

Explanation 1:

 Initial Batches :
    Batch 1 = {1, 2, 3} Batch Strength = 1 + 6 + 7 = 14
    Batch 2 = {4} Batch Strength = 2
    Batch 3 = {5, 6, 7} Batch Strength = 9 + 4 + 5 = 18
    Selected Batches are Batch 1 and Batch 2.
Explanation 2:

 Initial Batches :
    Batch 1 = {1, 5} Batch Strength = 1 + 5  = 6
    Batch 2 = {2, 3} Batch Strength = 5
    Batch 3 = {4} Batch Strength = 4  
    Selected Batch is only Batch 1.


Solution ->

    int temp;
    public void makeGraph(int A,int C[][],ArrayList<ArrayList<Integer>> graph){
        for(int i = 0 ; i <= A ; i++){
            graph.add(new ArrayList<>());
        }
        for(int[] x: C){
            graph.get(x[0]).add(x[1]);
            graph.get(x[1]).add(x[0]);
        }
    }
    public void DFS(ArrayList<ArrayList<Integer>> graph, int src , int visited[],int []B){
        visited[src] = 1;
        temp += B[src-1];
        
        for(int child : graph.get(src)){
            if(visited[child] == 0){
                DFS(graph,child,visited,B);
            }     
        }
        visited[src] = 2;
    }
    public int solve(int A, int[] B, int[][] C, int D) {
        ArrayList<ArrayList<Integer>> graph = new ArrayList<>();
        int ans = 0;
        makeGraph(A,C,graph);
        int visited[] = new int[A+1];
        for(int i = 1 ; i <= A ; i++){
            if(visited[i] == 0){
                temp = 0;
                DFS(graph,i,visited,B);
                if(temp >= D){
                    ans++;
                }
            }
        }
        return ans;
    }

    
---------------------------------------------------------------------------------------------------------

Q1. Gym Trainer

Problem Description

You are the trainer of a gym and there are A people who come to your gym.

Some of them are friends because they walk together, and some of them are friends because they talk together.
But people become possessive about each other, so a person cannot walk with one friend and talk with another. Although he can walk with two or more people or talk with two or more people.

You being the trainer, decided to suggest each one of the 2 possible diets. But friends, being friends will always have the same diet as all the other friends are having.

Find and return the number of ways you can suggest each of them a diet.

As the number of ways can be huge, return the answer modulo 109+7.

NOTE: If there is any person who walks with one person and talks with the another person, then you may return 0.



Problem Constraints

1 <= A, N, M <= 105

1 <= B[i][0], B[i][1], C[i][0], C[i][1] <= A



Input Format

The first argument contains an integer A, representing the number of people.
The second argument contains a 2-D integer array B of size N x 2, where B[i][0] and B[i][1] are friends because they walk together.
The third argument contains a 2-D integer array C of size M x 2, where C[i][0] and C[i][1] are friends because they talk together.



Output Format

Return an integer representing the number of ways to suggest one of the two diets to the people.



Example Input

Input 1:

 A = 4
 B = [
       [1, 2]
     ]
 C = [
       [3, 4]
     ]
Input 2:

 A = 3
 B = [
       [1, 2]
     ]
 C = [
       [1, 3] 
     ]


Example Output

Output 1:

 4
Output 2:

 0


Example Explanation

Explanation 1:

 There are four ways to suggest the diet:
 Diet-1 to (1, 2) and Diet-2 to (3, 4).
 Diet-1 to (1, 2) and Diet-1 to (3, 4).
 Diet-2 to (1, 2) and Diet-1 to (3, 4).
 Diet-2 to (1, 2) and Diet-2 to (3, 4).
 
Explanation 2:

 Person 1 walks with person 2 and talks with person 3. So, we will return 0.


Solution ->

    public ArrayList<ArrayList<Integer>> makeGraphSide1(int A, int [][]B, ArrayList<ArrayList<Integer>> graph , int side[]){
        for(int i = 0 ; i <= A ; i++){
            graph.add(new ArrayList<>());
        }
        for(int[] x : B){
            graph.get(x[0]).add(x[1]);
            graph.get(x[1]).add(x[0]);
            side[x[0]] = side[x[1]] = 1;    
        }
        return graph;
    }
    public ArrayList<ArrayList<Integer>> makeGraphSide2(int A, int [][]C, ArrayList<ArrayList<Integer>> graph , int side[]){
        for(int[] x : C){
            if(side[x[0]] ==0 || side[x[0]] == 2 && side[x[1]] ==0 || side[x[1]] == 2){
                graph.get(x[0]).add(x[1]);
                graph.get(x[1]).add(x[0]);
                side[x[0]] = side[x[1]] = 2; 
            }else{
                return null;
            }   
        }
        return graph;
    }
    public void DFS(ArrayList<ArrayList<Integer>> graph, int[] side, int src){
        side[src] = 3;
        for(int x : graph.get(src)){
            if(side[x] != 3){
                DFS(graph,side,x);
            }
        }
    }
    public int solve(int A, int[][] B, int[][] C) {
        ArrayList<ArrayList<Integer>> graph = new ArrayList<>();
        int mod = 1000000007;
        int side[] = new int[A+1];
        graph = makeGraphSide1(A,B,graph,side);
        graph = makeGraphSide2(A,C,graph,side);
        if(graph == null){
            return 0;
        }
        int one = 0;
        
        for(int i = 1 ; i <= A ; i++){
            if(side[i] == 0 || side[i] == 1 || side[i] == 2){
                one++;
                DFS(graph,side,i);
            }
        }
        long ans = 1;
        for(int i = 0 ; i < one ; i++){
            ans = (ans*2)%mod;
        }
        // System.out.println(pow[one]);
        return (int)(ans);
    }

    
---------------------------------------------------------------------------------------------------------

Q2. Cows and snacks

The legendary Farmer John is throwing a huge party, and animals from all over the world are hanging out at his house. His guests are hungry, so he instructs his cow Bessie to bring out the snacks! Moo!

There are A snacks flavors, numbered with integers 1,2,…,A. Bessie has A snacks, one snack of each flavor. There are M guests and every guest has exactly two favorite flavors. The procedure for eating snacks will go as follows:

First, Bessie will line up the guests in some way.
Each guest in their turn will eat all remaining snacks of their favorite flavor. In case no favorite flavors are present when a guest goes up, they become very sad.
Help Bessie to minimize the number of sad guests by lining the guests in an optimal way.



Problem Constraints

2 <= A <= 100000
1 <= M <= 100000
1 <= B[i][0] , B[i][1] <= A
B[i][0] != B[i][1]



Input Format

First argument of input contains a single integer A.
Second argument of input contains a M x 2 integer matrix B denoting favorite flavors of each guest.



Output Format

Return a single integer denoting the ,minimum possible number of sad guests.



Example Input

Input 1:

 A = 5
 B = [ 
       [1, 2],
       [4, 3],
       [1, 4],
       [3, 4]
     ]
Input 2:

 A = 6
 B = [
       [2, 3],
       [2, 1],
       [3, 4],
       [6, 5],
       [4, 5]
     ]


Example Output

Output 1:

 1
Output 2:

 0


Example Explanation

Explanation 1:

 Bessie can order the guests like this: (3, 1, 2, 4). Guest 3 goes first and eats snacks 1 and 4. 
 Then the guest 1 goes and eats the snack 2 only, because the snack 1 has already been eaten.
 Similarly, the guest 2 goes up and eats the snack 3 only. All the snacks are gone, so the guest 4 will be sad.
Explanation 2:

 Bessie can order the guests like this: (1, 2, 3, 5, 4). So no-one will be sad. 


Solution ->

    class DSU{
    int[] parent;
    int[] size;
    int vtx;
    public DSU(int size){
        this.parent = new int[size+2];
        this.size = new int[size+2];
        this.vtx = size+2;

        for(int i = 0 ; i < this.vtx ; i++){
            this.parent[i] = i;
            this.size[i] = 1;
        }
    }
    int find(int v){
        if(v == parent[v]){
            return v;
        }
        return parent[v] = find(parent[v]);
    }
    void union(int a, int b){
        a = find(a);
        b = find(b);

        if(a != b){
            if(this.size[a] < this.size[b]){
                int temp = a;
                a = b;
                b = temp;
            }
            parent[b] = a;
            size[a] += size[b];
        }
    }
    
    }
    public class Solution {
    public int solve(int A, int[][] B) {
        DSU d = new DSU(A);
        int ans = 0;
        for(int x[] : B){
            int a = x[0];
            int b = x[1];
            if(d.find(a) != d.find(b)){
                d.union(a,b);
            }else{
                ans++;
            }
        }
        return ans;
    }
    }

    
---------------------------------------------------------------------------------------------------------

Q3. Maximum Depth

Problem Description

Given a Tree of A nodes having A-1 edges. Each node is numbered from 1 to A where 1 is the root of the tree.

You are given Q queries. In each query, you will be given two integers L and X. Find the value of such node which lies at level L mod (MaxDepth + 1) and has value greater than or equal to X.

Answer to the query is the smallest possible value or -1, if all the values at the required level are smaller than X.

NOTE:

Level and Depth of the root is considered as 0.
It is guaranteed that each edge will be connecting exactly two different nodes of the tree.
Please read the input format for more clarification.


Problem Constraints

2 <= A, Q(size of array E and F) <= 105

1 <= B[i], C[i] <= A

1 <= D[i], E[i], F[i] <= 106



Input Format

The first argument is an integer A denoting the number of nodes.

The second and third arguments are the integer arrays B and C where for each i (0 <= i < A-1), B[i] and C[i] are the nodes connected by an edge.

The fourth argument is an integer array D, where D[i] denotes the value of the (i+1)th node

The fifth and sixth arguments are the integer arrays E and F where for each i (0 <= i < Q), E[i] denotes L and F[i] denotes X for ith query.



Output Format

Return an array of integers where the ith element denotes the answer to ith query.



Example Input

Input 1:

 A = 5
 B = [1, 4, 3, 1]
 C = [5, 2, 4, 4]
 D = [7, 38, 27, 37, 1]
 E = [1, 1, 2]
 F = [32, 18, 26]
Input 2:

 A = 3
 B = [1, 2]
 C = [3, 1]
 D = [7, 15, 27]
 E = [1, 10, 1]
 F = [29, 6, 26]


Example Output

Output 1:

 [37, 37, 27]
Output 2:

 [-1, 7, 27]


Example Explanation

Explanation 1:

      1[7]
     /    \
   5[1]  4[37]
        /    \
       2[38]  3[27]

 Query 1: 
    L = 1, X = 32
    Nodes for level 1 are 5, 4
    Value of Node 5 = 1 < 32
    Value of Node 4 = 37 >= 32
    Ans = 37
Explanation 2:

      1[7]
     /    \
   2[15]  3[27]

 Query 1: 
    L = 1, X = 6
    Nodes for level 1 are 2, 3 having value 15 and 27 respectively.
    Answer = -1 (Since no node is greater or equal to 29).
 Query 1: 
    L = 10 % 2 = 0, X = 6
    Nodes for level 0 is 1 having value 7.
    Answer = 7.  


Solution ->

    int maxDept;
    
    public void makeGraph(int vertex, int[]B, int[]C,ArrayList<ArrayList<Integer>> graph){
        for(int i = 0 ; i <= vertex ; i++){
            graph.add(new ArrayList<>());
        }
        for(int i = 0 ; i < B.length ; i++){
            graph.get(B[i]).add(C[i]);
            graph.get(C[i]).add(B[i]);
        }
    }
    
    public void dfs(int node, int depth, ArrayList<ArrayList<Integer>> graph, int[] visited, ArrayList<ArrayList<Integer>> lvlWise, int[] D){
        visited[node]=1;
        if(lvlWise.size()==depth)
        {
            lvlWise.add(new ArrayList<>());
        }
        lvlWise.get(depth).add(D[node-1]);
        
        
        for(int child:graph.get(node))
        {
            if(visited[child]==0)
            {
                dfs(child, depth+1, graph, visited, lvlWise, D);
            }
        }
    }
    
    public int[] solve(int A, int[] B, int[] C, int[] D, int[] E, int[] F) {
        maxDept = 0;
        ArrayList<ArrayList<Integer>> graph = new ArrayList<>();
        ArrayList<ArrayList<Integer>> lvlWise = new ArrayList<>();
        int visited[] = new int[A+1];
        
        makeGraph(A,B,C,graph);
        visited=new int[A+1];
        
        dfs(1, 0, graph, visited, lvlWise, D);
        
        for(ArrayList<Integer> al : lvlWise)
        {
            Collections.sort(al);
        }
        maxDept=lvlWise.size()-1;
        
        int ans[] = new int[E.length];
        
        for(int i = 0 ; i < E.length ; i++){
            int level = E[i]%(maxDept+1);
            int find= F[i];
            int idx=Collections.binarySearch(lvlWise.get(level), find);
        
            if(idx<0)
            {
                idx=-idx;
                idx--;
            }
            
            if(idx>=lvlWise.get(level).size())
            {
                ans[i]=-1;
            }
            else
            {
                ans[i]=lvlWise.get(level).get(idx);
            }
        }
        return ans;
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


