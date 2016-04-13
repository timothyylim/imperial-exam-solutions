#Computer Systems 2013
##1 a.

Big Endian: The most significant bit of a word in memory comes first.

| 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|
| T | E | S | T | I | N | G |


Little Endian: The least significant bit of a word in memory comes first.

| 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|
| G | N | I | T | S | E | T |

##1 b.

2's Complement (N-bits; N = 4):

| Bit Pattern    | 0000 | ... | 0111            | 1000          | ... | 1111 |
|----------------|------|-----|-----------------|---------------|-----|------|
| 2's Complement | +0   | ... | +2^(N-1)-1 = +7 | -2^(N-1) = -8 | ... | -1   |

-5 = 1011

##1 c.

Convert -139.325 to binary and hexadecimal using IEEE Single Precision Format (use rounding over truncation).

-139.325 in binary is 1000 1011.0101 0011 0011 0011...

This becomes 1.0001 0110 1010 0110 0110 011 x 2^7

Sign: 1 (negative)

Exponent: 7 + 127 = 134 --binary--> 1000 0110

Significand: 0001 0110 1010 0110 0110 011

Solution = Sign + Exponent + Significand

1100 0011 0000 1011 0101 0110 0110 011

Binary | 1100 | 0011 | 0000 | 1011 | 0101 | 0011 | 0011 | 0011
-------|------|------|------|------|------|------|------|-----
**Hex**    | **C**    | **3**    |  **0**   | **B**   |   **5**  |  **3**   |  **3**   | **3**


##1 d.

It's a really long proof so I haven't typed out every single step.

Equation | Rule
-------- | ---------
E = A' \* (A + B) + (B + A \* A) \* (A + B') | given
E = (A' \* A) + (A' \* B) + (B + A \* A) \* (A + B') | distributive
E = 0 + (A' \* B) + (B + A \* A) \* (A + B') | negation
E = (A' \* B) + (B + A \* A) \* (A + B') | simplification
E = (A' \* B) + (B + A) \* (A + B') | idempotent
E = (A' \* B) + (B + A) \* A + (B + A) \* B' | distributive
E = (A' \* B) + A \* A + B \* A + B' \* B + B' \* A | distributive
E = (A' \* B) + A + B \* B + A \* B' | idempotent, negation, and simplification
E = (A + A) \* (A + B) + A' \* B + A \* B' | distributive
E = A + A' \* B + A \* B' | negation and simplification
E = (A + A') \* (A + B) + (A \* B') | distributive
E = (A + B) + (A \* B') | negation and simplification
E = A + (B + (A \* B')) | associative
E = A + (B + A) \* (B + B') | distributive
E = A + (B + A) | negation and simplification
E = A + B | idempotent

##2 a.

**(i.)** The **EIP** (instruction pointer) register holds the address of the next instruction to be executed.  EIP is not normally manipulated explicitly by programs.  The eip register corresponds to the program counter register in other architectures.  It is updated by special control-flow CPU instructions (e.g. call, jmp, ret).  [Slide 6](http://www.commsp.ee.ic.ac.uk/~kkleung/Computer_Systems_2015/5_Pentium1-2.ppt).

**(ii.)** The use of methods involves using a stack and a stack pointer register (esp) as well as the base pointer register (ebp). When a method is first called using call, the eip (return address) is pushed to the stack and we jump to the start of method. Then when we run ret (return), we pop the return address into eip. Parameters and objects can also be passed if necessary using the stack. [Pentium Architecture: Methods](http://www.commsp.ee.ic.ac.uk/~kkleung/Computer_Systems_2015/7_Pentium4-5.ppt).

**(iii.)** IRET (return from an interrupt handler) will restore the state (EFLAGS and EIP) and then jump to the return address on the stack. RET (return from a call) will pop the return address into eip. It is the programmer's responsibility to restore any other registers. [Slide 26](http://www.commsp.ee.ic.ac.uk/~kkleung/Computer_Systems_2015/8_Slides_IO.PPT) and [slide 11](http://www.commsp.ee.ic.ac.uk/~kkleung/Computer_Systems_2015/7_Pentium4-5.ppt).

**(iv.)** A function call is synchronus while a hardware interrupt is asynchronus.  Also, before calling the interrupt handler, a pentium cpu will push the EFLAGS register and disable further interrupts.  A regular function call does not do this, it will only push EIP.
