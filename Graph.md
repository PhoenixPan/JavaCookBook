## Graph

#### Notice: Check visited node!!

Directed: |E| = |V|^2  
Undirected: |E| = |V|*(|V|-1)/2 + |V|  
Equal matrix: G(i,j) = G(j,i)  

For both directed and undirected:  
* Speace Complexity    
  * Adjacency Matrix O(V^2)   
  * Adjacency List O(V+E)  
  * Which one is better for sparse?  
* How expensive it is to find (u, v) belongs to E?  
  * Adjacency Matrix O(1)  
  * Adjacency List O(degree(u)) (O(1) to find node and dig in)  
    * Dense worst: O(V)  
    * Sparse: O(1)  

For undirected:  
* How expensive it is to compute the degree of a node?  
  * Adjacency Matrix O(V)   
  * Adjacency List O(degree(u))    

For directed:  
* How expensive it is to compute the out degree of a node?  
  * Adjacency Matrix O(V)   
  * Adjacency List O(degree(u))    
* How expensive it is to compute the in degree of a node?  
  * Adjacency Matrix O(V)   
  * Adjacency List O(V+E)    

# Breadth-First Search (BFS)
1. zig-zag
2. is not for the shortest distance

# Best First Search (BFS)
## Dijkstra
Find the shortest node from a single node to any other node in the graph  

### Q1
Given a matrix of size NxN and for each row and each column the elements are sorted in ascending order. How to find the Nth smallest element in it?  
12345  
23456  
34567  
45678  
56789  



# Depth-First Search (DFS)
