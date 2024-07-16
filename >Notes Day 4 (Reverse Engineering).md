# Assembly Code
* There are 16 General purpose registers
  - %rax - The first return register
  - %rbp - The base pointer that keeps track if the base of the stack
  - %rsp - The stack pointer that points to the top of the stack
### Common Terms
* HEAP - Memory that can be allocated and deallocated
* STACK - A contiguous section of memory used for passing arguments
* GENERAL REGISTER - A multipurpose register that can be used by either programmer or user to store data or a memory location address
* CONTROL REGISTER - A processor register that changes or controls the behavior of a CPU
* FLAGS REGISTER - Contains the current state of the processor
### Memory Offset
* Instruction Pointer - holds address for next instruction to be executed
  - RIP (64-Bit)
  - EIP (Lower 32 Bits)
  - IP (Lower 16 Bits)
### Common Instruction Pointers
* MOV  - move source to destination
* PUSH - push source onto stack
* POP  - Pop top of stack to destination
* INC  - Increment source by 1
* DEC  - Decrement source by 1
* ADD  - Add source to destination
* SUB  - Subtract source from destination
* CMP  - Compare 2 values by subtracting them and setting the %RFLAGS register. ZeroFlag set means they are the same.
* JMP  - Jump to specified location
* JLE  - Jump if less than or equal
* JE   - Jump if equal
