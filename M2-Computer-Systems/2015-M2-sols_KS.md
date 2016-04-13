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
The following program will take an array A[] and reverse it. E.g. A = [1, 2, 3] will be come A = [3, 2, 1]. I'm going to use the following registers as such:

Register | Use
---|----
R0 | we don't need this actually
R1 | value of A at lower index
R2 | lower address of A
R3 | higher address of A

Address | Contents            | Pseudocode
--------|---------------------|-------
081H    | LOAD R2, 200H       | R2 = memory address of lowest index of A
082H    | LOAD R3, 250H       | R3 = memory address of highest index of A
**083H**| **STORE R1, [R2]**  | **R1 = value of A at the lower memory address (temp)**
084H    | STORE R2, [R3]      | set lower memory address to higher memory address value (swap)
085H    | STORE R3, [R1]      | set higher memory address to temp memory address value (swap)
086H    | INC R2              | point to the next lowest value
087H    | DEC R3              | point to the next highest value
**088H**| **JGT R2, R3, 083H**| **loop if R3 has passed R3**
089H    | STOP                | end the program
...     |                     |
200H    | A[0]                | holds A[0]
...     |                     |
250H*   | A[n-1]              | holds A[n-1]

*let's call 200H + n-1 = 250H (n=51) -- I'm undecided if I should have written some code at the beginning to find the address by using the value of n (which could be stored at, let's say, 300H).  So we could say R0 = [300H], DEC R0 (to get n-1), R3 = 200H and then INC R3 and DEC R0 while [R0] > 0 or something but then we'd have to use JGT which doesn't technically say you can compare values, just addresses but I think you could use it for values too.  I'm not sure.

##Section C
###3 a.

###4 a. A translation Look-aside Buffer (TLB) is a memory cache that stores recent translations of virtual memory to physical addresses for faster retrieval. See [slide 26](file://icnas4.cc.ic.ac.uk/ks815/Memory%20Management.pdf) or [this video](https://www.youtube.com/watch?v=95QpHJX55bM).

###4 b.

Memory Access Time = 200 ns (m)

TLB Access Time = 10 ns (e, epsilon)

Hit Ratio = 97% (a, alpha)

Three Level Paging System

Effective Access Time (EAT) = 2\*m + e - m\*a

Access Time for a "miss" (so a = 0) = 2\*m + e

**EAT** = 2\*200 + 10 - 200\*0.97 = **216 ns**

**Access Time for a "miss"** = 2\*200 + 10 = **410 ns**

See [slide 28](file://icnas4.cc.ic.ac.uk/ks815/Memory%20Management.pdf).
