Why DFS? 
save space.  


## Q1: Find all subsets of a set  
<img width="636" alt="dfs" src="https://cloud.githubusercontent.com/assets/14355257/20113669/5d6554aa-a5bf-11e6-9d60-0299db53d260.png">
Meaning of each level: whether to add or not add this element into each subset.  

```
void findSubset(String input, int index, String solution)
  if(index == input.length()) 
    if (solutio.size() == 0)
      print "empty"
    else
      print solution
   return

  solution.append(intput.at(index))
  findSubset(input, index+1, solution)
  solution.delete_last(intput.at(index))

  findSubset(input, index+1, solution)
```
**Time Complexity = O(2^N)**

## Q2: Find all valid permutation pairs (n) using parenthesis provided
Left parenthesis added >= Right parenthesis added  
```
DFS {
  if (r == n && l == n)
    return solution
  if (l<n)
    solution += (
    DFS
    solution.remove_last
  if (r<l)
}
```
