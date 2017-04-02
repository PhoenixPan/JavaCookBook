## Class
1. One file can have multiple top-level class.
2. One file can have multiple public classes.
3. One file can only have one top-level public class.  

Differences between static and non-static classes?
1. 
2. 
3. 
4. 

## Helper Class
Non-public top-level class, usually used to support the public class.   

## Nested Class
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

## Local Class
Can be created even in a method and to be used immediately. When the program quits the method, the class vanishes as well.   

## Anonymous Class
Create an instance without a class name.  
```
new Thread(new Runnable() {
  @Override
  public void run() {
    // do something
  }
}).start;
```
