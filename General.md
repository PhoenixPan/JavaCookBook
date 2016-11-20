##Copy an array
```
BigInteger[] currentKey = new BigInteger[7];
System.arraycopy(w, k * 7, currentKey, 0, 7);
```

## Default toString()  
ObjectType@Address  

## Graph
#### Check visited node!!

Directed: |E| = |V|^2  
Undirected: |E| = |V|*(|V|-1)/2 + |V|  
Equal matrix: G(i,j) = G(j,i)  

For both directed and undirected:  
  Speace Complexity   
    Adjacency Matrix O(V^2)   
    Adjacency List O(V+E)  
    Which one is better for sparse?  
  How expensive it is to find (u, v) belongs to E?  
    Adjacency Matrix O(1)  
    Adjacency List O(degree(u)) (O(1) to find node and dig in)  
      Dense worst: O(V)  
      Sparse: O(1)  
For undirected:  
  How expensive it is to compute the degree of a node?  
    Adjacency Matrix O(V)   
    Adjacency List O(degree(u))    
For directed:  
  How expensive it is to compute the out degree of a node?  
    Adjacency Matrix O(V)   
    Adjacency List O(degree(u))    
  How expensive it is to compute the in degree of a node?  
    Adjacency Matrix O(V)   
    Adjacency List O(V+E)    
