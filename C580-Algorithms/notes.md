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
    
