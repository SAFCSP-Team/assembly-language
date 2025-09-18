
# Common Instructions in 8086 Assembly CheatSheet

## 1. Transfer Instructions
| Mnemonic | Example          | Description                              |
|--------------|----------------------------|----------------------------------------|
| **`MOV`**    | `MOV RAX, RBX`             | Copy data between registers/memory |
| **`PUSH`**   | `PUSH RAX`                 | Push value onto the stack|
| **`POP`**    | `POP RBX`                  | Pop value from stack into register |
| **`XCHG`**   | `XCHG RAX, RBX`            | Swap values** between operands       |
| **`LEA`**    | `LEA RBX, [RDI]`           | Load effective address             |

Example:
```asm
section .text
    mov rax, 1234h        ; Move immediate to RAX
    mov rbx, rax          ; Copy RAX to RBX
    push rax              ; Push RAX onto stack
    pop rcx               ; Pop top of stack into RCX
    xchg rax, rbx         ; Swap RAX and RBX
```


## 2. Arithmetic Instructions
| Mnemonic     | Example                    | Description                        |
|--------------|----------------------------|------------------------------------|
| **`ADD`**    | `ADD RAX, 1`               | Add source to destination          |
| **`ADC`**    | `ADC RAX, RBX`             | Add source + carry flag to dest.   |
| **`SUB`**    | `SUB RBX, RCX`             | Subtract source from destination   |
| **`SBB`**    | `SBB RAX, 1`               | Subtract source + carry flag       |
| **`INC`**    | `INC RCX`                  | Add 1 to operand                   |
| **`DEC`**    | `DEC RDX`                  | Subtract 1 from operand            |
| **`NEG`**    | `NEG RAX`                  | Two's complement (negate)          |
| **`CMP`**    | `CMP RAX, RBX`             | Compare operands, sets flags only  |
| **`MUL`**    | `MUL RCX`                  | Unsigned multiplication            |
| **`IMUL`**   | `IMUL RCX`                 | Signed multiplication              |
| **`DIV`**    | `DIV RBX`                  | Unsigned division                  |
| **`IDIV`**   | `IDIV RCX`                 | Signed division                    |

Example:
```asm
section .text
    add rax, 10           ; rax = rax + 10
    sub rbx, rcx          ; rbx = rbx - rcx
    inc rcx               ; rcx = rcx + 1
    dec rdx               ; rdx = rdx - 1
    neg rax               ; rax = -rax
    cmp rax, rbx          ; compare rax and rbx
    imul rcx              ; rax = rax * rcx (signed)
```

## 3. Logic Instructions
| Mnemonic | Example          | Description                           |
|----------|------------------|---------------------------------------|
| **`AND`**    | `AND RAX, 0Fh`  | Bitwise AND operation              |
| **`OR`**     | `OR RAX, RBX`   | Bitwise OR operation               |
| **`XOR`**    | `XOR RAX, RBX`  | Bitwise XOR operation              |
| **`NOT`**    | `NOT RBX`       | Flip all bits of operand           |
| **`TEST`**   | `TEST RAX, 1`   | AND operation, updates flags only  |
| **`SHL`**    | `SHL RAX, 1`    | Shift bits left, insert 0 on right |
| **`SHR`**    | `SHR RAX, 1`    | Shift bits right, insert 0 on left |

Example:
```asm
section .text
    and rax, 0xFF          ; rax = rax AND 0xFF
    or rax, rbx            ; rax = rax OR rbx
    not rbx                ; flip all bits in rbx
    shl rax, 2             ; rax = rax << 2 
    shr rbx, 1             ; rbx = rbx >> 1 
```

## 4. String Instructions

| Mnemonic    | Description                                               |
|--------------|----------------------------------------------------------------|
| **`MOVS`**   | Copy data from source to destination (`MOVSB` = byte, `MOVSQ` = quadword) |
| **`CMPS`**   | Compare source with destination (`CMPSB`= byte, `CMPSQ` = quadword)      |
| **`LODS`**   | Load source to `RAX` (`LODSB` = byte, `LODSQ` = quadword)                |
| **`STOS`**   | Store RAX at destination (`STOSB` = byte, `STOSQ` = quadword)           |

