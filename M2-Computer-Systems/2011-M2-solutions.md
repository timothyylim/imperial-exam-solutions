# Section A

## 1

### ai) 
  16-bit / 4-bit = 4 memory chips per module. 2M / 256K = 8 memory modules required
  
### aii) 
  byte addressable: 2M * 2(bytes per row) = 2^20 * 2 * 2 = 2^22 
    22 bits are required to address every byte in the memory
  word addressable: 2M * 1(word per row) = 2^21
    21 bits required to address every word
    
### aiii) 
  I don't really understand where are 2 numbers there in this table...
  
```
    100h  101h  101h  101h
    03h   f7h   80h   01h

Big Endian means the most significant bit first

Little Endian means the least significant bit first
```
### bi)
Tiny Precision has 7 bits for the exponent => can express 2^7 (128) powers. Exponent for IEEE is held in Excess-127 format.
Analogically as for IEEE (here Excess-63) 000 0000 corresponds to -63, 111 1111 corresponds to 64, 100 0000 corresponds to power 1.

```
  4180h       = 0100 0001 1000 0000
  sign        = 0
  exponent    = 100 0001 = (129 - 127) = 2
  significand = 1000 0000 = 2^8
  
  Decimal value = 2^8 * 2^2 = 2^10 = 1024
```

  
  
  
## 2 
### b) 
  
  pseudocode:
    A=0
    B given
    for i = 0 to C
      A = A+B
  
  assembly:
    000H      A
    001H      B
    002H      C
    003H      1
    
    080H      LOAD R1, [001H]
    081H      LOAD R2, [002H]
    082H      IFZER R2, [087H]
    083H      IFNEG R2, [087H]
    084H      ADD R1, [001H]  //a = a+b
    085H      SUB R2, [003H]  //c-1
    086H      GOTO    082H
    087H      STORE R1, [000H]
    088H      STOP
    
