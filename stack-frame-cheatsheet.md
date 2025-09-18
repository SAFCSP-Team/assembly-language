# Stack Frame Cheatsheet
### What is the Stack?
The stack is a special section of a **program’s memory** used to **store temporary data**. It operates on a Last-In, First-Out (LIFO) principle. The stack is primarily used for:
- **Function calls and returns**
- **Storing local variables**
- **Saving register states**
  
Each time a function is called, a **new section of the stack called a `stack frame` is created** to hold that **function’s data**. When the **function finishes**, its **stack frame is destroyed**, and the stack returns to its previous state.

### What is a Stack Frame?

A **stack frame** is a section of the **stack** dedicated to a single **function call**. It contains:
1. **Function parameters** (if not passed via registers)
2. **Local variables**
3. **Saved registers** (such as the **return address** and **base pointer**)

>[!Note]
>The stack grows **downward** (toward lower memory addresses). When a **function is called**, a new stack frame is created; when it returns, the frame is destroyed.

## Stack Frame Layout
| Stack Component      | Description                                                                 |
|---------------------------|---------------------------------------------------------------------------------|
| **Return Address**        | Address to return to after the function call                                   |
| **Saved Base Pointer (RBP)** | Value of the caller function's base pointer                                 |
| **Function Parameters**   | Passed arguments to the function (when not passed via registers)              |
| **Local Variables**       | Space allocated for **variables** that exist **only within the function**              |
| **Scratch Registers**     |  Registers that must be preserved (`RAX`, `RCX`, `RDX`, etc.)        |


## Basic Stack Instructions

| Instruction | Purpose                                                 |
|-----------------|--------------------------------------------------------------|
| `PUSH reg`      | **Push value** of register onto the stack                        |
| `POP reg`       | **Pop top of stack** into register                               |
| `MOV`           | **Move data** between registers or memory                        |
| `LEA`           | **Load Effective Address** for pointer arithmetic             |
| `CALL label`    | **Call function** (push return address, jump to label)           |
| `RET`           | **Return from function** (pop return address, jump to it)        |


## Creating and Destroying a Stack Frame
To manage a stack frame in x86-64 assembly, the following steps are typically performed:

### Creating a Stack Frame
```asm
push rbp            ; Save old base pointer
mov rbp, rsp        ; Set new base pointer (frame pointer)
sub rsp, 16         ; Allocate 16 bytes for local variables
```
### Destroying a Stack Frame
```asm
mov rsp, rbp        ; Deallocate local variable space
pop rbp             ; Restore previous base pointer
ret                 ; Return to caller
```

## Register Usage in x86-64
1. **Parameter Passing**: 
   - The first six arguments are passed via registers:
     - `RDI`, `RSI`, `RDX`, `RCX`, `R8`, `R9`
   - Additional arguments are passed on the stack.
2. **Return Value**:
   - The return value of a function is stored in `RAX`.
  

## Example: Function with a Stack Frame

This example demonstrates a function that **adds two integers** (passed in `RDI` and `RSI`) and returns the result in `RAX`.

```asm
section .text
global _start

_start:
    mov rdi, 5              ; First argument (5)
    mov rsi, 3              ; Second argument (3)
    call add_two_numbers    ; Call the function
    ; Result (8) is now in RAX

    mov rax, 60             ; syscall number for exit
    xor rdi, rdi            ; exit code 0
    syscall                 ; invoke system call

add_two_numbers:
    push rbp                ; Save old base pointer
    mov rbp, rsp            ; Set new base pointer

    mov rax, rdi            ; Copy first argument to RAX
    add rax, rsi            ; Add second argument

    mov rsp, rbp            ; Restore stack pointer
    pop rbp                 ; Restore base pointer
    ret                     ; Return to caller
```
