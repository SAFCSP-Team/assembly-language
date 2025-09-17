# Memory Cheatsheet
### What is the Memory?
- **Memory** (**RAM**) is a hardware component where **data** and **programs** are temporarily stored while the computer is running.  
- It is **volatile**, meaning its contents are lost when the system powers off.
- **Memory** is a collection of **bytes**, each with a **unique address**, used to store **data**.
<img width="3368" height="2382" alt="address-value@4x (1)" src="https://github.com/user-attachments/assets/875e293c-4d79-41a0-9698-c2a205d3aba1" />


## Process's Memory Layout
<img width="3369" height="2382" alt="High-address@4x" src="https://github.com/user-attachments/assets/48a3ec71-78a3-4d7d-8187-def68275f343" />

## Segments
|Segment       |Purpose                                           |Grows         |Example                   |
|:------------:|--------------------------------------------------|:------------:|:------------------------:|
| **.text**    | Stores **program instructions (code)**           | Fixed        | `section .text`          |
| **.rodata**  | **Read-only data** (constants, literals)         | Fixed        | `section .rodata`        |
| **.data**    | Stores **initialized global and static variables**| Fixed        | `section .data`         |
| **.bss**     | Stores **uninitialized global and static variables**| Fixed     | `section .bss`           |
| **Heap**     | Stores **dynamically allocated memory**          | Upwards      | Allocated at runtime     |
| **Stack**    | Stores **local variables**, **function call/return info** | Downwards | Grows/shrinks on calls |




## Declaring Data in Assembly 
### x86-64 data types
| Name        | Directive     | Size                | Example      |
|-------------|:-------------:|---------------------|---------------------|
| **BYTE**    | `db`          | 1 byte (**8 bits**)| `mybyte db 1`       |
| **WORD**    | `dw`          | 2 bytes (**16 bits**)| `myword dw 2`       |
| **DWORD**   | `dd`          | 4 bytes (**32 bits**)| `mydword dd 3`      |
| **QWORD**   | `dq`          | 8 bytes (**64 bits**)| `myqword dq 4`      |


## Addressing Memory
- **Immediate Addressing**: Data is part of the instruction.
```asm
MOV RAX, 10 ; Move immediate value 10 to RAX
```                            
- **Register Addressing**: Data is in a register.
```asm
MOV RAX, RBX ; Move data from RBX to RAX
```                              
- **Direct Addressing**: Access memory at a specific address.  
```asm
MOV RAX, [1234h] ; Move value at memory address 1234 into RAX
```           
- **Indirect Addressing**: The address is stored in a register.
```asm
MOV RAX, [RBX] ; Move value at memory address in RBX to RAX
```            
- **Indexed Addressing**: Combines a base register and an index register.
```asm
MOV RAX, [RBX + RSI] ; source = RBX + RSI
```                                
- **Base-Index with Displacement**: Combines a base register, index register, and offset.
```asm
- MOV RAX, [RBX + RSI + 10h] ; source = RBX + RSI + 10
``` 


## Common Instructions

| Instruction         | Purpose                                     | Example                          |
|---------------------|---------------------------------------------|----------------------------------|
| `MOV dest, src`      | **Copy data** between registers/memory       | `MOV RAX, [num]`               |
| `ADD dest, src`      | **Add source** to destination                | `ADD RAX, 1`                   |
| `SUB dest, src`      | **Subtract source** from destination         | `SUB RAX, RBX`                 |
| `INC reg`            | **Increment register** by 1                  | `INC RAX`                      |
| `DEC reg`            | **Decrement register** by 1                  | `DEC RAX`                      |
| `CMP reg, value`     | **Compare register** with value              | `CMP RAX, 0`                   |
| `LEA reg, [addr]`    | **Load address** into register (not value)   | `LEA RSI, [msg]`               |
| `PUSH reg`           | **Push register** onto stack                 | `PUSH RAX`                     |
| `POP reg`            | **Pop value** from stack into register       | `POP RAX`                      |
| `CALL label`         | **Call function** (pushes return address)    | `CALL myfunc`                  |
| `RET`                | **Return from function** (pops address from stack)| `RET`                     |



