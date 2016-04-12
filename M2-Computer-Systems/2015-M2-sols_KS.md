#Computer Systems 2015
##Section A
###1 a.

**(i).** Sign and Magnitude: just flip the sign for negatives.

1010 1101

**(ii).** One's complement: invert all digits.

1101 0010

**(iii).**  Two's complement: add one to the one's complement.

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
1. OPCODE, REG, ADDRESS

2. OPCODE, ADDRESS, REG

3. REG, ADDRESS, OPCODE

I don't know which one is the most efficient but I would assume #1 because that's what the lecture notes mostly use. :/

**(iii.)**


**(iv.)** 

For more information on jump instructions and nested loops see Introductory Pentium slides 14-21.
