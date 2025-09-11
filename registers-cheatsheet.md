# Registers Cheatsheet
### What are registers?
Registers are small, fast storage locations inside the CPU used to perform operations and hold data.

## General-Purpose Registers (GPRs)

These registers are used for arithmetic, data movement, and logic operations. Each register can be accessed in different sizes: **64-bit**, **32-bit**, **16-bit**, and **8-bit**. For 8-bit registers, the lower and higher halves are separately accessible.

| Register | 64-bit | 32-bit | 16-bit | 8-bit High (`bits 8–15`)| 8-bit Low (`bits 0–7`) | Purpose                                                                    |
|:--------:|:------:|:------:|:------:|:---------------------------:|------------------------|----------------------------------------------------------------------------|
| **RAX**  | RAX    | EAX    | AX     | AH                          | AL                     | Accumulator for arithmetic, logic, and I/O operations.                     |
| **RBX**  | RBX    | EBX    | BX     | BH                          | BL                     | Base register, often used for address calculations.                        |
| **RCX**  | RCX    | ECX    | CX     | CH                          | CL                     | Counter for loops, shifts, and string operations.                          |
| **RDX**  | RDX    | EDX    | DX     | DH                          | DL                     | Data register, often used for I/O and multiplication/division operations.  |
| **RSI**  | RSI    | ESI    | SI     | -                           | -                      | Source index for string/memory operations.                                 |
| **RDI**  | RDI    | EDI    | DI     | -                           | -                      | Destination index for string/memory operations.                            |
| **RBP**  | RBP    | EBP    | BP     | -                           | -                      | Base pointer for stack frames in function calls.                           |
| **RSP**  | RSP    | ESP    | SP     | -                           | -                      | Stack pointer for the current stack location.                              |
| **R8**   | R8     | R8D    | R8W    | R8B                         | -                      | An additional general-purpose register, offering more flexibility in 64-bit mode.|
| **R9**   | R9     | R9D    | R9W    | R9B                         | -                      | An additional general-purpose register, offering more flexibility in 64-bit mode.|
| **R10**  | R10    | R10D   | R10W   | R10B                        | -                      | An additional general-purpose register, offering more flexibility in 64-bit mode.|
| **R11**  | R11    | R11D   | R11W   | R11B                        | -                      | An additional general-purpose register, offering more flexibility in 64-bit mode.|
| **R12**  | R12    | R12D   | R12W   | R12B                        | -                      | An additional general-purpose register, offering more flexibility in 64-bit mode.|
| **R13**  | R13    | R13D   | R13W   | R13B                        | -                      | An additional general-purpose register, offering more flexibility in 64-bit mode.|
| **R14**  | R14    | R14D   | R14W   | R14B                        | -                      | An additional general-purpose register, offering more flexibility in 64-bit mode.|
| **R15**  | R15    | R15D   | R15W   | R15B                        | -                      | An additional general-purpose register, offering more flexibility in 64-bit mode.|

## Special-Purpose Registers
### Instruction Pointer (IP) Registers
| 64-bit | 32-bit | 16-bit | Purpose |
|:------:|:------:|:------:|:-------:|
| RIP        | EIP        | 	IP       | Instruction Pointer holds the address of the next instruction to be executed.|



### **Flags Register**
The Flags Register (RFLAGS in 64-bit mode) contains status and control flags used by the CPU.

| **Flag**    | **Label**      | **Bit** | **Purpose**                                                                              |
|:-----------:|:--------------:|:-------:|:----------------------------------------------------------------------------------------:|
| **CF**      |Carry Flag      | 0       | Set if an arithmetic operation generates a carry/borrow.                                 |
| **ZF**      |Zero Flag       | 6       | Set if the result of an operation is zero.                                               |
| **SF**      |Sign Flag       | 7       | Set if the result is negative.                                                           |
| **OF**      |Overflow Flag   | 11      | Set if an arithmetic operation overflows a signed number.                                |
| **PF**      |Parity Flag     | 2       | Set if the number of set bits in the result is even.                                     |
| **AF**      |Auxiliary Flag  | 4       | Used in BCD (binary-coded decimal) operations.                                           |
| **DF**      |Direction Flag  | 10      | Determines string operation direction (`0` = increment, `1` = decrement).                |
| **IF**      |Interrupt Flag  | 9       | Enables (`1`) or disables (`0`) maskable hardware interrupts.                            |

Most used flags: CF, ZF, SF, OF



