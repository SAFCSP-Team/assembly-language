# Stack Frame Cheatsheet
## What is the Stack?
The stack is a special section of a **program’s memory** used to **store temporary data**. It operates on a Last-In, First-Out (LIFO) principle. The stack is primarily used for:
- **Function calls and returns**
- **Storing local variables**
- **Saving register states**
  
Each time a function is called, a **new section of the stack called a `stack frame` is created** to hold that **function’s data**. When the **function finishes**, its **stack frame is destroyed**, and the stack returns to its previous state.

>[!Note]
>The stack grows **downward** to lower memory addresses.


## What is a Stack Frame?
A **stack frame** is a section of the **stack** dedicated to a single **function call**. It contains:
1. **Function parameters** (if not passed via registers)
2. **Local variables**
3. **Saved registers** (such as the **return address** and **base pointer**)


## Stack Frame Layout

| Stack Component         | Description                                                      |
|------------------------ |------------------------------------------------------------------|
| **Return Address**      | Address to return to after the function call                     |
| **Saved Base Pointer**  | Value of the caller function's base pointer (`EBP`)              |
| **Function Parameters** | Arguments passed to the function (via stack)                     |
| **Local Variables**     | Space allocated for **variables** that exist **only within the function** |
| **Scratch Registers**   | Registers that must be preserved (`EAX`, `ECX`, `EDX`, etc.)     |

## Basic Stack Instructions

| Instruction | Purpose                                            |
|-------------|---------------------------------------------------|
| `PUSH reg`  | **Push value** of register onto the stack         |
| `POP reg`   | **Pop top of stack** into register                |
| `CALL`      | **Call function** (push return address, jump)     |
| `RET`       | **Return from function** (pop return address, jump)|

## Creating and Destroying a Stack Frame

To manage a stack frame in **32-bit x86 assembly**, the following steps are typically performed:

### Creating a Stack Frame

```asm
push ebp            ; Save old base pointer
mov ebp, esp        ; Set new base pointer (frame pointer)
sub esp, 16         ; Allocate 16 bytes for local variables
```

### Destroying a Stack Frame

```asm
mov esp, ebp        ; Deallocate local variable space
pop ebp             ; Restore previous base pointer
ret                 ; Return to caller
```

## Register Usage in 32-bit x86

1. **Parameter Passing**:  
   - All arguments are **pushed onto the stack** (right to left) before the call.
   - The **caller** places arguments on the stack.
2. **Return Value**:  
   - The return value is stored in `EAX`.


## Example: Function with a Stack Frame

This example demonstrates a function that **adds two integers** (arguments passed on the stack) and returns the result in `EAX`.

```asm
section .text
global _start

_start:
    push 3                  ; Second argument (rightmost)
    push 5                  ; First argument
    call add_two_numbers    ; Call the function
    add esp, 8              ; Clean up the stack (2 args x 4 bytes)

    ; Result (8) is now in EAX

    mov eax, 1              ; syscall number for exit (Linux)
    xor ebx, ebx            ; exit code 0
    int 0x80                ; invoke system call

add_two_numbers:
    push ebp                ; Save old base pointer
    mov ebp, esp            ; Set new base pointer

    mov eax, [ebp+8]        ; First argument (5)
    add eax, [ebp+12]       ; Add second argument (3)

    mov esp, ebp            ; Restore stack pointer
    pop ebp                 ; Restore base pointer
    ret                     ; Return to caller
```
