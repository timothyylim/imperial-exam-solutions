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
### bi) 
  ```
  32-bit / 8-bit = 4 chips per module (256K * 32-bit)
  16Megabytes = 4M * 4 bytes = 4M * 32-bit 
  4M / 256K = 16 modules
  ```
### bii)

```
  total chips = 16 * 4 = 64 chips
  total modules = 16
  ```
  
### biii)

  16 modules => need 4 bits to represent module
  Low-order interleaving = last 4 bits in memory address represent module (from 0 to 15)
  003CB4 - last for bits are 0100 => module 4 contains the addressed memory

### c) 
  IEEE single precision floating point format has:
  Sign S = 1 bit
  Exponent E = 8 bits
  Significand = 23 bits
  
  Exponent E is stored in Excess - 127 format. Significand is the part after the coma in the normalised representation of the number
  
  C49A5000 = 1100 0100 1001 1010 0101 0000 0000 0000
  Sign = 1 => number is negative
  Exponend = 1000 1001; in Excess-127 this is 10
  Significand = 001 1010 0101
  
  The number is then -1.00110100101 * 2^10 = -100 1101 0010.1
  Decimal is then -1234.5
  
## 2
### ai)
  Memory, registers and constants are the three types of operands 
  
### aii)
  Programmed I/O - when a device recieves I/O signal, it waits in the process queue for its CPU time to perform the analysis of the I/O
  Interrupt driven I/O - when a device recieves I/O signal, it interrupts the current process (jumps the queue) and performs the analysis of the I/O
  
  I/O is not a frequent event and user would want to have a very quick response to their I/O actions. The interrupt driven I/O achieves this through reacting to user processes very quickly and then resuming its other tasks after processing the I/O.
### aiii)  

  ebp and eip will be saved
  ebp needed to set up the stack pointer to where it was before the interrupt
  eip needed to point at the next instruction of the method, when it resumes
  
## 2
### b)
```

001H      1
002H      n
003H      300H

080H      LOAD R0, [002H]
081H      LOAD R1, [003H]
082H      IFZER R0, XXX
083H      IFNEG R0, XXX
084H      LOAD R2, R0
085H      IFZER R2, XXX
086H      IFNEG R2, XXX
087H      LOAD R3, [R1]
          SUB R1, [001H]
088H      SUB R3, [R1]
          IFNEG R3, SWAP
          
          SUB R2, [001H]
          GOTO 085H
          SUB R0, [001H]
          GOTO 082H
          



200H
201H
202H
