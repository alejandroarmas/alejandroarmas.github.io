+++
title = "Breaking Down Virtual Memory: The Role of Paging in Modern Operating Systems"
author = "Alejandro Armas"
tags = ["Programming", "Operating Systems"] 
date = 2021-05-21
+++



### Introduction

Have you ever wondered why 32-bit and 64-bit get thrown around and not know what it meant? So too did I. Well the simple answer is that these refer to the amount of memory addressable to a program or more accurately, the computer architectures bit width i.r.t registers and address busses.

Now let's see how much this amounts to:
  {{< katex "2^{32} = 4,294,967,296" true />}}  Bytes or more succincly 4GiB. In modern days we are able to address  {{< katex "2^{64} = 18,446,744,073,709,551,616" true />}}  Bytes or 16.0 exabytes (EB). That's just over the amount of storage [Google uses](https://www.quora.com/Is-a-megabyte-larger-than-a-gigabyte) (circa 2018)! I highly doubt we will have machines with that much RAM soon *unless... we find a way to download more* 😆

Now the topic of today is tangential to what I just talked about, but nonetheless super interesting. Lets dive in. 

### Virtualizing Memory 

Every process in the **Operating System (OS)** is given the impression that it is working with a large contiguous section of memory. 

Behind the scenes, the OS is secretly multiplexing address spaces across physical memory. The memory of a process is physically fragmented across the RAM or even *paged out* to an auxillary store, like a disk drive or SSD, if seldom used and/or if the memory is at capacity.

This is important since it provides a notion of *isolation and protection* between processes. 

You wouldn't want some shitty javascript program in your browser to be able to access the same memory as your word processing program (Microsoft Word!) and reading your darkest secrets! 😱

In addition to this, virtualizing memory adds *portability* to your programs since they don't have to worry about where they are physically placed and allows a process to *address a size of memory different than what is physically available* on a machine.

Originally this confusing topic was concieved due to the **huge** disparity between the capacity of cache and disk drives in the [late 60's to early 70's](http://denninginstitute.com/itcore/virtualmemory/vmhistory.html), thus the desire to address memory larger than what was physically available was a natural need. 

### Early Attempts

Early approaches in space multiplexing involved methods like **Base and Bounds** or **segmentation** which allotted a process a bound and base to its address space and a physical offset.
Segmentation is a generalization of base and bounds. Offering *multiple* base and bounds across physical memory.
> In the hardware these are then stored in registers so that we are able to return a process back to its architectural state after a context switch. See [Concurrency](/2021/04/29/concurrency.html).
 
Now the problem with this is that memory would then be fragmentented, such that you concievably run into a problem of not being able to allot enough space for a new process! That is bad.

Interestingly the x86 ISA supported segmentation up until x86-64 starting around 2003.

### Paging

{{< figure src="/posts/memory/images/X86_Paging_4K.svg" alt="Function Graphed" caption="Figure 1. Two-level page table structure (Source: [Wikipedia)](https://en.wikipedia.org/wiki/Page_table)" class="figure-container">}}


Paging is really the same thing as segmentation, however these segments are of fixed size and referred to as a **page**. Simply it's a contiguous sequence of bits, often 4 KiB

Consider the RV32 ISA (Risc-V). A **virtual address** *could* be cut up like this:

|        31-22        |     21-0      |
|---------------------|---------------|
| virtual page number |  page offset  |

The operating system then translates these virtual addresses to physical ones with the help of a data structure called a **page table** which you can imagine as a rather large array where each **page table entry** (value retrieved when you index) is a pointer to another page in memory. Often times this entry could be a **physical table entry**.


This means in this first level of the page table, you got 10 bits to choose a **physical table entry**  {{< katex "2^{10} = 1024" true />}}  options. Thats 1024 pages to choose from.. nice. 

Each of those 1024 pages has  {{< katex "2^{22} = 4,194,304" true />}}  potential **physical table entries** as its page table entries.

|        31-10         |        9-0        |
|----------------------|-------------------|
| physical page number |  permission bits  |


In total that gives us  {{< katex "2^{34}" true />}}  addressible bytes (16GiB). *Remember those offset bits?* This is an address space allotted to a process larger than what's physically available! Cool.

#### Other Details

There is also auxiliary information about the page it's permission bits such as a present bit, a dirty bit, write bit, read bit, execute bit, process ID information, amongst others.

Intuitively it makes sense that some pages allotted to the process should be read-only (ex. code segment). Additionally your favorite error *segmentation fault* is derived from the fact that sometimes your program attempts to use an address which when translated, accesses a page of memory *without* the appropriate permission bits.


Since it is *wasteful* to organize our pages this way, we typical use **hierarchical page tables** where a page table entry points to page where again its page table entries point to *another* page and so forth. This forms a tree structure.


The reason this is more efficient is because the address space of a process typically occupies the top and bottom parts of the address space therefor page table entries are not full.



There are some other nuances of interest; sometimes the pages within a process' page table could be shared with another process. 

This typically occurs when a process is forked, when a process builds its program with a shared library (ex. C++ Standard Library `.so` `.dll` file types), or works with the same file as another process to maintain a consistent file state.
