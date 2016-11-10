# Q1: Element dedupilication in an array  
1. Use slow and fast pointers to distinguish processed and unprocessed elements;  

All elements on the left side of slow pointer (inclusive) will be returned.  
## Q1.1: Retain one of each in a sorted array  
```
public void deduplication(int[] input) {
  if (input == null || input.length <= 1)
    return input;
  
  int slow = 0;
  for (int fast = 0; fast < input.length; fast++) {
    if(input[fast] != input[slow]) {
      input[++slow] = array[fast];
     }
  }
  return Arrays.copyOf(input,slow + 1);
}
```
```
public void deduplication(int[] input) {
  if (input == null || input.length <= 1)
    return input;
  
  int slow = 1;
  for (int fast = 0; fast < input.length; fast++) {
    if(input[fast] = input[slow - 1]) {
      continue;
     }
     input[slow++] = input[fast];
  }
  return Arrays.copyOf(input, 0, slow);
}
```
## Q1.2: Retain N of each in a sorted array  
N = 2
```
public void deduplication(int[] input) {
  if (input == null || input.length <= 2)
    return input;
    int slow = 1;
    
  for (int fast = 2; fast < input.length; fast++) {
    if(input[fast] = input[fast - 2]) {
      fast ++;
    }
    else {
      input[++slow] = input[fast++]; // the result should including slow
    }
  }
}
```
## Q1.3: Retain no duplication
```
public void deduplication(int[] input) {
  if (input == null || input.length <= 1)
    return input;
  
  int slow = 0;
  int fast = 0;
  while (fast < input.length) {
    int begin = fast;
    while(fast < input.length && input[fsat] == input[begin]) {
      fast++;
    }
    if (fast - begin == 1) {
      input[slow++] = input[begin];
    }
  }
  return slow;
}
```
#Q2
## Q2.1: Use the least number of comparisons to find the largest and smallest number  
1 2 4 3 6 5 8 7  

Step1: Compare each adjacent pair, get a winning set and a losing set  
Number of comparision: N/2  
Step2: Find the largest from the winning set  
Number of comparision: N/2  
Step3: Find the smallest from the losing set  
Number of comparision: N/2  
Total: 1.5N

# Q2.2: Use the least number of comparisons to find the largest and the second largest number
Step1: Compare each adjacent pair, get a winning set and a losing set  
Step2: Find the largest from the winning set, add the losing elements to the winning element  
Step3: Find the largest element from those elements that lost to the largest  
8[2 7 4]
4[3 1]   8[2 7]
3[2] 4[1] 7[5] 8[2]
3 2 1 4 5 7 2 8  
N+log(N)

# Q3: 2D array print in spiral order or rotate  
剥洋葱: 4 for loops  

# Q4: BFS print binary tree  
BFS v.s. DFS  


## Q4.1: 
