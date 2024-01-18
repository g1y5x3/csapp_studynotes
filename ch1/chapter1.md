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
each with its own

An L1 cache on the processor chips holds tens of thousands of bytes and can be accessed nearly as fast as the register file. A larger L2 cache with
hundreds of thousands to millions of bytes is connected to the processor by a special bus. It might take 5 times longer for the processor to access
the L2 cache than the L1 cache, but is still 5 to 10 times faster than accessing the main memory. The L1 and L2 caches are implemented with a
hardware technology known as *static random access memory (SRAM)*.


|   |         |
|---|---------|
|L0 | Regs    |
|---|---------|
|L1 | L1 cache|
|---|---------|
