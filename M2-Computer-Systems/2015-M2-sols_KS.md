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

**(i)** Idempotent law A + A = A 

**(ii)** DeMorgan's law A + B = A' . B'

**(iii)** Negation

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

**(i.)** Every machine instruction must have an OPCODE or operation code for selecting a CPU instruction (4 bits).

For more information see [CPU Organization](http://www.commsp.ee.ic.ac.uk/~kkleung/Computer_Systems_2015/3_Slides_CPUOrganisation.ppt) slides 6-8.

**(ii.)** Three possible ways to address operands in an instruction:

1. **Register Operands:** both operands are stored in general purpose registers.

2. **Immediate Operands:** one operand is included in instruction as a constant.

3. **Memory Operands:** operand is stored in a memory address location.

Immediate addressing is the fastest because it doesn't require any look-up (although the other operand is usually a register or memory address then) but register addressing is faster than memory addressing because it doesn't require any memory. For more information and examples see slides 14-20 of [Pentium Architecture: Registers & Addressing Modes](http://www.commsp.ee.ic.ac.uk/~kkleung/Computer_Systems_2015/5_Pentium1-2.ppt) or check out this [page](http://www.tutorialspoint.com/assembly_programming/assembly_addressing_modes.htm).

**(iii.)** 

**(iv.)** CALL will always push the EIP so that we can return to where we were before the call using RET. Jump instructions do not save (push) the EIP register and therefore will not return to any location after jumping. Jump also typically has a conditional flag only allowing the program to jump to a different address if the flag contains a specific value (although an unconditional jump does exist). This can be used to create a nested function by jumping "backwards" and then subsequently executing calls in order from there ultimately leading back to the jump instruction. The jump instruction will, if used correctly, eventually be bypassed due to some condition which is also how while and for loops work. For more information on jump instructions and nested loops see [slides 14-21](http://www.commsp.ee.ic.ac.uk/~kkleung/Computer_Systems_2015/6_Pentium3.ppt).

###2 b.
I'm going to use the following registers as such:

Register | Use
---|----
R1 | counter
R2 | value of A at lower index
R3 | lower address of A
R4 | higher address of A

**I haven't quite finished with the code below.  Just started.  Will come back to it.**

Address | Contents            | Notes
--------|---------------------|-------
079H    | LOAD R1, 300H       | set the counter = n 
080H    | DEC R1              | decrement the counter
081H    | LOAD R3, 200H       | R3 = memory address of lower index of A
082H    | LOAD R4, 250H       | R4 = memory address of higher index of A
083H    | STORE R2, [R3]      | R2 = value of A at the lower memory address (temp)
084H    | STORE R3, [R4]      | set lower memory address to higher memory address value
085H    | STORE R4, [R2]      | set higher memory address to temp memory address value
086H    | INC R3              | point to the next lowest value
087H    | DEC R4              | point to the next highest value
088H    | DEC R1              | decrement the counter
089H    | DEC R1              | decrement counter again
090H    | JGT R1, 301H, 081H  | loop if the counter > 0
091H    | STOP                | end the program
...     |                     |
200H    | A[0]                | holds A[0]
...     |                     |
250H*   | A[n-1]              | holds A[n-1]
300H    | n                   | holds n
301H    | 0                   | constant 0

*let's call 200H + n-1 = 250H (n=51)
