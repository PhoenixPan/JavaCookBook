
Thread passing from: Object - JVM - OS - Hardware  


## Deamon Thread
Set thread as deamond threads which will prevent JVM from exiting
JVM will exit only when there is no deamon threads.  
```
t3.setDaemon(true);
```
## join() 
Let the main thread wait while executing another method  
```
t1.start();
t1.join();
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
