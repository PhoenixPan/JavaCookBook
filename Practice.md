# Q1: Element dedupilication in an array  
1. Use slow and fast pointers to distinguish processed and unprocessed elements;  


## Q1.1: Sorted array

```
public void deduplication(int[] input) {
  if (input == null || input.length <= 1)
    return input;
  
  int slow = 0;
  for (int fast = 0; fast < input.length; fast++) {
    if(input[fast] = input[slow - 1]) {
      continue;
     }
  }
  return Arrays.copyOf(input, slow + 1);
}
```

