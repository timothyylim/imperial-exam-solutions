# Section A
## 1
### ai)
  ```
  | A | B | A OR B |
  | 0 | 0 |   0    |
  | 0 | 1 |   1    |
  | 1 | 0 |   1    |
  | 1 | 1 |   1    |
  
  | A | B | A NAND B |
  | 0 | 0 |   1    |
  | 0 | 1 |   1    |
  | 1 | 0 |   1    |
  | 1 | 1 |   0    |
  ```
### aii)  
  ```
  De Morgan Rules:
  (A+B)' = A' * B'
  (A*B)' = A' + B'
  Same applies if there is more than 2 variables
```
### aiii)
```
  A+B = (A' * B')' = (A NAND A) NAND (B NAND B)
  ```
### b) 
  ```
  32-bit / 8-bit = 4 chips per module (256K * 32-bit)
  16Megabytes = 4M * 4 bytes = 4M * 32-bit 
  4M / 256K = 16 modules
  total chips = 16 * 4 = 64 chips
  total modules = 16
  ```
  16 modules => need 4 bits to represent module
  Low-order interleaving = last 4 bits in memory address represent module
  
