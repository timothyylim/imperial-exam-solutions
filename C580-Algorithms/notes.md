# Introduction 

- Binary Search
  - Pseudocode
  ```
  Binary Search (Input: list L, value k)
    - Repeat while there are elements to search
      - Choose element e near middle of the list
      - if e == k, return True 
      - else if k > e continue searching after e
      - else search before e
    - return False
  ```
  python
  ```
  	def binarySearch(alist, item):
    first = 0
    last = len(alist)-1
    found = False

    while first<=last and not found:
        midpoint = (first + last)//2
        if alist[midpoint] == item:
            found = True
	        else:
	            if item < alist[midpoint]:
	                last = midpoint-1
	            else:
	                first = midpoint+1
	
	    return found
  ```
  - Worst-case analysis
  ```
  T(N) = Theta(log2(N))
  ```
  

# Sorting

- Insert Sort 
  - Pseudocode
  ```
  Insert Sort (Input: sequence A = (a1,...,an))
  for each element a[i] in A
    j == i
    while j > 1 and a[j] < a[j-1]
      swap a[j] and a[j-1]
      j --
  return
  ```
  python
  ```
  def insertionSort(a):
   for index in range(1,len(a)):

     currentvalue = a[index]
     position = index

     while position>0 and a[position-1]>currentvalue:
         a[position]=a[position-1]
         position = position-1

     a[position]=currentvalue
  ```
  - Worst-case analysis
    - Reverse sorted array would take Theta(N^2)
  - Average time?
    - O(N^2), even the average case increases by a factor of N  
  
- Merge Sort 
  - Pseudocode
  ```
  Merge Sort(Input: sequence A = (a1...an) where N>=1)
  if length of A is 1: return
  
  a = MergeSort(a[1]...a[N/2])
  b = MergeSort(a[N/2]...a[N])
  return Merge(a,b)
  ```
  - Worst-case analysis
    - T(N) = Theta(Nlog2N)
  - How does it compare to insert sort?
    - Faster for large unsorted lists 
    - Slower for lists that are already sorted or for small lists
  
- Quick Sort 
  - Pseudocode
  ```
  Quicksort (Input: sequence A = a1, . . . , aN)
  
  if A has more than one element
  	p = Partition A 
  	Quicksort (a[0]...a[p-1])
  	Quicksort (a[p+1]...a[n])
  else return
  ```
  
  ```
  Partition (Input: A = (a[0]...a[n]))
  choose pivot p from A
  swap p and a[n]
  storeIndex = 1
  for each a in (a[0]...a[n-1])
  	if a < p
  		swap a and A[storeindex]
  		sotreIndex++
  swap a[n] and a[storeIndex]
  return storeIndex
  ```
  - Worst-case analysis
  - Strategies to avoid O(N^2) 

# Dynamic Data Structures

- Stack
  - Amortised runtime = T(N) = 3Nc-c 

- Queue 

- Binary Heap Implementation of a Priority Queue 
  - Pseudocode for add(key k, data d)
  ```
  add(key k, data d)
    - insert new node n = (k,d)
    - while k > key of n's parents
      - swap n with its parents
    return 
  ```
  - Pseudocode for remove
  ```
  remove
    - Store top node
    - n = (k,d)
    - while k < key of any child of n
      - swap n with child of highest key 
  ```
  - dynamic array
    - parent of a[n] is a[n/2]
    - children of a[n] are [2*n] and a[2*n+1]
- Sets


- Trees
  
- Binary Search Tree
  - Definition
    - all keys in left subtree are less or equal to root key and all keys in the right subtree are greater or equal to the root key 
  - Performance 
    -  

- Hash Tables
  - Collision resolution
    - Chaining (worst case is when all keys hash to the same value O(N)
      - Average time is O(N/m) 
    - Probing
      - Probe until a space is found  


# Graphs

- BFS
  - Pseudocode
  ```
  BFS (given graph g and source vertex s)
  initialize Q = <s> of verticies
  while Q is not empty
    remove vertex u from Q
    for each vertext that has an edge {u,v}
      if v is not yet visited
        mark v as visited 
        add v to Q
  ```
  - Shortest Path pseudocode
  ```
  BFS Shortest Paths(input: graph G = (V,E), source vertex s)
  Initialise a Q = <s> of verticies
  dist = <d1,...,dv> = <inf,...,inf>
  ds = 0
  while the Q is not empty
    remove vertex u from Q
    for each vertex v such that g has an edge {u,v}
      if v has not yet been visited
      dv = du +1
      add v to Q
  ```
  
  Worst case is O(V+E) time 
    - worst case is if graph is connected
    

- DFS
  - Pseudocode
  ```
  DFS
  mark s as visited
  for each vertex v such that g has an edge {s,v}
    if v has not been visited
      DFS(g,v)
  ```

- Kruskal's
  ```
  1. T (the final spanning tree) is defined to be the empty set;
  2. For each vertex v of G, make the empty set out of v;
  3. Sort the edges of G in ascending (non-decreasing) order;
  4. For each edge (u, v) from the sored list of step 3.
      If u and v belong to different sets
         Add (u,v) to T;
         Get together u and v in one single set;
  5. Return T
  ```
  
- Prims
  ```
  1.  Make a queue (Q) with all the vertices of G (V);
  2.  For each member of Q set the priority to INFINITY;
  3.  Only for the starting vertex (s) set the priority to 0;
  4.  The parent of (s) should be NULL;
  5.  While Q isn’t empty
  6.     Get the minimum from Q – let’s say (u); (priority queue);
  7.     For each adjacent vertex to (v) to (u)
  8.        If (v) is in Q and weight of (u, v) < priority of (v) then
  9.           The parent of (v) is set to be (u)
  10.          The priority of (v) is the weight of (u, v)
  ```

- Bellman-Ford
 ```
 Bellman-Ford(input: weight graph G and vertex s)
 set distance[v] to infinity for all verticies
 set distance[s] = 0
 repeat |V| -1 times
  for each edge e in E
    relax e
  for each edge (u,v) in E
    if distance[v] > distance[u] + w(u,v)
      return FALSE
  return TRUE
 ```
 
 - Dijkstra's
 ```
 distance[v] = infinity
 distance[s] = 0
 S = 0
 while V - S != 0
  u is the vertex V - S with least distance[u]
  for each vertex v adjacent to u
    relax (u,v)
  S = S U {u}
 ```
