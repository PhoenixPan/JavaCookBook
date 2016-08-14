
##In short: Java has pointers and is strictly pass-by-value.   
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