Example:
```asm
section .data
    src: dq 0x123456789ABCDEF0
    dest:dq 0

section .text
    lea rsi, [rel src]           ; Source pointer
    lea rdi, [rel dest]          ; Destination pointer
    movsq                        ; Move quadword from [RSI] to [RDI]
    cmpsq                        ; Compare quadword at [RSI] and [RDI]
    lodsq                        ; Load quadword at [RSI] into RAX
    stosq                        ; Store RAX at [RDI]
```

## 5. Jumps (Unsigned)

| Mnemonic     | Condition           | Description                       |
|--------------|---------------------|-----------------------------------|
| **`JMP`**        | —                       | Unconditional **jump** to label       |
| **`JE`** / **`JZ`**  | `ZF = 1`              | **Jump if result is zero**            |
| **`JNE`** / **`JNZ`**| `ZF = 0`              | **Jump if result is not zero**        |
| **`JA`** / **`JNBE`**| `CF = 0` and `ZF = 0` | For unsigned, **greater than**        |
| **`JAE`** / **`JNB`**| `CF = 0`              | Unsigned, **greater or equal**        |
| **`JB`** / **`JNAE`**| `CF = 1`              | Unsigned, **less than**               |
| **`JBE`** / **`JNA`**| `CF = 1` or `ZF = 1`  | Unsigned, **less or equal**           |
| **`JC`**         | `CF = 1`                | **Carry flag** set                    |
| **`JNC`**        | `CF = 0`                | **Carry flag** clear                  |
| **`JPE`**        | `PF = 1`                | **Parity flag** even                  |
| **`JPO`**        | `PF = 0`                | **Parity flag** odd                   |

Example:
```asm
section .text
    mov rax, 5
    mov rbx, 10
    cmp rax, rbx
    ja  greater_label    ; Jump if unsigned above (CF=0 and ZF=0)
    jb  less_label       ; Jump if unsigned below (CF=1)
    je  equal_label      ; Jump if equal (ZF=1)
greater_label:
    ; code for rax > rbx
    jmp done
less_label:
    ; code for rax < rbx
    jmp done
equal_label:
    ; code for rax == rbx
done:
```

## 6. Jumps (Signed)
| Mnemonic      | Condition              | Description                           |
|---------------|------------------------|---------------------------------------|
| **`JG`** / **`JNLE`** | `ZF = 0` and `SF = OF` | Signed, **greater than**              |
| **`JGE`** / **`JNL`** | `SF = OF`             | Signed, **greater or equal**          |
| **`JL`** / **`JNGE`** | `SF ≠ OF`             | Signed, **less than**                 |
| **`JLE`** / **`JNG`** | `ZF = 1` or `SF ≠ OF` | Signed, **less or equal**             |
| **`JS`**         | `SF = 1`               | **Sign flag set** (negative)          |
| **`JNS`**        | `SF = 0`               | **Sign flag clear** (positive)        |
| **`JO`**         | `OF = 1`               | **Overflow flag set**                 |
| **`JNO`**        | `OF = 0`               | **Overflow flag clear**               |

Example:
```asm
section .text
    mov rax, -5
    mov rbx, 10
    cmp rax, rbx
    jg  signed_greater    ; Jump if rax > rbx (signed)
    jl  signed_less       ; Jump if rax < rbx (signed)
    je  signed_equal      ; Jump if rax == rbx
signed_greater:
    ; code for rax > rbx (signed)
    jmp signed_done
signed_less:
    ; code for rax < rbx (signed)
    jmp signed_done
signed_equal:
    ; code for rax == rbx
signed_done:
```

## 7. Loop Instructions

| Mnemonic           | Description                                  |
|--------------------|----------------------------------------------|
| **`LOOP`**           | **Decrement RCX**, jump if `RCX ≠ 0`             |
| **`LOOPE`** / **`LOOPZ`**  | Decrement `RCX`, jump if `RCX ≠ 0` and `ZF = 1`  |
| **`LOOPNE`** / **`LOOPNZ`**| Decrement `RCX`, jump if `RCX ≠ 0` and `ZF = 0`  |

Example:
```asm

section .text
    mov     rcx, 5
loop_start:
    ; Loop body code here 
    dec     rax
    loop    loop_start     ; Decrement RCX, jump if not zero
    ; RCX == 0 here
```


