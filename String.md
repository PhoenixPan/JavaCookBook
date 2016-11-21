# Frequent topics:  
1. Removal: a particular or multiple spaces
2. Deduplication
3. Replacement: replace spaces with "20%"
4. Reversal(Swap): I love you -> you love I
5. Substring: regular, Robin-Carp(hash-based, O(n)), KMP

6. Move letters: ABCD1234 -> A1B2C3D4
7. Permutation: use DFS
8. Encoding/decoding: aaabcc -> a4b1c2
9. Longest substring that contains only unique chars
10. Matching


## General
1. Do not change the string when you are using its length

## 1.Removal

#### Q: Remove particular chars   
Fast/slow pointers: i = slow, j = fast   
i: all elements on left are processed  
j: current index to remove. All elements between i and j do not matter  
[j,size-1]: unknown area  

```
if current != target
  i++;
  j++;
else
  // i don't move
  j++;
  copy j to i
```
Time: O(n) Space:O(1)

#### Q: Remove leading and duplicated spaces
input = "___abc__ed__ef__"  
output = "abc_ed_ef"  
