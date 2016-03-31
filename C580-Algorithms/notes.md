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

- Queue 

- Binary Heap Implementation of a Priority Queue 
  - Pseudocode for add(key k, data d)
  - Pseudocode for remove

- Sets

- Trees

- Binary Search Tree
  - Add 
  - Search
  - Performance 

- Hash Tables



