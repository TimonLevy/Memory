# ANSWER SHEET

Shieeeeeet, if my memory serves me right. Here are some answers.

![](/Pictures/Hayadaata.png)

<br><br>

## MOST SIGNIFICANT BIT

Let's look at this byte. `0 0 0 0 0 0 1 0`, it might look like the value of this byte is obviously 2. <br>
_But is it?_

Well, to calculate the value of this byte is simply to take each lit bit and calculate it's power of two using it's index. But how do we know what the index of the bit is? what do we use as a reference?

Intro, the **most significant bit**.

The most significant bit is the bit in a binary number that holds the largest value, meaning the biggest power of two. This bit is usually the left-most, or the first transmitted. We will get to how do we know that in the future. MSB is the reference that we use to know what side to start our bit indexing from.

Let's get back to that supposedly 2 binary number from before. `0000 0010` if the MSB is the left-most bit, that would represent the largest number 2^7 (128). The right-most bit would represent 2^0 (1) then the bit that is right side to that one will represent 2. However if the right-most bit is the MSB, then the one right side to that will represent one power lower, so that binary number can be interperted as 2^6 which is 64 as well.

It's all depending on the MSB placement.

## BIG ENDIAN VS LITTLE ENDIAN

This relates the the prior answer, systems need to know where the MSB and LSB (least significant bit) are located in their binary structures. To answer that we have endianness.

> A **Big-Endian** system will place it's MSB at the beginning of a binary structure, at the smallest address and the LSB at the end of the structure. it will also transmit and recieve the MSB first.

> A **Little-Endian** is the opposite, it will store it's LSB at the lowest address and the MSB at the end, as well as sending and recieving the LSB first.

So, for example with the binary number from before.

```
BIG ENDIAN        |        LITTLE ENDIAN
                  |
MSB               0                  LSB
                  0
                  0
                  0

                  0
                  0
                  1
LSB               0                  MSB
                  |
Value:            |
2                 |                   64
```

A **little endian** system will keep the number 2 in memory like this: `0100 0000`

<br><br>

##

![](/Pictures/Hayadaata.png)


<br><br>

## WHAT IS PROTEC MODE AND WHAT IS REAL MODE

The difference between them is with the complexity of the access to the memory of an application and with how application memories are addressed.<br>
In the CPU there are registers which are tiny buffers that keep memory to be used for operations of the CPU, there is a cluster of registers called the segment registers, they are responsible to keep addresses of data to be used by the CPU.

For example the `Code Segment` register keeps the address of the beginning of the area in memory where the code of the current application is kept. The `Instruction Pointer` register is used to offset the `CS` register and this combination points to the next code instruction in memory that the CPU must execute. That was an explanation on how the cpu calculates the data addresses of the code of the application.

**Real mode** is the cpu mode of operation in which the CPU uses real physical address. In real mode, the `Code Segment` register will point to a segment of memory in the _real memory_ that belongs to the context of the current program. Then, the `Instruction Pointer` register will offset it to the current intruction and that's how a CPU will execute the application in real mode.

> Real Memory used to be the first 1M bytes in memory, today it just refers to the installed RAM installed in the motherboard.

However, that is unsafe since that can lead to overwriting memory written in that _real memory_. To counter that, **protected mode** was introduced with intel's 286 microprocessor.<br>
In it, instead of accessing the _real memory_ directly, the `CS` will point to a segment descriptor. It is a data structure that describes the start, length and access rights of a segment. The segment descriptors are kept in two large tables, called the `Global Descriptor Table` and `Local Descriptor Table`. Global contains the segment descriptor of all applications in it, while the local keeps only the current application's segment descriptors in it.

Afterwards with the introduction of the 386 microprocessor things changed again. **Paging** was added, using paging and a slew of other registers invisible to programs, programs were able to run in their own "confined" memory space. The program's memory is kept in structures called "_pages_" that are fixed in size and spread out in the _real memory_, then those pages are all mapped to one memory space that belongs to the program, no program can access other program's pages. This grants programs their "own" "seperated" memory space which they are free to operate in using their own virtual address ranges that are translated to the _real memory addresses_ where the data resides.

![](/Pictures/Protected_Mode_Meme.jpg)
  
**Privilege Rings** is another feature of protected mode where _operating system processes_ and _user processes_ are categorized into 4 privilege level ring from 0 - 3. 0 is the most priveleged level where are process can run, thus OS and driver processes run in those rings and 3 is where user processes will run. These rings exist in order to deny high privilege ring processes from accessing data, call gates or executing instructions which may jeopardize the integrity of the system.

In **real mode** the programs have access to _real memory_ addresses.<br>
In **protected mode** the programs have virtual addresses which are translate using pages, page tables and page directories.

<br>

## REGISTERS

Registers are memory caches inside the CPU that it uses to perform it's calculations and some more operations. Registers can be accessed in 64, 32, 16 and 8 bit modes where each mode of access is given a designated later: R (Register, 64 bit), E (Extended, 32 bit) and more. There are many types of registers:

#### **General Purpose Registers (GPR)**

> These are registers used for general purposes, here are some of them:
> * **AX** - Accumulator register. Used in arithmatic operations.
> * **CX** - Counter register. Used in shift instructions and counting iterations when doing loops.
> * **DX** - Used in arithmetic operations, like store remainder when doing division.

#### **Segment Registers**

> There are 6 of these:
> * **SS** - Stack Segment, pointer to the stack.
> * **CS** - Code Degment, pointer to the code.
> * etc..

#### **EFLAGS**

> This is a 32 bit register where each bit is a different flag used for and by operations, here are some examples of flags:
> * **ZF** - Zero Flag, is set if the result of an operation is zero. Used in if statements.
> * **SF** - Sign Flag, set if the result of an operation is negative.
> * **OF** - Overflow Flag, Set if the operation results in a number that is too large to contain.

#### Stupid Registers

> These are just some stupid regiters that have nothing in their brains, they are so stupid:
> ![](https://media.tenor.com/9RCIDZjkhBsAAAAC/hamster-meme.gif)
> ![](https://i.kym-cdn.com/news_feeds/icons/mobile/000/035/373/c98.jpg)

My favorite is the staring hamster, all he does is stare. There are **zero** thoughts going through his head right now. He is simply living the moment.

![](/Pictures/Oger_With_No_Brain.png)

<br><br>

#### Interrupt Descriptor Table

