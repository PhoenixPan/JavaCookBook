# Java PriorityQueue
1. Object implements comparable interface (compareTo). Define the natural order (the order defined by comparable).   
  ```
  PriorityQueue<E> minHeap = new PriorityQueue()  // Default capacity = 11
  PriorityQueue<E> minHeap = new PriorityQueue(size) 
  PriorityQueue<E> maxHeap = new PriorityQueue(size, Collections.reverseOrder()) // Can only reverse natural order
  ```
2. Object implements comparator interface (compare). Dfine the order of objects using user-identified rules.  
  ```
  PriorityQueue<E> minHeap = new PriorityQueue(size, new Comparator<E>())
  ```
3. When comparator is provided, the order is decided by the comparator rather than the comprable  
4. Initial size > 0, IllegalArgumentException



# Java Heap

1. Don't change input!  
2. Online: Give a streaming input, if the stream stops, the algorithm should give the correct result of the data up to now  
3. Offline: Give the entire input and generate the result
4. Not only look at the time complexity but also unit time spent on each operation (whether it's I/O or memory, efficiency 1:1000)

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
## Counting Sort

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
## Bucket Sort  
```
// Code on photo
(int)(n * d) // distribute elements to buckets 
```
Uniformly distribution (one element in each bucket): O(4n) -> O(n)  
Worst case (all in one bucket): mergeSort, O(nlogn); insertionSortO(n^2) (Collections.sort())  


## External Sort (I/O optimization)
ArrayList: continuous I/O, good for I/O  
LinkedList: random I/O, not good for I/O, but save RAM space (not useful here)  
Disk seek: slow. Find the area storing data.  
Disk read: fast. Disk only rotates 1~2 degrees, but the head will move in and out to read the entire area.  
Why reduce I/O? Hard drive operations are much slower than RAM operations.  
  
Sort 10 billion integer data with 4G RAM  
one int = 4 bytes  
10 b int = 40 Gb  
We usualy can use only half of the RAM  
Merge: Divide the dataset to 20 pieces, each 2 Gb, and sort each chunk.   
Sort: Read 0.1 Gb each time.  
Optimized algorithm: two times data size (80 Gb I/O) wish O(1) disk seeks.  
  

# K-elements

1. Binary reduction: so many I/O (logk) between each stage (if the dataset is too large to be put in memory)
  * A1 A2 -> A12  A3 A4 -> A34  <-1|2->  A12 A34 -> A14
  * Time = O(nk * log(k))
2. minHeap(): only one I/O for each element (n)   
  * check the smallest element of each A, output[n] = Ak[n]
  * TIme = O(nk^2)
  * A1 (n times) A2 (n times) A3 (n times) A4 (n times)    output.size = k
3. Optimized minHeap()
  * Instead of liner for loop, make it log
  * Time = O(nk * logk)
  ```
  class BetterHeap {
    int indexWithInArray;     // e.g. = 4 The 5th position in array
    int indexFromWhichArray;  // e.g. = 3 In array A3
  }
  ```

# Binary Search Tree
1. Find (the closest value):  traverse the tree
  * Case 1: if targetValue < currentValue -> update solution -> current = current.left
  * Case 2: if targetValue > currentValue -> update solution -> current = current.right
  * Case 3: if targetValue == currentValue -> return 
2. Find (the largest element that is smaller than target):
  * Case 1: if targetValue <= currentValue -> current = current.left
  * Case 2: if targetValue > currentValue -> update solution -> current = current.right 
3. Remove: 
  * Case 1: if target node is a leaf node, delete
  * Case 2: if target node has only one child, replace it with its child
  * **Case 3**: if target node has two node, replace it with the largest element in left tree or the smallest one in right tree, which may have a left or right tree (**recrusive on this node!**) 
    ```
    // On photo
    // Return type is TreeNode!!
    ```
4. Insert:  
  * Case 1: if targetValue < currentValue -> previous = current -> current = current.left
  * Case 2: if targetValue > currentValue -> previous = current -> current = current.right
  * Case 3: if current == null  previous.left(or right) = current
  
# DP
Question on photo  
Get the minimum cost  
中心开花 split from the middle   
Base case: the shortest piece that cannot be cut
If size = 1 piece, no cut needed   
M[0][1] = 0   
M[1][2] = 0   
M[2][3] = 0  
M[3][4] = 0  

If size = 2 pieces, each case has one way to cut   
M[0][2] =   
M[1][3] =  
M[2][4] =  

If size = 3 pieces, each case has two ways to cut   
M[0][3] =  
M[1][4] =  

M[0][3]= min(case1, case2) = min(12, 11) = 11  

k = possible cutting places  
