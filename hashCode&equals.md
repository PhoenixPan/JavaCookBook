# hashCode & equals functions

## Basic

### .hashCode()
Default implementation: return an integer representing a *memory address*  
Return a different hash code for distinct objects  
After override a hashCode() function, you can still get the original hash code by invoking:  
```
int originalHashCode = System.identityHashCode(myObject);
```

### .equals(Object o)
```
public boolean equals(Object obj) {
    return (this == obj);
}
```

### Double equal signs: ==  
Returns true if and only if both variables refer to the same object, if their references are one and the same.

## Contract
You must override hashCode() in every class that overrides equals(). Failure to do so will result in a violation of the general contract for Object.hashCode(), which will prevent your class from functioning properly in conjunction with all hash-based collections, including HashMap, HashSet, and Hashtable.  

If **one.equals(two)**, **one.hashCode** must equal to **two.hashCode**   
If one.hashCode = two.hashCode, it is **not necessary** that one.equals(two)   

## Why
Hashing retrieval is a two-step process.  
1. Find the right bucket (using hashCode())  
2. Search the bucket for the right element (using equals() )  

When using a hash-based Collection or Map such as HashSet, LinkedHashSet, HashMap, Hashtable, or WeakHashMap, make sure that the hashCode() of the key objects that you put into the collection never changes while the object is in the collection. The bulletproof way to ensure this is to make your keys immutable, which has also other benefits.  

You may have the same hash code for different objects after your implementation, 

```
// This is true in default implementation  
Student s1 = new Student("John", 18);
Student s2 = new Student("John", 18);
s1.hashCode() != s2.hashCode();
```

## HashSet example
HashSet checks equality based on equals() method  
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
```
class Emp 
{
	private int age ;
	
	public Emp( int age )
	{
		super();
		this.age = age;
	}
	
	public int hashCode()
	{
		return age;
	}
	
	// Critical to hash functions
//	public boolean equals( Object obj )
//	{
//		boolean flag = false;
//		Emp emp = ( Emp )obj;
//		if( emp.age == age )
//			flag = true;
//		return flag;
//	}
	
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
