Differences between static and non-static classes?
1. 
2. 
3. 
4. 

## Nested Class
1. Inner class: Non-static nested class.  
2. A class within the body of another class or interface.  
3. Only a nested class can be a static class. The static class does not require the initialization of the outer class.    
4. Both normal and static nested classes require the reference of outer class.  
5. Normal nested class can access all members of the outer class while static nested class can only access static members of the outer class.  
6. An inner class instance cannot be created without an instance of outer class.  
  ```
  OuterClass outer = new OuterClass();
  OuterClass.InnerClass inner = outer.new InnerClass();
  ```
