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
  Assuming there is a typo in the exam question and the table should actually look like:
    100h  101h  102h  103h
    03h   f7h   80h   01h
  
  
  
  
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
    
