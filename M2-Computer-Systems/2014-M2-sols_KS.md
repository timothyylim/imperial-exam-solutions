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

**(iii.)** This question refers to arithmetic shifts (sal, see [slide 6](http://www.commsp.ee.ic.ac.uk/~kkleung/Computer_Systems_2015/6_Pentium3.ppt) or [wikipedia](https://en.wikipedia.org/wiki/Arithmetic_shift) or check out this [video tutorial](https://www.youtube.com/watch?v=_Z3yz0k9dmQ&nohtml5=False)).  Arithmetic shifts can be used to multiply or divide a signed integer by by a power of two.  Shifting left by n bits on a signed or unsigned binary number has the effect of multiplying it by 2^n.  So in this case, the operand will be multiplied by 4.  The most significant bit would ordinarily store the sign and multiplying a number by 4 does not change the sign so the most significant bit should remain the same as it was before if the result is correct.  If the most significant bit flips, this procedure would result in overflow.

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

Actual answer from the exam grading scheme:

Address| Contents            
-------|------------
800H   | LOAD[90FH]          
801H   | PUSH[91FH]           
802H   | PUSH[91FH]           
803H   | SUB                  
804H   | PUSH[91FH]           
805H   | PUSH[91FH]           
806H   | MULT                 
807H   | PUSH[910H]           
808H   | PUSH[91DH]           
809H   | MULT                 
80AH   | ADD                  
80BH   | MULT                 
80CH   | POP[920H]            
80DH   | STORE                

Address| Stack Contents            
-------|------------
920H   | A  
91FH   | X
91EH   | Y
91DH   | Z
...    | ...
910H   | 5
90FH   | 501H (start of memory)
...    | ...
500H   | Stack Memory...

###3 a.

See Scheduling slide 3 for the process state diagram.

Newly created processes are not allowed to run immediately because some processes may be already running. The scheduler put new processes on the CPU when it is ready.

###3 b.

For pre-emptive scheduling (in the case you want to control runaway processes as opposed to non-preemptive scheduling):

* Let process run for a maximum amount of fixed time
       * Requires clock interrupt
* External event results in higher priority process being run

A clock is necessary because you often need to give processes time limits. 

Read more about fixed priority pre-emptive scheduling on [wikipedia](https://en.wikipedia.org/wiki/Fixed-priority_pre-emptive_scheduling).


###3 c.

The send, receive, and reply operations may be synchronous or asynchronous. Synchronous message passing occurs between objects that are running at the same time. With asynchronous message passing it is possible for the receiving object to be busy or not running when the requesting object sends the message.

Synchronous message passing is what typical object-oriented programming languages such as Java and Smalltalk use. Asynchronous message passing requires additional capabilities for storing and retransmitting data for systems that may not run concurrently.

The buffer required in asynchronous communication can cause problems when it is full. A decision has to be made whether to block the sender or whether to discard future messages. If the sender is blocked, it may lead to an unexpected deadlock. If messages are dropped, then communication is no longer reliable.

If you don't specify a time limit then this may result in a buffer overflow.

Read more about message passing on [wikipedia](https://en.wikipedia.org/wiki/Message_passing).


###3 d.

Threads are execution streams that share the same address space. When multithreading is used, each process can
contain one or more threads.

Threads exist in the user space and have their own registers and stack.

Check out Process-Threads slide 45.

###3 e.

The use of fork and exec exemplifies the spirit of UNIX in that it provides a very simple way to start new processes.

The fork call basically makes a duplicate of the current process, identical in almost every way (not everything is copied over, for example, resource limits in some implementations but the idea is to create as close a copy as possible).

The new process (child) gets a different process ID (PID) and has the the PID of the old process (parent) as its parent PID (PPID). Because the two processes are now running exactly the same code, they can tell which is which by the return code of fork - the child gets 0, the parent gets the PID of the child. This is all, of course, assuming the fork call works - if not, no child is created and the parent gets an error code.

The exec call is a way to basically replace the entire current process with a new program. It loads the program into the current process space and runs it from the entry point.

So, fork and exec are often used in sequence to get a new program running as a child of a current process. Shells typically do this whenever you try to run a program like find - the shell forks, then the child loads the find program into memory, setting up all command line arguments, standard I/O and so forth.

If the exec is called following fork (and this is what happens mostly), that causes a write to the process space and it is then copied for the child process.

Check out the differences between exec and fork on [stackoverflow](http://stackoverflow.com/questions/1653340/differences-between-exec-and-fork).

The main reason is likely that the separation of the fork() and exec() steps allows arbitrary setup of the child environment to be done using other system calls. For example, you can:
* Set up an arbitrary set of open file descriptors
* Alter the signal mask
* Set the current working directory
* Set the process group and/or session
* Set the user, group, and supplementary groups
* Set hard and soft resource limits

...and many more besides.

[Why fork and exec are kept 2 separate calls.](http://stackoverflow.com/questions/5090731/why-fork-and-exec-are-kept-2-seperate-calls)


###4 a.

DMA which stands for Direct Memory Access is a system in which a hardware component of a computer gains access to the Memory Bus and controls the transfer. Say A CD/DVD drive usually works using DMA. But remember that the CPU is always the MASTER of everything, that means even though the CPU has given the DMA controller the mastership, It still has the power to check DMA. It can reinvoke the Bus control any time it wants, it may even do the task of DMA. There are registers that are used to set the Control of Bus from CPU to DMA and DMA to CPU. Once the DMA controller is done, it may interrupt or signal the CPU that it has finished its job. That's about DMA.

Now coming to Interrupt I/O. Interrupt I/O is way more frequent than DMA. A process usually undergoes I/O plenty of times. Asking for a input from the user would be an interrupt I/O. Not DMA. There are two types of interrupts:

1. Software Interupt
2. Hardware Interupt

Each interrupt has a special number assigned to it. And each interrupt is serviced by a Interupt Routine ( a simple function ) that is saved somewhere inside your RAM and which is invoked from a Table that consists of Interrupt numbers. I'm telling this for your understanding. When you move your mouse or type on keyboard, Its actually an interrupt that is happening. 

[DMA vs Interrupt Driven I/O](http://stackoverflow.com/questions/25318145/dma-vs-interrupt-driven-i-o)

###4 b.

Three methods that connect blocks to files:

1. Block Chaining - for diagram see "Block Linkage (Chaining) II" from "File Systems"
2. File Allocation Table - for diagram see "Block Allocation Table II" from "File Systems"
3. Index Blocks - for diagram see "Index Blocks II" from "File Systems"

In each of the diagrams, insert the block numbers and the name of the file accordingly.

###4 c.

An inode (index block in UNIX/Linux) consists of various pieces of information regarding a file including (but not limited to) access controls, user ID, access time, and a set of direct, indirect, double, and triple pointers. On file open, the OS opens the inode which is structured this way on the disk but also includes the disk device number, the inode number, the number of processes with opened file, and the major/minor device number.

See "Unix/Linux: Inodes" from "File Systems".

###4 d.

In MINIX, each file or directory is represented as an inode, which records metadata including type (file, directory, block, char, pipe), IDs for user and group, three timestamps that record the date and time of last access, last modification, and last status change. An inode also contains a list of addresses that point to the zones in the data area where the file or directory data is actually stored. From [wikipedia](https://en.wikipedia.org/wiki/MINIX_file_system).

As far as the diagram goes I think he might be looking for the one in "File Systems" on the "Inodes" slide. Otherwise I might write something like what you see when we type "ls -l".

###4 e.



