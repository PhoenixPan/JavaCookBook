# Basic
1. Define the meaning of each element and then fill up the entire structure (bottom-up or top-down)
2. Usually more efficient than recursion (such as in Fibonacci)
3. Induction rule

# Type One
1. Calculate MAX or MIN using a group of original data
2. Linear scan and look back to the previous elements
3. Example: Longest ascending array, cut rope, etc.  

## Largest sum of a subarray
Input: (-1, 2, 4, -1, -2, 10, -1)  
Output: (2, 4, -1, -2, 10)  
M[i] represents the largest sum from the 0 to i-th element  
M[i] = input[i] + M[i-1]   if(M[i-1]>0)
       input[i]            otherwise
       
Input: (-1, 2, 4, -1, -2, 10, -100, 10, 100)  
How to return the left/right index of the solution?  
```
int sum = 0;
int start = 0;
int end = 0;
int max = 0; 
if (sum < 0)
  reset both start and end to next // after -100, set to 10
if (max.update) // If update, change solutionStart/End
  solutionStart = start;
  solutionEnd = end;
int solutionStart = 0;
int solutionEnd = 0;
```

# Cut something
## Q1: Dictionary Word Problem
For an arbitary input, can it be made up by using the words in the dictionary?
bob  
cat  
rob  
Input: "bobcatrob"  
case 1: no cut, check "bo" from the dict  
case 2: b: 左大段[1] tells you whether it is true or false   右小段 manual check from dict  



