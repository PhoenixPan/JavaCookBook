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
