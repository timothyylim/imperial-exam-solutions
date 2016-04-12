#Computer Systems 2015
##Section A
###1 a.

**(i).** Sign and Magnitude: find the positive binary and, if negative, flip the sign (first bit).

1010 1101

**(ii).** One's complement: find positive binary and, if negative, flip all of the bits.

1101 0010

**(iii).**  Two's complement: same as one's complement but if negative, add one to the one's complement.

1101 0011

**(iv).** -45 + 64 = 19

64 is the offset (excess-64), -45 is the number we want so we'll do the binary of 19.

0001 0011.

###1 b.

**High Order Interleaving** involves putting the module address bits first in the address
which results in having the adjacent addresses all come from the same module. If multiple memory
modules can be accessed concurrently then separate processors can access different rows simultaneously
allowing for parallel operation.

**Low Order Interleaving** involves putting the module address bits last in the address which results
in having the adjacent addresses all come from different modules.  This is good if the CPU can request
multiple adjacent memory locations.

###1 c.

![alt text](http://hyperphysics.phy-astr.gsu.edu/hbase/electronic/ietron/nor2.gif "Logo Title Text 1")

From Tim.

###1 d.

1. Convert to binary number: 11 0100.0100 1100 11...

2. Normalise: 1.1010 0010 0110 011.. x 2^5

3. Find Significand field (23 bits): 1010 0010 0110 0110 0110 011

4. Find Exponent field (5+127 = 132): 1000 0100

5. Sign: 1 

6. Put it all together... Sign + Exponent + Significand = 1 + 1000 0100 + 1010 0010 0110 0110 0110 011

| Binary | 1100 | 0010 | 0101 | 0001 | 0011 | 0011 | 0011 |0011 |
|--------|------|------|------|------|------|------|------|-----|
| Hex    | C    | 2    | 5    | 1    | 3    | 3    | 3    | 3   |

http://www.h-schmidt.net/FloatConverter/IEEE754.html

##Section B
###2 a.

**(i.)** Every machine instruction (16 bits) has a:
* **OPCODE** or operation code for selecting CPU instruction -- 4 bits
* **REG** or register for specifying the 1st operand for instruction -- 2 bits
* **ADDRESS** for specifying the 2nd operand for instruction -- 10 bits

**(ii.)** Three possible ways to address operands in an instruction:

1. **Register Operands:** operand is stored in general purpose registers.

2. **Immediate Operands:** operand is included in instruction (constant).

3. **Memory Operands:** operand is stored in a memory address location.

Immediate addressing is the fastest because it doesn't require any lookup.

See slide 14 of Pentium Architecture: Registers & Addressing Modes for examples or check out this [page](http://www.tutorialspoint.com/assembly_programming/assembly_addressing_modes.htm) for more information.

**(iii.)** 


**(iv.)** The call instruction will begin the instruction no matter what. Jump instructions typically have a conditional flag where they will only jump to a different address within the stack if the flag contains a specific value. This can be used to create a nested function by jumping "backwards" in the stack and then subsequently executing calls in order from there ultimately leading back to the jump instruction.The jump instruction will, if used correctly, eventually be bypassed due to some condition which is also how while and for loops work. For more information on jump instructions and nested loops see slides 14-21 of Pentium Architecture: Introductory Programming.
