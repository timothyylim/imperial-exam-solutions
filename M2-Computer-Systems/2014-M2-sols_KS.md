#Computer Systems 2014
##Section A
###1 a.

Decimal       | Binary
--------------|-------
13            | 0000 1101
-4            | 1111 1100
13 + (-4) = 9 | **1** 0000 1001

The bolded bit gets discarded so we end up with 0000 1001.  Note: if we had A - (-B) = -C or -A - B = C where A and B had different signs but C had the same sign as the subtrahend then we'd have to worry about overflow.

###1 b.

8G x 16-bit Main Memory. 8G = 8 x 2^30 rows.  16-bit = 2 bytes per row.

**(i.) Word-Addressable Main Memory:**
* word-addressable = address for every row (word = 1 row).
* bits required for addressing: 8 x 2^30 = 2^3 x 2^30 = 2^33. Therefore, we need 33 bits. 

**(ii.) Byte-Addressable Main Memory:**
* byte-addressable = address for every byte.
* bits required for addressing: 2 x 8 x 2^30 = 2^1 x 2^3 x 2^30 = 2^34. Therefore, we need 34 bits. 

###1 c.

Equation | Rule
------------ | -------------
E = A + (A' \* B) + (A + B)' | given
E = (A + A') \* (A + B) + (A + B)' | distributive
E = 1 \* (A + B) + (A + B)' | negation
E = (A + B) + (A + B)' | simplification
E = 1 | negation

###1 d.

C304 F000 ==> **1100 0011 0000 0100 1111 0000 0000 0000 (binary)**

Sign (1st bit): 1 --> negative number

Exponent (middle 8-bits): 1000 0110 = 134 --> E = 134 - 127 = 7

Significand + **hidden bit** (last 23-bits): **1**.000 0100 1111 0000 0000 0000

Now we put it all together... (significand + hidden bit) x (2^exponent) = a binary number.  Convert binary to decimal.  Add sign.

1.0000 1001 1110 0000 0000 000 x 2^7 = 1000 0100.1111 0000 0000 000 = 2^7 + 2^2 + 2^-1 + 2^-2 + 2^-3 + 2^-4 = 132.9375

add in the sign... -1.329375 x 2^2 = **-132.9375 (decimal)**

http://www.h-schmidt.net/FloatConverter/IEEE754.html

##Section B
###2 a.

**(i.)** Every machine instruction must have an OPCODE or operation code for selecting a CPU instruction (4 bits).

For more information see [CPU Organization](http://www.commsp.ee.ic.ac.uk/~kkleung/Computer_Systems_2015/3_Slides_CPUOrganisation.ppt) slides 6-8.

**(ii.)** Operands can be stored in either a register or a memory location (address).  Register addressing is faster than memory addressing because it doesn't involve accessing the memory which is time intensive.  See this [page](http://www.tutorialspoint.com/assembly_programming/assembly_addressing_modes.htm) for further reading.

**(iii.)** This question refers to arithmetic shifts (sal, see [slide 6](http://www.commsp.ee.ic.ac.uk/~kkleung/Computer_Systems_2015/6_Pentium3.ppt) or [wikipedia](https://en.wikipedia.org/wiki/Arithmetic_shift) or check out this [video tutorial](https://www.youtube.com/watch?v=_Z3yz0k9dmQ&nohtml5=False)).  Arithmetic shifts can be used to multiply or divide a signed integer by by a power of two.  Shifting left by n bits on a signed or unsigned binary number has the effect of multiplying it by 2^n.  So in this case, the operand will be multiplied by 4.  The most significant bit would ordinarily store the sign and multiplying a number by 4 does not change the sign so the most significant bit should remain the same as it was before if the result is correct.  This procedure could result in overflow which would likely be the case if the most significant bit flips.

As a side note, since it is shifting to the left, extra spaces created by the shift will be filled with zeros.  If we were shifting right with SAR we would fill the spaces with the sign bit and it would round a negative division towards negative infinity although IDIV (division) would round towards 0.  SHL and SAL are identical but SHR is for unsigned numbers while SAR is for signed (i.e. 2's complement) numbers. The carry flag will always have the last bit that was discarded at the end.

**(iv.)**  The CPU will receive an interrupt in the form of an interrupt vector number (0 to 255 on a Pentium CPU) which is an index that will determine where to find the "descriptor" in the interrupt descriptor table.  The descriptor will include the Interrupt Handler's start address which is held in a special CPU register called the IDT Base Register.

When an Interrupt occurs the Pentium CPU will:

* complete the currently executing instruction
* push the EFLAGS register onto the stack
* clear the interrupt flag bit in the EFLAGS register - this disables further interrupts
* push the return address (i.e. contents of the EIP register) onto the stack
* call the interrupt handler using the entry in the itnerrupt descriptor table
* to return, the interrupt handler executs the iret instruction which restores the state (e.g. EFLAGS and EIP) and jumps to the return address on the stack.  It is the programmers responsibility to resotre any other registers.

For more information on interrupts see [Pentium I/O](http://www.commsp.ee.ic.ac.uk/~kkleung/Computer_Systems_2015/8_Slides_IO.PPT) slides 24-29. For more information on the EIP and EFLAGS registers, see slides 6 and 7 of [Pentium Architecture: Registers & Addressing Modes](http://www.commsp.ee.ic.ac.uk/~kkleung/Computer_Systems_2015/5_Pentium1-2.ppt).
