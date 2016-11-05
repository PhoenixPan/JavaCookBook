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
