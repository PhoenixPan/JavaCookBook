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
Record prefix  

## Q2: P
## Q3: Cut rope: Maximal Produt when Cutting Rope
Give a rope with integer length n, how to cut the rope into m integer length parts with length p[0], p[1], ..., p[m-1] in order to get the maximal product of p[0] * p[1] * ... * p[m-1]? m is determined by you and must be greater than 0 (at least one cut must be made)  
1. Base case: 1 meter rope
2. Induction rule:  
2 meters rope: M[2] = M[1] * 1  
3 meters rope:  
case 1:左大段 = 2  右小段 = 1  max(2, M[2]),1  // 左边一刀都不切的话
case 2:左大段 = 1  右小段 = 2  M[2],2  
M[4] = max(M[3] * 1, M[2] * 2, M[1] * 3)  

4 meters rope:  
case 1:左大段 = 3  右小段 = 1  M[3],1  
case 2:左大段 = 2  右小段 = 2  M[2],2  
case 3:左大段 = 1  右小段 = 3  M[1],3  
M[4] = max(M[3] * 1, M[2] * 2, M[1] * 3)  

## Q4: Edit distance
Given two strings of alphanumeric characters, determine the minimum number of Replace, Delete, and Insert operations needed to transform one string into the other.  
s1 = "xxxxxxxx"  size = i  
s2 = "yyyyyyyyyyyy"  size = j  


s1 = "asdf"
s2 = "sghj"
s1 = c1 | s1r   (char head | rest of the string)  
s2 = c2 | s2r  
```
if s1[n] = s2[n]  
 i - 1
 j - 1
```
