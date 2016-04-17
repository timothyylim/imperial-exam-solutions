#Computer Systems 2012
*Ananda didn't teach this year*
##Section A
###1 a.
2M X 16-bit memory made up from 256K x 4-bit chips.

2 x 2^20 = 2^1 x 2^20 = 2^21 rows.

16-bit = 2 bytes = 2 words per row.

256 x 2^10 = 2^8 x 2^10 = 2^18 rows per chip.

Memory Size = 2M x 2 Bytes = 4MB

**(i.) 4 chips** per module are required (4-bit x N = 16-bit).  Since each module will have 512KB (256K x 2 Bytes) and the total memory size required is 4MB, then we will need **8 modules**.

**(ii.)** Bits required to access byte-addressable memory: 2^21 rows * 2^1 bytes per row = 2^22 so **22 bits.**  Bits required to access word-addressable memory: **21 bits.**

**(iii.) Big Endian**

Integer #1 = 03F7 (hex) = 0000 0011 1111 0111 (binary) = 1+2+4+16+32+64+128+256+512 = 1015 (decimal)

Integer #2 = 8001 (hex) = 1000 0000 0000 0001 (binary) = [subtract 1 then flip] = -32767 (decimal)

| Two's Complement | Binary              | Decimal |
|------------------|---------------------|---------|
| Integer #1       | 0000 0011 1111 0111 | 1015    |
| Integer #2       | 1000 0000 0000 0001 | -32767  |
| Sum              | 1000 0011 1111 1000 | -31752  |

**(iv.) Little Endian**

Integer #1 = F703 (hex) = 1111 0111 0000 0011 (binary) = -(2^N-1) - (2^0 + 2^1 + 2^8 + 2^9 + 2^10 + 2^12 + 2^13 + 2^14) = 2^15 - 30467 = 2301 (decimal)

Integer #2 = 0180 (hex) = 0000 0001 1000 0000 (binary) = 384 (decimal)

| Two's Complement | Binary              | Decimal |
|------------------|---------------------|---------|
| Integer #1       | 1111 0111 0000 0011 | -2301   |
| Integer #2       | 0000 0001 1000 0000 | 384     |
| Sum              | 1111 1000 1000 0011 |  -1917  |


###1 b.



##Section B
###2 a.

