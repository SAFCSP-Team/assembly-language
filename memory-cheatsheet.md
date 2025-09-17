# Memory Cheatsheet
### What is the Memory?
Memory (or RAM) is a hardware component where data and programs are temporarily stored while a computer is running. It is **volatile**, meaning its contents are lost when the system powers off.

Memory is a collection of bytes, each with a **unique address**, used to store **data**.
<img width="3368" height="2382" alt="address-value@4x" src="https://github.com/user-attachments/assets/abcb92f2-7fbd-4a88-b1d3-8395e94bf269" />

## Memory Layout
<img width="3369" height="2382" alt="High-address@4x" src="https://github.com/user-attachments/assets/48a3ec71-78a3-4d7d-8187-def68275f343" />

## Segments
|Segment|Purpose|Grows|Example|
|:---------:|---------|:-------:|:------------:|
|.text|Stores program instructions (code)|Fixed|`section .text`|
|.rodata|	Read-only data (constants, literals)|	Fixed	|`section .rodata`|
|.data|Stores initialized global and static variables|Fixed|`section .data`|
|.bss |Stores uninitialized global and static variables|Fixed|`section .bss`|
|Heap|Stores dynamically allocated memory|Upwards|Allocated at runtime |
|Stack|Stores local variables, function call/return info|Downwards|Grows/shrinks on calls|

## Declaring Data in Assembly 
### x86-64 data types
| Name    | Directive | Size                | Example      |
|---------|-----------|---------------------|--------------|
| **BYTE**| `db`      | 1 byte (8 bits)     | `mybyte db 1`|
| **WORD**| `dw`      | 2 bytes (16 bits)   | `myword dw 2`|
| **DWORD**|`dd`      | 4 bytes (32 bits)   | `mydword dd 3`|
| **QWORD**|`dq`      | 8 bytes (64 bits)   | `myqword dq 4`|

## Addressing Memory
Addressing modes specify how to access memory or data.

|Name|Description|Example|
|-------|--------|-------|
|**Immediate Addressing** | Data is part of the instruction. | `MOV AX, 10 ; Move immediate value 10 to AX` |
|**Register Addressing** |Data is in a register.|` MOV AX, BX ; Move data from BX to AX`
|**Direct Addressing** |Access memory at a specific address.|`MOV AX, [1234h] ; Move value at memory address 1234 into AX`
|**Indirect Addressing** |The address is stored in a register.|`MOV AX, [BX] ; Move value at memory address in BX to AX`
|**Indexed Addressing** |Combines a base register and an index register.|`MOV AX, [BX + SI] ; source = BX + SI`
|**Base-Index with Displacement** |Combines a base register, index register, and a constant offset.|`MOV AX, [BX + SI + 10h] ; source = BX + SI + 10`

## Common Instructions

| Instruction         | Purpose                                     | Example                          |
|---------------------|---------------------------------------------|----------------------------------|
| `MOV dest, src`     | Copy data between registers/memory          | `MOV rax, [num]`                 |
| `ADD dest, src`     | Add source to destination                   | `ADD rax, 1`                     |
| `SUB dest, src`     | Subtract source from destination            | `SUB rax, rbx`                   |
| `INC reg`           | Increment register by 1                     | `INC rax`                        |
| `DEC reg`           | Decrement register by 1                     | `DEC rax`                        |
| `CMP reg, value`    | Compare register with value                 | `CMP rax, 0`                     |
| `LEA reg, [addr]`   | Load address into register (not value)      | `LEA rsi, [msg]`                 |
| `PUSH reg`          | Push register onto stack                    | `PUSH rax`                       |
| `POP reg`           | Pop value from stack into register          | `POP rax`                        |
| `call label`        | Call function (pushes return address)       | `call myfunc`                    |
| `ret`               | Return from function (pop address from stack)| `ret`                           |



