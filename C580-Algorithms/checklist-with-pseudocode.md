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

- Insert

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

- Merge

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

- Quick
- Count
- Radix
- Heap sort

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
```

### Graphs

- BFS
- DFS
- Kruskal's
- Prims
- Bellman-Ford
- Dijkstras

### Data Structures

- Hashtable
- Queue
- Array
- Stack
- Red Black Tree
- Set
- Binary Heap
- Binary Search Tree

### String Matching 

- KMP
- BM 

