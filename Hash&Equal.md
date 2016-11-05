If **one.equals(two)**, **one.hashCode** must equal to **two.hashCode**  
If one.hashCode = two.hashCode, it is **not necessary** that one.equals(two)



## hashCode()
Default implementation: memory address in integer value   
After override a hashCode() function, you can still get the original hash code by invoking:  
```
int originalHashCode = System.identityHashCode(myObject);
```


## equals(Object o)
```
public boolean equals(Object obj) {
    return (this == obj);
}
```


## ==
Returns true if and only if both variables refer to the same object, if their references are one and the same.


When using a hash-based Collection or Map such as HashSet, LinkedHashSet, HashMap, Hashtable, or WeakHashMap, make sure that the hashCode() of the key objects that you put into the collection never changes while the object is in the collection. The bulletproof way to ensure this is to make your keys immutable, which has also other benefits.  


## HashSet example
```
	public static void main(String[] args) {
		Emp emp1 = new Emp(23);
		Emp emp2 = new Emp(24);
		Emp emp3 = new Emp(25);
		Emp emp4 = new Emp(26);
		Emp emp5 = new Emp(27);
		
		HashSet<Emp> hs = new HashSet<Emp>();
		hs.add(emp1);
		hs.add(emp2);
		hs.add(emp3);
		hs.add(emp4);
		hs.add(emp5);
		
		Emp unwanted = new Emp(24);
		hs.add(unwanted);
		
		System.out.println("HashSet Size--->>>"+hs.size());
		System.out.println("hs.contains( new Emp(25))--->>>"+hs.contains(new Emp(25)));
		System.out.println("hs.remove( new Emp(24)--->>>"+hs.remove(new Emp(24)));
		System.out.println("Now HashSet Size--->>>"+hs.size());
		Iterator itr = hs.iterator();
		int count = 0;
		while  (itr.hasNext()) {
			itr.next();
			count++;
		}
		System.out.println(count);
      }
```
We have 
```
HashSet Size--->>>6
hs.contains( new Emp(25))--->>>false
hs.remove( new Emp(24)--->>>false
Now HashSet Size--->>>6
6
```
