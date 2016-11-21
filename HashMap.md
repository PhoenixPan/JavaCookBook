# HashTable(HashMap)
Wikipedia: https://en.wikipedia.org/wiki/Hash_table   
  
1. Space, search, insert, delete: average time complexiy is O(1), worst O(n), due to hash collision.  
2. Collision resolution:  
  separate chaining:   
    Insert complexity: O(1) with a known tail pointer  
    Insert complexity: O(n) if we need to check duplication  
    Delete: O(n)  
    


Sort an HashMap using its value  
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
