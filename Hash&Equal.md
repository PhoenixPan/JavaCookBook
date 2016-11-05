If **one.equals(two)**, **one.hashCode** must equal to **two.hashCode**  
If one.hashCode = two.hashCode, it is **not necessary** that one.equals(two)



## hashCode()
Default implementation: memory address in integer value   

## equals()
```
public boolean equals(Object obj) {
    return (this == obj);
}
```
## ==
Returns true if and only if both variables refer to the same object, if their references are one and the same.


When using a hash-based Collection or Map such as HashSet, LinkedHashSet, HashMap, Hashtable, or WeakHashMap, make sure that the hashCode() of the key objects that you put into the collection never changes while the object is in the collection. The bulletproof way to ensure this is to make your keys immutable, which has also other benefits.  
