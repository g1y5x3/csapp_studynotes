# Chapter 1 A Tour of Computer Systems
All information in a system - including disk files, programs stored in memory, 
user data stored in memory, and data transferred across a network - is 
represented as a bunch of bits.

In order to run `hello.c` on the system, the individual C statements must be
translated by other programs into a sequence of low-level *machine-language*
instructions. These instructions are then packaged in a form called an 
*executable object program* and stored.

The compilation system:
1. preprocessor
2. compiler
3. assembler
4. linker

A processor appears to operate according to a very simple instruction execution
model, definted by its *instruction set architecture*.

Physically, main memory consists of a collection of dynamic random access 
memory (DRAM) chips. Logically, memory is organized as a linear array of bytes,
each with its own unique address (array index) starting at zero. 

An L1 cache on the processor chips holds tens of thousands of bytes and can be 
accessed nearly as fast as the register file. A larger L2 cache with hundreds 
of thousands to millions of bytes is connected to the processor by a special 
bus. It might take 5 times longer for the processor to access the L2 cache than 
the L1 cache, but is still 5 to 10 times faster than accessing the main memory.
The L1 and L2 caches are implemented with a hardware technology known as 
*static random access memory (SRAM)*.

|   |                                       |
|---|---------------------------------------|
|L0 | Regs                                  |
|L1 | L1 cache (SRAM)                       |
|L2 | L2 cache (SRAM)                       |
|L3 | L3 cache (SRAM)                       |
|L4 | Main memory (DRAM)                    |
|L5 | Local secondary storage (local disks) |
|L6 | Remote secondary storage              |

We can think of the operating system as a layer of software interprosed between
the application program and the hardware. The operating system has two primary
purposes:
1. to protect the hardware from misuse by runaway applications and 
2. to provide applications with simple and uniform mechanisms for manipulating
complicated and often wildly different low-level hardware devices.

## The Operating System Manages the Hardware
The operating system achieves both goals via the fundamental abstractions:
- processes/threads
- virtual memory
- files

### process
A process is the operating system's *abstraction* for a running program.
Multiple processes can run concurrently on the same sytem, and each process
*appears* to have exclusive use of the hardware.

When the operating system decides to transfer control from the current process
to some new process, it performs a context switch by saving the context of the
current process, restoring the context of the new process, and then passing
control to the new process.

The transition from one process to another is managed by the operating system
kernel. The kernel is the portion of the operating system code that is always
resident in memory. When an application program requires some action by the
operating system, such as to read or write a file, it executes a special system
call instruction, transferring control to the kernel. The kernel then performs
the requested operation and returns back to the application program. Note that
the kernel is not a separate process. Instead, it is a collection of code and
data structures that the system uses to manage all the prodcesses.

### virtual memory
- program code and data
- heap (expands and contracts dynamically at run time as a result of calls to C
standard library routines such as `malloc` and `free`)
- shared libraries (e.g C standard library and the math library)
- stack (the compiler uses to implement function calls)
- kernel virtual memory

### files
A file is a sequence of bytes, nothing more and nothing less. Every I/O device,
including disks, keyboards, displays, and even networks, is modeled as a file.

## Concurrency and Parallelism
- Thread-Level Concurrency

  Hyperthreading, sometimes called simultaneous multi-threading, is a technique
  that allows a single CPU to execute multiple flows of control. It involves
  having multiple copies of some of the CPU hardward, such as program counters
  and register files, while having only single copies of other parts of the
  hardward, such as the units that perform floating-point arithmetic.

- Instruction-Level Parallelism
- Single-Instruction, Multiple-Data (SIMD) Parallelism

  For example, recent generations of intel and AMD processors have instructions
  that can add 8 pairs of single precision floating-point numbers in parallel.
