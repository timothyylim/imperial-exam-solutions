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
  
  adding back the avoided bit -> our number is 1.1 * 2^2
  Binary value = 1.1 * 2^2 = 110 = Decimal 6
```
### bii)
  -17.5 conversion:
  negative => sign bit is 1
  17 = 2^4 + 2^0 = 0001 0001
  0.5 = 2^(-1) = 0.1
  17.5 = 1 0001.1
  17.5 normalised form = 1.00011 * 2^4, hence exponent is 4, in excess-63 4 = 100 0011
  Following the same method as for IEEE format we lose the first bit of 17.5 and store everything what's left after the coma => 
  ```
    -17.5
    Sign        = 1
    Exponent    = 100 0011
    Significand = 0001 1000
    Total:  1100 0011 0001 1000
    in HEX:   C    3    1   8
  ```
### bii)

  sum: 6 + (-17.5) = -11.5
  Exponents differ by (4-2)=2, hence shift smaller number by 2 places to the left. Since -17.5 is negative and |-17.5| > |6| deduct 6 from 17.5 and keep the Sign bit unchanged:
  ````
      1.00011 *2^4
    - 0.011   *2^4
    -----------
      0.10111 *2^4 = 1.0111 * 2^3 (normalised form) = 1011.1 = Decimal 11.5
      
      Decimal answer (including the Sign bit) is then -11.5
  
  The Tiny Precision format is 
    (1) (100 0011) (0111 0000)
          power 3
  HEX: C 3 7 0
  ```
  For multiplication we first evaluate the sign bits by adding them together => 1 + 0 = 1
  Negative number multiplied by a positive number will stay negative
  ```
      1.00011 * 2^4
    * 1.1     * 2^2
    ---------------
      1.00011
      0.100011
    ---------------
      1.101001  * 2^(4+2)
  Multiplication of Significands is then 1.101001 * 2^6 (normalised form) = 110 1001 = Decimal 105
  Decimal answer (including the Sign bit) is then -105
  The Tiny Precision format is:
    (1) (100 0110) (1010 0100)
          power 6
  HEX: C 6 A 4
  
  -17.5 * 6 = 105
  ```
## 2 

### ai) 

2 fields that specify the unconditional jump instruction are OPCODE of the jump instruction (e.g. JMP) and ADDRESS of the instruction to jump to. When CPU executes the jump instruction it sets the eip to the ADDRESS mentioned in the instruction, then it goes to that memory address to fetch the new instruction, loads it into Instruction Decoder, decodes the instruction and proceeds as normal. If jump is conditional, then the condition is first checked is ALU, if condition is true, then amend eip to ADDRESS from the jump instruction and do all the usual steps.

### aii) 
1) Register Operands
2) Immediate (Constant) Operands
3) Memory Operands

Register Operands allow the fastest access time as the values are stored immediately in the CPU and there is no need to go fetch the values anywhere else. Constants are the second fastest and their values are stored in cashe. Memory operands are the slowest as CPU needs first to read them from their memory addresses and then fetch them back into CPU through internal bus, which delays processing speed significantly. All of the operands allow maximum range of data representation as the user can basically store anything they want in any of the operands. If I had to choose, I would say Memory allows the maximum range as if e.g. CPU registers are 16 bits, and you can only store 16bit value, in quadword memory you can store 64 bit values.

### aiii) 

Stack memory access is LIFO - last in first out. Once a value is pushed onto stack, it becomes the first one to be popped until another value is pushed onto the stack.

When a program performs a funtion call it pushes any values to be passed to the function, the current call's ebp and the return address (address of the instruction after the function call) onto the stack. When the function returns, the program pops the return address into eip and resets the esp to the initial ebp, so it continues from where it left off.

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
    
