# Section A
### 1

a

When you execute something synchronously, you wait for it to finish before moving on to another task. When you execute something asynchronously, you can move on to another task before it finishes.

Synchronous (one thread):
```
1 thread ->   |----A-----||-----B-----------||-------C------|
```
Synchronous (multi-threaded):
```
thread A -> |----A-----|   
                        \  
thread B ------------>   ->|-----B-----------|   
                                              \   
thread C ---------------------------------->   ->|-------C------| 
```
Asynchronous (one thread):
```

         A-Start ---------------------------------------- A-End   
           | B-Start ----------------------------------------|--- B-End   
           |   |     C-Start -------------------- C-End      |     |   
           V   V       V                           V         V     V      
1 thread-> |-A-|---B---|-C-|-A-|-C-|--A--|-B-|--C--|---A-----|--B--| 
```
Asynchronous (multi-Threaded):
```

 thread A ->     |----A-----|
 thread B ----->     |-----B-----------| 
 thread C --------->     |-------C----------
 ```
 http://stackoverflow.com/questions/748175/asynchronous-vs-synchronous-execution-what-does-it-really-mean
 
 b)
 
 
