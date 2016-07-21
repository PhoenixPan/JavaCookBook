

Though changes on ArrayList elements inside or outsiede should have the same effect, but not in cases of not-yet-initialized objects:

```
private FragmentStepCount fragmentStepCount;

list.add(fragmentStepCount);

System.out.println(list.get(0) == null) //true

fragmentStepCount = new FragmentStepCount();

System.out.println(list.get(0) == null) //still true, not changed

//Thus we need to 
list.set(0, fragmentStepCount);
        

```
