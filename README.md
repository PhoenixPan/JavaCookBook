# JavaCookbook

## By topic:
- [Class](#Class)  
- [Generics](#Generics)  
- [Pass-by-value or pass-by-reference](#PassBy)   
- [Comparable and Comparator](#ComparableAndComparator)  
- [hashCode(), equals(), and ==](#hashCode&equals)  

<a id="Class"></a>  
## Class
1. One file can have multiple top-level class.
2. One file can have multiple public classes.
3. One file can only have one top-level public class.  

Differences between static and non-static classes?
1. 
2. 
3. 
4. 

### Helper Class
Non-public top-level class, usually used to support the public class.   

### Nested Class
1. A class within the body of another class or interface, either static or non-static.
  
  ```
  class Car {
    class Wheel {
    }
  }
  ```
  
2. **Inner class/Member class**: Non-static nested class.    
3. Only a nested class can be a static class. The static class does not require the initialization of the outer class. We usually use them when the inner class needs to be accessed outside.      
4. Both normal and static nested classes require the reference of outer class.  
5. Normal nested class can access all members of the outer class while static nested class can only access static members of the outer class.  
6. An inner class instance cannot be created without an instance of outer class.

  ```
  OuterClass outer = new OuterClass();  
  OuterClass.InnerClass inner = new OuterClass.InnerClass();  
  ```
  
7. Why do we prefer static nested class? inner classes require instances, which consume a lot of resources when the amount is large.  
8. Nested class can access private members of outer class.  

### Local Class
Can be created even in a method and to be used immediately. When the program quits the method, the class vanishes as well.   

### Anonymous Class
Create an instance without a class name.  
```
new Thread(new Runnable() {
  @Override
  public void run() {
    // do something
  }
}).start;
```

<a id="Generics"></a> 
## Generics
1. Only represent reference types, not primitive types
2. One method can have multiple generic types  
  ```
  public static <A, B> void myMthod() {}
  ```
3. Syntax: place before return type  
  ```
  public static <E> void myMthod2() {}
  public static <E> E myMthod3() {}
  ```  
4. To narrow the scale of E, use "extends" instead of "implements" even for interfaces  
  ```
  public static <E extends comparable<E> E myMthod4() {}
  ```   
  If you need to extend a class as well as implement an interface, class should be placed before interface  
  ```  
  public class MyClass<T extends classB & interfaceC> {}  
  ```  
  http://stackoverflow.com/questions/745756/java-generics-wildcarding-with-multiple-classes
  
##### Practice: Implement HashMap  

##### Example generic Stack Class
```
public class Stack<E extends Object> {

	private E[] stack;
	private int topIndex;
	
	public Stack() {
		stack = (E[])(new Object[6]);
		topIndex = -1;
	}
	
	public void push(E object) {
		if (topIndex == stack.length - 1) {
			E[] newStack = (E[])(new Object[stack.length * 2]);
			for (int i = 0; i < stack.length; i++) {
				newStack[i] = stack[i];
			}
			stack = newStack;
		}
		stack[++topIndex] = object;
	}
	
	public E pull() {
		if (topIndex == -1)
			throw new EmptyStackException();
		return stack[topIndex--];
	}
	
	public boolean isEmpty() {
		return topIndex == -1;
	}
	
	public static void main(String[] args) {
		String test = "t";
		Stack<String> stack = new Stack<>();
		int count = 0;
		while (count < 1000) {
			stack.push(test);
			count ++;
		}
		while (count > 0) {
			System.out.println(stack.pull());
			count --;
		}
	}
}
```

<a id="PassBy"></a> 
## Pass-by-value or pass-by-reference
**In short: Java has pointers and is strictly pass-by-value.**    
1. Pass-by-value: The actual parameter is fully evaluated and the resulting value is copied into a location being used to hold the formal parameter's value during method/function execution;  
2. Pass-by-reference: The formal parameter merely acts as an alias for the actual parameter. Anytime the method/function uses the formal parameter, it is actually using the actual parameter.  

Some say “In Java, Objects are passed by reference, and primitives are passed by value.” However, Objects are not passed by reference. A correct statement would be __Object references are passed by value__


For example, this does not change the original StringBuilder
```
static void foo(StringBuilder builder) {
    builder = new StringBuilder("ipad");    // refer to a new location
    builder.append("4");                    // change on new location
}
```
But this will
```
static void foo(StringBuilder builder) {
    builder.append("4");                    // operate on original StringBuilder
}
```
  
  
Though changes on ArrayList elements inside or outsiede should have the same effect, but not in cases of not-yet-initialized objects:

```
private Person john;
list.add(john);
System.out.println(list.get(0) == null) //true

john = new Person();
System.out.println(list.get(0) == null) //still true, not changed

//Thus we need to 
list.set(0, john);
```
<a id="ComparableAndComparator"></a> 
## Comparable and Comparator
### Comparable
```
public class ComparableDemo implements Comparable<ComparableDemo> {
	
	private int element = 0;
	
	@Override
	public int compareTo(ComparableDemo o) {
		if (this.element > o.element)
			return 1;
		else if (this.element == o.element)
			return 0;
		else
			return -1;
	}
}
```

### Comparator

```
import java.util.*;

class Car {

	int weight = 500;

	public Car(int weight) {
		this.weight = weight;
	}
}

class CarComparator implements Comparator<Car> {
	@Override
	/**
	 * Parameter type has to be the same class as declared above
	 */
	public int compare(Car c1, Car c2) {
		if (c1.weight > c2.weight)
			return 1;
		else if (c1.weight == c2.weight)
			return 0;
		else
			return -1;
	}
}

public class ComparatorDemo {

	public static void main(String[] args) {
		CarComparator cc = new CarComparator();
		Car c1 = new Car(400);
		Car c2 = new Car(800);
		System.out.println(cc.compare(c1, c2));

		ArrayList<Car> list = new ArrayList<>();
		Collections.sort(list, cc); // Collection, Comparator

		/**
		 * Another example from my project.
		 */

		// Get all followers' profiles from MySQL
		ArrayList<String[]> allProfiles = new ArrayList<>();

		// Sort the result according to ascending alphabet
		Collections.sort(allProfiles, new Comparator<String[]>() {

			@Override
			public int compare(String[] s1, String[] s2) {
				int response = 0;
				if (s1[0].compareTo(s2[0]) > 0) {
					response = 1;
				} else if (s1[0].compareTo(s2[0]) < 0) {
					response = -1;
				} else if (s1[0].compareTo(s2[0]) == 0) {
					if (s1[1].compareTo(s2[1]) > 0) {
						response = 1;
					} else if (s1[1].compareTo(s2[1]) < 0) {
						response = -1;
					}
				}
				return response;
			}
		});

	}

}
```
<a id="hashCode&equals"></a> 
## hashCode(), equals(), and == 
1. hashCode(): Default implementation: return an integer representing a *memory address*. Return a different hash code for distinct objects. After override a hashCode() function, you can still get the original hash code by invoking:  
	```
	int originalHashCode = System.identityHashCode(myObject);
	```

2. equals(Object o): is essentially ==:  
	```
	// Java default implementation
	public boolean equals(Object obj) {
	    return (this == obj);
	}
	```

3. ==: Returns true **if and only if** both variables refer to the same object, if their references are one and the same

### Contract
You must override hashCode() in every class that overrides equals(). Failure to do so will result in a violation of the general contract for Object.hashCode(), which will prevent your class from functioning properly in conjunction with all hash-based collections, including HashMap, HashSet, and Hashtable.  

If **one.equals(two)**, **one.hashCode** must equal to **two.hashCode**   
If one.hashCode = two.hashCode, it is **not necessary** that one.equals(two)   

### Why
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

### HashSet example
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
```

