# Java Heap

## Question 1: Shuffling Cards  
Spade, heart, square, club  

1. Put a random card (random52) to the first (or last) position using swap.  p = 1/52  
2. Pick the second card from the second to the end the random51. P = 51/52 * 1/51 = 1/52  
this card was not selected during the 1st round: 51/52  
this card was selected during the 2nd round: 50/51  
3. Next loop: P = 51/52 * 50/51 * 1/50   
this card was not selected during the 1st round   
this card was not selected during the 2nd round   
this card was selected during the 3rd round  

Application: Select random k elements from a collection of size n  

##★Question 2: Select one random element from a collection of size n (O(1) space)  
1. Keep a length counter  
2. result = random(0, counter-1)  
3. if result == 0, replace the return value with the current element   

Mutation 1: Select random k elements  
if r < counter
solution[r] = current


Mutation 2: Select a random largest number's index  
1,2,6,3,4,4,6 (6, either 2 or 6)  
1. Keep variables:  
int return  
int max  
int max_counter  
2. Cases: 
If current < max, ignore  
If current == max; return = random(0,max_counter-1); max_counter++;  
If current > max, max = current;max_counter = 0;  


##Question 3: Design one random method based on another  
A: Design a Random(5) based on Random(7)  
Normalization: (1/7)/(5/7)
Time complexity: O(1)  

B: Design a Random(7) based on Random(5)  
1. Ascend dimension: Random(5) - 0 1 2 3 4 becomes:  
#★★★★★
 0  1  2  3  4  
 5  6  7  8  9  
10 11 12 13 14  
15 16 17 18 19  
20 21 22 23 24  
2. How to guarantee the probability of every number is 1/25?  
r1 = r2 = Random(5)
Random(25) = r1 * 5 + r2
3. %7
 0  1  2  3  4  
 5  6  0  1  2   
 3  4  5  6  0   
 1  2  3  4  5  
 6 21 22 23 24 (ignore)  
Time complexity: O(2) to infinity. Average: O()

Termination at iteration 1: P1 = 21/25 (excluding the last 4 number) * 2 (call twice)    
Termination at iteration 2: P2 = 21/25 (1-P1) (excluding the last 4 number) * 2^2 (call four times)   
Termination at iteration 3: P3 = 21/25 (1-P1)^2 (excluding the last 4 number) * 2^2 (call four times)   
...  
Expectation = P1 + P2 + P3...  

Mutation: Design a Random(1,000,000) based on Random(5)  
Let's start with Random(2)
binary system: Random(2)
To represent 1 million, 2^20 ---> Random(2)^20

## Question 4: Give an unlimited data stream, keep the medium of the numbers read so far  (O(N) space)
left half(knowing the largetst) | right half(knowing the smallest)  
max_heap                        | min_heap  
max_heap.top <= min_heap.top  

1. Case: If max_heap.size() == min_heap.size():  
If min_heap.top > current; min_heap.insert(current); return min_heap.top  
If max_heap.top <= current; max_heap.insert(current); return max_heap.top  
#★★★★★
2. Case: if max_heap.size() < min_heap.size():  
If min_heap.top > current; max_heap.insert(current); return (max_heap.top + min_heap.top)/2  
If min_heap.top <= current; min_heap.insert(current); max_heap.insert(current)  


Time complexity = O(LogN) (insert to heap)  
Space complexity = O(N)  

Mutation:  Infinite dataset:   
Part of data goes to hard drive:  
       max_heap           min_heap  
Total: 5000               5000  
Memory:1000               1000  
Disk:  4000               4000 (maintain the extreme value)  
if max_heap.top < disk_left.max, re-shuffle the memory and disk on left.  

## Question 5: Given a certain number(100000) of urls, how to find 95-th percentile of all url's length   
It's an over kill to use heap like Question 4.   
```
max = max(url.len)  
container[0];container[1];...container[max]  
for (int i = 0; i < max;i++)  
    counter += container[i]  
    if (counter >= 950000)  
      sysout(i)  
      return 
```

# Sort
## K-sort 
n array of n elements, where each element is at most k positions away from its regular position.  
The efficiency is better or equal to merge sort.   
Examples:  
1 2 3   k=0  
1 3 2   k=1  
3 2 1   k=2  
```
public void kSort(intp[] arr, int k) {
  PriorityQueue<Integer> heap = new PriorityQueue<>();
  for (int i = 0; i <= Math.min(k, arr.length - 1); i++) {
    heap.offer(arr[i]);
  }
  for (int i = 0; i < arr.length; i++) {
    if (i + k + 1 < arr.length)
      heap.offer(arr[i + k + 1])
    arr[i] = heap.poll();
  }
}
```
