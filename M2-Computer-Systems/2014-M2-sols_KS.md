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

Sign (1st bit): 1 ==> negative number

Exponent (middle 8-bits): 1000 0110 = 134 ==> E = 134 - 127 = 7

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

###2 b. 

Address| Contents            | Pseudocode
-------|---------------------|-------
001H   | A                   | Ouput Variable
002H   | X                   | Input Variable
003H   | Y                   | Input Variable
004H   | Z                   | Input Variable
005H   | 5                   | Constant Variable
006H   | push [004H]         | Push Z onto the stack
       | push [005H]         | Push 5 onto the stack
       | mult                | Multiply Z and 5 
       | push [002H]         | Push X onto the stack 
       | push [003H]         | Push Y onto the stack 
       | mult                | Multiply X and Y 
       | add                 | (X * Y)+(Z * 5)
       | push [002H]         | Push X onto the stack 
       | push [003H]         | Push Y onto the stack 
       | sub                 | X - Y
       | mult                | (X * Y)+(Z * 5) + (X-Y)
       | pop[001H]           | returns the solution


Protip: draw a stack on a piece of paper while you work through the solution.

###3 a.

See Scheduling slide 3 for the process state diagram

Newly created processes are not allowed to run immediately because some processes may be already running. The scheduler put new processes on the CPU when it is ready.

###3 b.

For Preemptive Scheduling (in the case you want to control runaway processes as opposed to non-preemptive scheduling)

- Let process run for a maximum amount of fixed time
       - Requires clock interrupt
– External event results in higher priority process
being run

A clock is necessary because you often need to give processes time limits. 

https://en.wikipedia.org/wiki/Fixed-priority_pre-emptive_scheduling


### 3 c.

The send, receive, and reply operations may be synchronous or asynchronous. Synchronous message passing occurs between objects that are running at the same time. With asynchronous message passing it is possible for the receiving object to be busy or not running when the requesting object sends the message.

Synchronous message passing is what typical object-oriented programming languages such as Java and Smalltalk use. Asynchronous message passing requires additional capabilities for storing and retransmitting data for systems that may not run concurrently.

The buffer required in asynchronous communication can cause problems when it is full. A decision has to be made whether to block the sender or whether to discard future messages. If the sender is blocked, it may lead to an unexpected deadlock. If messages are dropped, then communication is no longer reliable.

If you don't specify a time limit then you may result in a buffer overflow.

https://en.wikipedia.org/wiki/Message_passing


### 3 d.

Threads are execution streams that share the same address space. When multithreading is used, each process can
contain one or more threads.

Threads exist in the user space and have their own registers and stack.

Check out Process-Threads slide 45.

### 3 e.

The use of fork and exec exemplifies the spirit of UNIX in that it provides a very simple way to start new processes.

The fork call basically makes a duplicate of the current process, identical in almost every way (not everything is copied over, for example, resource limits in some implementations but the idea is to create as close a copy as possible).

The new process (child) gets a different process ID (PID) and has the the PID of the old process (parent) as its parent PID (PPID). Because the two processes are now running exactly the same code, they can tell which is which by the return code of fork - the child gets 0, the parent gets the PID of the child. This is all, of course, assuming the fork call works - if not, no child is created and the parent gets an error code.

The exec call is a way to basically replace the entire current process with a new program. It loads the program into the current process space and runs it from the entry point.

So, fork and exec are often used in sequence to get a new program running as a child of a current process. Shells typically do this whenever you try to run a program like find - the shell forks, then the child loads the find program into memory, setting up all command line arguments, standard I/O and so forth.

If the exec is called following fork (and this is what happens mostly), that causes a write to the process space and it is then copied for the child process.

http://stackoverflow.com/questions/1653340/differences-between-exec-and-fork

The main reason is likely that the separation of the fork() and exec() steps allows arbitrary setup of the child environment to be done using other system calls. For example, you can:

    Set up an arbitrary set of open file descriptors;
    Alter the signal mask;
    Set the current working directory;
    Set the process group and/or session;
    Set the user, group and supplementary groups;
    Set hard and soft resource limits;

...and many more besides.

http://stackoverflow.com/questions/5090731/why-fork-and-exec-are-kept-2-seperate-calls


###4 a.

DMA is Direct Memory Access. To be continued.

See Device Management lecture notes.