**(i.)** The two fields are the OPCODE for **JMP** and **the new address** to load into the EIP register which will dictate where the program goes next.  The address can also be stored in the EAX register which could also be used after JMP.
[Slides 14-15](http://www.commsp.ee.ic.ac.uk/~kkleung/Computer_Systems_2015/6_Pentium3.ppt) and [wikipedia](https://en.wikipedia.org/wiki/JMP_(x86_instruction)) have helpful information on this.

**(ii.)** Three possible ways to address operands in an instruction:

1. **Register Operands:** both operands are stored in general purpose registers.

2. **Immediate Operands:** one operand is included in instruction as a constant.

3. **Memory Operands:** operand is stored in a memory address location.

Immediate addressing is the fastest because it doesn't require any look-up (although the other operand is usually a register or memory address then) but register addressing is faster than memory addressing because it doesn't require any memory. For more information and examples see slides 14-20 of [Pentium Architecture: Registers & Addressing Modes](http://www.commsp.ee.ic.ac.uk/~kkleung/Computer_Systems_2015/5_Pentium1-2.ppt) or check out this [page](http://www.tutorialspoint.com/assembly_programming/assembly_addressing_modes.htm).

**(iii.)** Stack memory is a LIFO queue. The largest address is used as the beginning of the stack (the esp will point to the start of the stack) and the stack grows downwards in memory. When a function is called, the calling method first passes parameters. Then the called method sets up the frame pointer (ebp) and allocates local variables as necessary. The eip is also pushed to the stack (registers are saved) and the method is executed.  Once finished, the method results are copied to eax, the eip is pushed (registers are restored) and the local variable memory is deallocated.  The method returns and executes the next call (now in eip). [more information](http://www.commsp.ee.ic.ac.uk/~kkleung/Computer_Systems_2015/7_Pentium4-5.ppt).

###2 b.

The following program will calculate A[0] - A[1] + A[2] - A[3] +...+ A[n-2] - A[n-1]. n is a positive, even integer. I'm going to use the following registers as such:

Register | Use
---|----
R0 | counter
R1 | A (value)
R2 | not used
R3 | not used

Address | Contents            | Pseudocode
--------|---------------------|-------
080H    | LOAD R0, [302H]     | R0 = C
081H    | LOAD R1, [303H]     | R1 = 0
**082H**| **ADD R2, [301H]** | **A = A + B**
083H    | SUB R0, [304H]      | counter = counter - 1
084H    | IFZER R0, 088H      | if counter = 0, stop
085H    | IFNEG R0, 088H      | if counter < 0, stop
**086H**| **GOTO 082H**       | **if counter > 0, loop**
087H    | STORE R1, [300H]    | A = R1
088H    | STOP                | end the program
...     |                     |
300H    | A                   | holds result
301H    | B                   | holds B
302H    | C                   | holds C
303H    | 0                   | constant, 0
304H    | 1                   | constant, 1


##Section C
### 3 a.

### 3 b.

Synchronous Messages

Synchronous messaging involves a client that waits for the server to respond to a message. Messages are able to flow in both directions, to and from. Essentially it means that synchronous messaging is a two way communication. i.e. Sender sends a message to receiver and receiver receives this message and gives reply to the sender. Sender will not send another message until get reply from receiver.

Asynchronous Messages

Asynchronous messaging involves a client that does not wait for a message from the server. An event is used to trigger a message from a server. So even if the client is down , the messaging will complete successfully. Asynchronous Messaging means that, it is a one way communication and the flow of communication is one way only.

I assume the kernel has to maintain a buffer for asynchronous send but not for synchronous send. 


### 3 c.

The process schedule could feasibly run in a separate process, but such a design would be very inefficient since you would have to swap from one process to the scheduling process (which would then have to make several system calls to the kernel) and then back to the new process, as opposed to just placing the scheduler in the kernel where you will not need system calls nor need to swap contexts more than once. Therefore, the scheduler is generally in the exclusive realm of the kernel.

http://stackoverflow.com/questions/11769772/os-does-the-process-scheduler-runs-in-separate-process

### 3 d.


##Section D

### 4 a.

Direct memory access (DMA) is a feature of computer systems that allows certain hardware subsystems to access main system memory (RAM) independently of the central processing unit (CPU).

Without DMA, when the CPU is using programmed input/output, it is typically fully occupied for the entire duration of the read or write operation, and is thus unavailable to perform other work. 

I don't believe Ananda went over the parameters...

### 4 b.



Synchronous (one thread):

```
1 thread ->   |----A-----||-----B-----------||-------C------|
```

Synchronous (multi-threaded):

```
thread A -> |----A-----|   
                        \  
thread B ------------>   ->|-----B-----------|   
                                              \   
thread C ---------------------------------->   ->|-------C------| 
```

Asynchronous (one thread):

```
         A-Start ---------------------------------------- A-End   
           | B-Start ----------------------------------------|--- B-End   
           |   |     C-Start -------------------- C-End      |     |   
           V   V       V                           V         V     V      
1 thread-> |-A-|---B---|-C-|-A-|-C-|--A--|-B-|--C--|---A-----|--B--| 
```


Asynchronous (multi-Threaded):
```
 thread A ->     |----A-----|
 thread B ----->     |-----B-----------| 
 thread C --------->     |-------C----------|
```

Synchronized means "connected", or "dependent" in some way. In other words two synchronous tasks must be aware of one another, and one must execute in some way that is dependent on the other. In most cases that means that one cannot start until the other has completed. Asynchronous means they are totally independent and neither one must consider the other in any way, either in initiation or in execution.

As an aside, I should mention that technically, the concept of synchronous vs. asynchronous really does not have anything to do with threads. Although, in general, it would be unusual to find asynchronous tasks running on the same thread, it is possible, (see below for e.g.) and it is common to find two or more tasks executing synchronously on separate threads... No, the concept of synchronous/asynchronous has to do solely with whether or not a second or subsequent task can be initiated before the other task has completed, or whether it must wait. That is all. What thread (or threads), or processes, or CPUs, or indeed, what hardware, the task[s] are executed on is not relevant. Indeed, to make this point I have edited the graphics to show this.

ASYNCHRONOUS EXAMPLE. In solving many engineering problems, the software is designed to split up the overall problem into multiple individual tasks, and then execute them asynchronously. Inverting a matrix, or a finite element analysis problem, are good examples. In computing, sorting a list is an example. The quick sort routine, for example, splits the list into two lists, and sorts each of them by calling itself recursively. In both of the above examples, the two tasks can (and often were) executed asynchronously. They do not need to be on separate threads. Even a machine with one CPU, and only one thread of execution can be coded to initiate processing of a second task before a first one has completed. The only criterion is that the results of one task are not necessary as inputs to the other task. As long as the start and end times of the tasks overlap, (possible only if the output of neither is needed as inputs to the other), they are being executed asynchronously, no matter how many threads are in use.

SYNCHRONOUS EXAMPLE. Any process consisting of multiple tasks where the tasks must be executed in sequence, but one must be executed on another machine (Fetch and/or update data, get a stock quote from a financial service, etc.). If it's on a separate machine it is on a separate thread, whether synchronous or asynchronous.

http://stackoverflow.com/questions/748175/asynchronous-vs-synchronous-execution-what-does-it-really-mean

