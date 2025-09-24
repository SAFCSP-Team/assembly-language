# Memory Cheatsheet
### What is the Memory?
- **Memory** (**RAM**) is a hardware component where **data** and **programs** are temporarily stored while the computer is running.  
- It is **volatile**, meaning its contents are lost when the system powers off.
- **Memory** is a collection of **bytes**, each with a **unique address**, used to store **data**.
<img width="3368" height="2382" alt="address-value@4x (1)" src="https://github.com/user-attachments/assets/875e293c-4d79-41a0-9698-c2a205d3aba1" />


## Process's Memory Layout
<img width="3369" height="2382" alt="High-address@4x" src="https://github.com/user-attachments/assets/e2725b85-40d8-4a66-8fb2-6e10fb7c6498" />

> [!NOTE]
> This diagram explains the process layout on a Linux system. The layouts differ depending on the operating system.

## Segments
| Segment      | Purpose                                        | Grows        | Example              |
|:-----------: |:----------------------------------------------: |:------------:|:-------------------:|
| **.text**    | Stores **program instructions (code)**         | Fixed        | `section .text`      |
| **.rodata**  | **Read-only data** (constants, literals)       | Fixed        | `section .rodata`    |
| **.data**    | Stores **initialized global/static variables** | Fixed        | `section .data`      |
| **.bss**     | Stores **uninitialized global/static vars**    | Fixed        | `section .bss`       |
| **Heap**     | Stores **dynamically allocated memory**        | Upwards      | Allocated at runtime |
| **Stack**    | Local vars, call/return info                   | Downwards    | Grows/shrinks on calls |


## Declaring Data in Assembly 
### x86 (32-bit) data types

| Name        | Directive     | Size                | Example      |
|-------------|:-------------:|---------------------|---------------------|
| **BYTE**    | `db`          | 1 byte (**8 bits**) | `mybyte db 1`       |
| **WORD**    | `dw`          | 2 bytes (**16 bits**)| `myword dw 2`       |
| **DWORD**   | `dd`          | 4 bytes (**32 bits**)| `mydword dd 3`      |
| **QWORD**   | `dq`          | 8 bytes (**64 bits**)| `myqword dq 4`      |



## Addressing Memory
- **Immediate Addressing**: Data is part of the instruction.
```asm
mov eax, 10 ; Move immediate value 10 to EAX
```
- **Register Addressing**: Data is in a register.
```asm
mov eax, ebx ; Move data from EBX to EAX
```                              
- **Direct Addressing**: Access memory at a specific address.  
```asm
mov eax, [1234h] ; Move value at memory address 1234 into EAX
```
- **Indirect Addressing**: The address is stored in a register.
```asm
mov eax, [ebx] ; Move value at memory address in EBX to EAX
```            
- **Indexed Addressing**: Combines a base register and an index register.
```asm
mov eax, [ebx + esi] ; source = EBX + ESI
```                                                           
- **Base-Index with Displacement**: Combines a base register, index register, and offset.
```asm
mov eax, [ebx + esi + 10h] ; source = EBX + ESI + 10
``` 

## Common Instructions

| Instruction         | Purpose                                     | Example                          |
|---------------------|---------------------------------------------|----------------------------------|
| `MOV dest, src`      | **Copy data** between registers/memory       | `MOV EAX, [num]`               |
| `ADD dest, src`      | **Add source** to destination                | `ADD EAX, 1`                   |
| `SUB dest, src`      | **Subtract source** from destination         | `SUB EAX, EBX`                 |
| `INC reg`            | **Increment register** by 1                  | `INC EAX`                      |
| `DEC reg`            | **Decrement register** by 1                  | `DEC EAX`                      |
| `CMP reg, value`     | **Compare register** with value              | `CMP EAX, 0`                   |
| `LEA reg, [addr]`    | **Load address** into register (not value)   | `LEA ESI, [msg]`               |
| `PUSH reg`           | **Push register** onto stack                 | `PUSH EAX`                     |
| `POP reg`            | **Pop register** from stack into register    | `POP EAX`                      |
| `CALL label`         | **Call function** (pushes return address)    | `CALL myfunc`                  |
| `RET`                | **Return from function** (pops address)      | `RET`                          |

Example:
```asm
section .data
num         dd  42             ; DWORD (4 bytes) variable at label 'num'
array       dd  10, 20, 30, 40 ; DWORD array (4 elements)

section .text
global _start

_start:
    ; Immediate Addressing
    mov     eax, 123           ; EAX = 123

    ; Register Addressing
    mov     ebx, eax           ; EBX = EAX

    ; Direct Addressing (label)
    mov     eax, [num]         ; EAX = value at address 'num' (42)

    ; Indirect Addressing
    mov     ecx, num           ; ECX = address of 'num'
    mov     edx, [ecx]         ; EDX = value at address in ECX (42)

    ; Indexed Addressing (array access)
    mov     esi, 2             ; index = 2
    mov     eax, [array + esi*4] ; EAX = array[2] (30), address of array + 2*4 (DWORD offset = 4)

    ; Base-Index + Displacement
    mov     ebx, array         ; EBX = address of array
    mov     esi, 1             ; index = 1
    mov     eax, [ebx + esi*4 + 4] ; EAX = array[1 + 1] = array[2] (30)
```
