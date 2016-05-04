should be able to recall the pseudocode and run time analysis for the following:

### misc.

- Binary Search

*split it in half each time*

```
binary search (input List: L, value k):

  Repeat
    select element near middle of L
    if e == k, return True
    if k > e search elements after e
    else search elements before e
    return False
```



- Amortized analysis

### Sorting

- Insert Sort

*check behind you and insert as far back as you need to*

```
insert sort (input: Sequence A = [a1...aN]):

  for each element a[i] in [a2...aN]:
    j = i
    while j > 1 and a[j] < a[j-1]:
      swap a[j] and a[j-1]
      j --
      
    return
```

```
Best case is an already sorted list: O(N)
Worst case is a reversed sorted list: O(N^2)
General Time Complexity: O(N^2)
```

- Merge Sort

*divide and conquer*

```
Merge Sort (input: Sequence A = [a1...aN] where N >= 1):

  if A has 1 element:
    return
    
  a = Merge Sort (a1...a[N/2]) // split the first half
  b = Merge Sort (a[N/2]...aN) // split the second half
  return Merge(a,b)            // merge them back together

Merge (input: Sequence A, Sequence B):

  Loop through A and B to form a new Sequence C as follows:
  
  p is smallest element of A not yet used
  q is smallest element of B not yet used
  the next element of C is the smaller of p and q
  
  return C
```

```
Some crazy shit gets you T(N) = O(N(log2 N))
```

- Quick Sort

```
Quicksort (Input: sequence A = (a1...aN))

  if A has more than 1 element:
    p = Partition A
    Quicksort(a1...aP-1)
    Quicksort(aP+1...aN)
    return
  
  return

Partition (Given sequence A = (a1...aN))

  select pivot element p from A
  swap p and aN
  storeIndex = 1
  
  for each a in (a1...aN-1)
    if a < p:
      swap a and storeIndex
      storeIndex ++
  
  swap a[N] and a[storeIndex]
  
  return storeIndex
```

[smug harvard guy explaining it](https://www.youtube.com/watch?v=aQiWF4E8flQ)

- Count
- Radix
- Heap sort
- 
```
Heap: each node has to be less or equal to its parent

add (key k, data d):
  insert new node n = (k,d) at end of the heap
  while k > key of n's parent:
    swap n with parent

remove:
  store top node (n0)
  replace top node with end node n = (k,d)
  while k < key of any child of n:
    swap with child of n that has the highest key
  return n0

Both methods take O(log2N) time.
```

```
HeapSort (input: List L)

  Create empty Heap H
  Remove each element of L and put it in H
  Remove each element of H and put it in L
  return L
```

```
Performance is O(NLog2N)
```
### Graphs

- BFS

```
BFS (graph g, source vertex s)

  Create Queue q = [s]
  while q is not empty:
    remove vertex u from q
    for each v that g has an edge {u,v}:
      if v has not been visited:
        mark v as visited
        add v to q
```

- DFS

```
DFS (graph g, source vertex s)
  
  mark s as visited
  for each vertex that g has an edge {s,v}
    if v has not been visited
      DFS(g,v)
```

- Kruskal's

*sort then add the smallest edge each time*

```
The set of edges is iterated over in weight order
If the next edge connects two distinct components, it is added
```

- Prims

*always add edges to the same component*

```
Prims (input: connected weighted graph G, vertex r)

  T = ({r},0)
  Add all edges (r,v) in G to queue Q prioritised by min weight
  
  while T has fewer than |V|-1 edges:
    Remove next edge (x,y) from Q
    if y is not in T
      add y to T
      add (x,y) to T
      add all edges (y,v) in G to Q
  
  return T
```
```
O(Elog2V)
```

- Bellman-Ford

*Distance vector routing from networks uses Bellman-Ford*

- Dijkstras




### Data Structures

- Set
- Binary Search Tree

```
All keys in the left subtree are less or equal to root key and all keys in right subtree are greater or equal to root key.
```

```
O(NlogN)?
```

- Red Black Tree



- Queue
- Array
- Stack

- Hashtable


### String Matching 

- Naive

- KMP

http://jakeboxer.com/blog/2009/12/13/the-knuth-morris-pratt-algorithm-in-my-own-words/

- BM 


### Dynamic Programming

- Rod Cutting

https://www.youtube.com/watch?v=ElFrskby_7M


