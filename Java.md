# Stack and Heap
In Java, memory comprised of stack and heap.  
stack: local variables 当前执行状态  
heap: dynamic elements, such as new object 动态分配的object(new出来的)     
stack        heap  
Jack  -> name = "Jack"  

# Array
1. Occupies consecutive memory  
2. Can access elements via index in O(1) time  
```
int[] array;
// Valid
array = new int[] {1,2,3};
// Invalid
array = {1,2,3};
```

```
// Valid
int[][] 2darray = new int[5][]
// Invalid
int[][] 2darray = new int[][]
```
stack                heap        
int[] array  -> {0,0,0} length=3    
             point to  


##### 2D array  
Not necessary consecutive between dimensions  
<img src="https://cloud.githubusercontent.com/assets/14355257/20873582/d0c7bc28-ba76-11e6-9063-e3a12746f98b.png" width="225" height="300" />
               
