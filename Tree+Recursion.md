1. What do you expect from l/r nodes?
2. What do you want to do with current layer?
3. What do you want to report upward?

## Q1.Whether a binary tree is balanced?  

### Q1.1
Old method: O(ologn) Photo  
### Q1.2
New method: O(n) Photo     Trace down and then trace up  
### *Q1.3  
### *Q1.4
to understand 

## Q2. Path problem
1. 人字形path (leaf to parent to another leaf)
2. 直上直下的path

### Q2.1
recursive:  
helper(Node root, int[] max, int sum)  
### Q2.2
1. Hyper function
One path -5, 11, 6  
Find target = 17  
2. Hash set (no need to look back)  
HashSet = {-5, 6, 12}  
exist? + target = current // Does this have a solution? if so, 17 exists  
Time, Space: O(n)

### Q2.3
Find the max sum in the tree  
Three: -5 2 11 6 14: 11 + 14 = 25  
1. Hyper function  
One path -5, 11, 6  
Find target = 17  
