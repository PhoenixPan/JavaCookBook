Thread passing from: Object - JVM - OS - Hardware  
Critical section: one part of the function that takes unnecessarily long time to complete and slow down the entire program.

## extends Thread or implement Runnable
Whether the object is a thread.  

## Synchronization  
Impose order on concurrent events
Methods: locks, synchronized, concurrent data structure, wait/notify, volatile  
```
synchronized(this) {
  // Take the lock of this object while block others from accessing
}

public synchronized int myMethod() {
  // Add a lock to the object. Equal to add a synchronized block outside the method
}

public synchronized static int myMethod() {
  // Add a lock to the class on static method
}
```

## volatile
No lock. Guranteed mutual exclusion from system, but looks like there is one.  
Understanding: so fast that no one can compete.  
volatile is good for flag variable, as the reading and writing on volatile variable are mutual exclusion.  

##### differences between volatile and lock:  
volatile allows only single read or write operation.  
synchronized is too heavy for one variable.  


## Deamon Thread
Set thread as deamond threads which will prevent JVM from exiting.  
JVM will exit only when there is no deamon threads.  
```
t3.setDaemon(true);
```

## Have a rest
#### yield()
Immediately give away the cpu time to other threads for a period
#### sleep(1)
#### wait()

## join() 
Let the main thread wait while executing another method  
```
t1.start();
t1.join();
```

## interupt()
A flag to instruct a thread to stop
```
if(t/this/Thread.interrupeted) // Whether the thread/method is interrupted
  return;

t1.interrupt() // interrupted = true
```

## start() and run()
Concurrent / sequential 
```
// run in sequence in only one thread
threadA.run();
threadB.run();

System.out.println();

// create a new thread, run at the same time by creating two different threads
threadA.start();
threadB.start();
```
output  
```
0000000000000000000000000000000000000000000000000011111111111111111111111111111111111111111111111111
0111111111111111111111111100000000000000000000000000000000000000000000000001111111111111111111111111
```


## ConcurrentHashMap
locks for get and put method? low efficiency  
One lock for each bucket.   
