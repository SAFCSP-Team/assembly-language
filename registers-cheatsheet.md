# Registers Cheatsheet

**Registers** are **small**, **fast storage located** inside the **CPU**, and used to perform operations and hold data.


## General-Purpose Registers (GPRs)

These **registers** are used for **arithmetic**, **data movement**, and **logic operations**. Each **register** can be accessed in different sizes: **64-bit**, **32-bit**, **16-bit**, and **8-bit**. For **8-bit registers**, the lower and higher halves are separately accessible.

|64-bit | 32-bit | 16-bit | 8-bit High (`bits 8–15`) | 8-bit Low (`bits 0–7`) | Purpose                                                         |
|:------:|:------:|:-----:|:-----------------------:|:----------------------:|------------------------------------------------------------------|
| RAX    | EAX    | AX     | AH                      | AL              | **Accumulator** for **arithmetic**, **logic**, and **I/O operations**  |
| RBX    | EBX    | BX     | BH                      | BL              | **Base register**, often used for **address calculations**             |
| RCX    | ECX    | CX     | CH                      | CL              | **Counter** for **loops**, **shifts**, and **string operations**       |
| RDX    | EDX    | DX     | DH                      | DL | **Data register**, often used for **I/O** and **multiplication/division operations**|
| RSI    | ESI    | SI     | -                       | -                          | **Source index** for **string/memory operations**           |
| RDI    | EDI    | DI     | -                       | -                          | **Destination index** for **string/memory operations**      |
| RBP    | EBP    | BP     | -                       | -                          | **Base pointer** for **stack frames** in **function calls** |
| RSP    | ESP    | SP     | -                       | -                          | **Stack pointer** for the **current stack location**        |
| R8     | R8D    | R8W    | R8B                     |-                         | An additional **general-purpose register** in **64-bit mode** |
| R9     | R9D    | R9W    | R9B                     | -                        | An additional **general-purpose register** in **64-bit mode** |
| R10    | R10D   | R10W   | R10B                    | -                        | An additional **general-purpose register** in **64-bit mode** |
| R11    | R11D   | R11W   | R11B                    | -                        | An additional **general-purpose register** in **64-bit mode** |
| R12    | R12D   | R12W   | R12B                    | -                        | An additional **general-purpose register** in **64-bit mode** |
| R13    | R13D   | R13W   | R13B                    | -                        | An additional **general-purpose register** in **64-bit mode** |
| R14    | R14D   | R14W   | R14B                    | -                        | An additional **general-purpose register** in **64-bit mode** |
| R15    | R15D   | R15W   | R15B                    | -                        | An additional **general-purpose register** in **64-bit mode** |

Example:
```asm
; Add two numbers 
mov     eax, 10        ; EAX = 10
mov     ebx, 32        ; EBX = 32
add     eax, ebx       ; EAX = EAX + EBX (EAX = 42)
```

## Special-Purpose Registers
### Instruction Pointer (IP) Registers
| 64-bit | 32-bit | 16-bit | Purpose |
|:------:|:------:|:------:|:-------:|
| RIP    | EIP    | IP     | **Instruction Pointer** holds the **address** of the next **instruction** to be executed. |

Example:
```asm
; Instruction pointer with a jump
jmp     skip        ; The value of EIP points to 'mov eax, 2' after the jump
mov     eax, 1      ; This instruction is skipped
skip:
mov     eax, 2      ; Execution continues here
```

### Flags Register
The **EFLAGS Register** contains **status** and **control flags** used by the **CPU**.

| Flag   | Label     | Bit | Purpose                                                                             |
|:-------|:----------|:----|:------------------------------------------------------------------------------------|
| **CF** | Carry Flag     | 0   | Set if an **arithmetic operation** generates a **carry/borrow**.                |
| **ZF** | Zero Flag      | 6   | Set if the **result** of an **operation** is **zero**.                              |
| **SF** | Sign Flag      | 7   | Set if the **result** is **negative**.                                              |
| **OF** | Overflow Flag  | 11  | Set if an **arithmetic operation** overflows a **signed number**.               |
| **PF** | Parity Flag    | 2   | Set if the number of **set bits** in the result is **even**.                    |
| **AF** | Auxiliary Flag | 4   | Used in **BCD (binary-coded decimal)** operations.                              |
| **DF** | Direction Flag | 10  | Determines **string operation direction** (`0` = **increment**, `1` = **decrement**). |
| **IF** | Interrupt Flag | 9   | Enables (`1`) or disables (`0`) **maskable hardware interrupts**.               |

> [!NOTE]
> Most used flags: **CF**, **ZF**, **SF**, **OF**. 

Example:
```asm
mov     eax, 5
sub     eax, 5      ; EAX = 0, Zero Flag (ZF) is set
jz      label_zero  ; Jump if Zero Flag is set
mov     ebx, 1      ; Skipped if EAX == 0
label_zero:
mov     ebx, 0      ; Execute if Zero Flag was set (EAX == 0)
```


