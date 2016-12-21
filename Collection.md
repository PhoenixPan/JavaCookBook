## Iterator
next()  
hasNext()  
remove(): An optional operation, remove the last element returned by this iterator.    
```
String text = it.next();
it.remove();
```
Avoid: list.get(i) might be very slow: O(n)  
```
for(int i = 0; i< list.size(); i++) {
  System.out.println(list.get(i));
}
```
Encourage: list must implement iterable, so you are using iterator, which is usually not O(n)  
```
for(Integer i : list) {
}
```

##### ListIterator(Java)
Lies between two elements, can either go next() or previous(), returns the value it travels through.    
### Write a tree iterator


# HashTable(HashMap)
Wikipedia: https://en.wikipedia.org/wiki/Hash_table   

1. Load factor should be kept in a reasonable range. If it's too large, the efficiency of the map will dreases; If it's too small, it wastes memory 
2. Space, search, insert, delete: average time complexiy is O(1), worst O(n), due to hash collision
3. Collision resolution: endanger the efficiency of hashtable when the number of buckets are small
  * Separate chaining(closed addressing/open hashing): Use a structure (LinkedList) to deal with small number of elements. If the number of elements in each bucket is too large, the hashing function needs to be fixed.    
  Insert: O(1) with a known tail pointer  
  Insert: O(n) if we need to check duplication  
  Delete: O(n)  
  * Open addressing/closed hashing: worst case O(n) when the table is almost full  
  * When to use which one? Open addressing is better used for hash tables with small records that can be stored within the table (internal storage). If the table is expected to have a high load factor, the records are large, or the data is variable-sized, chained hash tables often perform as well or better.
4. Difference between HashMap and HashTable in Java
  * HashTable is thread safe whereas HashMap is not but the result is that HashTable has a much lower performance
  * HashTable does not allow null key


## Q: Find top N most frequent words.
Step 1: Use HashMap to sort the frequency of all words  
Step 2: Use a min_head to find the top k words
  ```
  if (minHeap.top < value){ min_heap.pop(); minHeap.insert(value)};
  else {//do nothing};
  ```
Step 3: Time complexity: O(n) + O(nlogk) = O(nlogk), k = minHeap.size()  

## Q: Find a missing number from 1 to n in an unsorted array. Time complexy: O(n)   
Solution 1: Sort and iterate.  Time: O(nlogn) Space:O(1)  
Solution 2: HashMap. Time: O(n) Space:O(n). Con: Space occupation
Solution 3: Get sum. Sum (1+n)n/2 - RealSum.  等差数列. Time: O(n) O(1). Con: May cause overflow is the sum is too large.
Solution 4: XOR. For loop (each element with n), if the result is not 0, that's the missing number. Time: O(n) Space:O(1)

## Q3: Find common numbers between two sorted arrays  
**Assumption**: Integers? Duplication? Size of array? 

1. Solution 1: if n ~ m, two pointers. Time: O(m+n) Space:O(1)
2. Solution 2: if n <<< m
  * binary search in array b[m]. Time: O(n log(m)) perform n times binary searches
  * HashSet: put a[n] into HashSet (smaller to save space). Time: O(m+n) Space: O(min(n, m))


## Function: Sort an HashMap using its value  
```
import java.util.Collections;
import java.util.Comparator;
import java.util.LinkedList;
import java.util.Map.Entry;
import java.util.TreeMap;

public class SortTest {

	/**
	 * Introduction
	 * 
	 * Sometimes we love to store our key-vale pairs into a map, and we want to
	 * sort the map both by key and by value. I believe you will fall in love
	 * with TreeMap.navigableKeySet()(ascending) and TreeMap.descendingKeySet(),
	 * but how to get entrySet by value?
	 * 
	 * Implementation
	 * 
	 * Make best use of Collections.sort(). The idea is learnt from mkyong - How
	 * to sort a Map in Java. Show me the code
	 * 
	 * @param args
	 */

	public static void main(String[] args) {
		TreeMap<K, V> treeMap = new TreeMap<K, V>();
		LinkedList<Entry<K, V>> linkedList = new LinkedList<Entry<K, V>>(treeMap.entrySet());
		Collections.sort(linkedList, new Comparator<Entry<K, V>>() {
			public int compare(Entry<K, V> thisEntry, Entry<K, V> thatEntry) {
				// by value in descending order
				int cmp = -thisEntry.getValue().compareTo(thatEntry.getValue());
				if (cmp != 0)
					return cmp;
				// break value tie by key in ascending order
				else
					return thisEntry.getKey().compareTo(thatEntry.getKey());
			}
		});

		for (Entry<K, V> entry : linkedList) {
			// play with entry.getKey() and entry.getValue()
		}
	}

}
```
  
If you're only interested in the keys, you can iterate through the keySet() of the map:
```
Map<String, Object> map = ...;

for (String key : map.keySet()) {
    // ...
}
```
If you only need the values, use values():
```
for (Object value : map.values()) {
    // ...
}
```
Finally, if you want both the key and value, use entrySet():
```
for (Map.Entry<String, Object> entry : map.entrySet()) {
    String key = entry.getKey();
    Object value = entry.getValue();
    // ...
}
```

If you want to remove items mid-iteration, you'll need to do so via an Iterator

```
public static void printMap(Map map) {
    Iterator it = map.entrySet().iterator();
    while (it.hasNext()) {
        Map.Entry pair = (Map.Entry)it.next();
        System.out.println(pair.getKey() + " = " + pair.getValue());
        it.remove(); // avoids a ConcurrentModificationException, not reusable
    }
}
```

http://www.sergiy.ca/how-to-iterate-over-a-map-in-java

http://stackoverflow.com/questions/1066589/iterate-through-a-hashmap
