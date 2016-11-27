Differences between static and non-static classes?
1. 
2. 
3. 
4. 

## Nested Class
1. A class within the body of another class or interface, either static or non-static.  
2. **Inner class/Member class**: Non-static nested class.  
3. Only a nested class can be a static class. The static class does not require the initialization of the outer class.    
4. Both normal and static nested classes require the reference of outer class.  
5. Normal nested class can access all members of the outer class while static nested class can only access static members of the outer class.  
6. An inner class instance cannot be created without an instance of outer class.  
  ```
  OuterClass outer = new OuterClass();  
  OuterClass.InnerClass inner = new OuterClass.InnerClass();  
  ```
7. Why do we prefer static nested class? inner classes require instances, which consume a lot of resources when the amount is large.  

## Local Class
Can be created even in a method and to be used immediately. When the program quits the method, the class vanishes as well.  
