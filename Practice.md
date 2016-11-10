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
