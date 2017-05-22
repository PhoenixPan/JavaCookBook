## Compile and run from cmd
1. Set environment variable JAVA_HOME of JDK location and add path %JAVA_HOME%\bin
2. Compile and execute .java with extra jar
 ```
 javac -cp .;h:\app\lib\mysql-connector-java-5.1.41-bin.jar Test.java
 java -cp .;h:\app\lib\mysql-connector-java-5.1.41-bin.jar Test
 ```

## Copy an array
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

## Enum
A fixed set of constants, such as months, states, and cards:   
```
pubic class Card {
  private enum Suit {SPADE, HEART, DIAMOND, CLUB;}
  public static void main(String[] args) {
    System.out.println(Suit.CLUB); // Show "CLUB"
  } 
}
// Or declare here
```
(enum types must not be local)  


```
public class News {
  public static void main(String[] args) {
    System.out.println(NewsFeed.SITE1.getUrl());
  }
}

enum NewsFeed {
  SITE1("http://www.test1.com"),
  SITE2("http://www.test2.com"),
  SITE3("http://www.test3.com"); // notice: "," and ";"
  
  private String url; 
  
  private NewsFeed(String url) {
    this.url = url;  // "this" could be "SITE1", "SITE2", or "SITE3" 
  }
  public String getUrl() { // url getter. If url is public then we don't need it
    return this.url;
  }
}
```

## Declaration Order
1. The order of methods doesn't matter.  
2. The order of variables matter.

  ```
  //error: cannot find symbol
  int sum = 0;
  int a = 5;
  sum = a + b;
  int b = 6;
  System.out.println(sum);
  ```



#### Protected: same package + subclasses from other packages. Less than Public, more than default.
1. Final class cannot be extended
2. Final methods cannot be overridden
3. Final variable cannot be re-assigned
