# Common Instructions in X86 Assembly CheatSheet

## 1. Transfer Instructions
| Mnemonic | Example          | Description                              |
|--------------|----------------------------|----------------------------------------|
| **`MOV`**    | `MOV EAX, EBX`             | Copy data between registers/memory |
| **`PUSH`**   | `PUSH EAX`                 | Push value onto the stack|
| **`POP`**    | `POP EBX`                  | Pop value from stack into register |
| **`XCHG`**   | `XCHG EAX, EBX`            | Swap values between operands       |
| **`LEA`**    | `LEA EBX, [EDI]`           | Load effective address             |

Example:
```asm
section .text
    mov eax, 1234h        ; Move immediate to EAX
    mov ebx, eax          ; Copy EAX to EBX
    push eax              ; Push EAX onto stack
    pop ecx               ; Pop top of stack into ECX
    xchg eax, ebx         ; Swap EAX and EBX
```


## 2. Arithmetic Instructions
| Mnemonic     | Example                    | Description                        |
|--------------|----------------------------|------------------------------------|
| **`ADD`**    | `ADD EAX, 1`               | Add source to destination          |
| **`ADC`**    | `ADC EAX, EBX`             | Add source + carry flag to dest.   |
| **`SUB`**    | `SUB EBX, ECX`             | Subtract source from destination   |
| **`SBB`**    | `SBB EAX, 1`               | Subtract source + carry flag       |
| **`INC`**    | `INC ECX`                  | Add 1 to operand                   |
| **`DEC`**    | `DEC EDX`                  | Subtract 1 from operand            |
| **`NEG`**    | `NEG EAX`                  | Two's complement **(negate)**      |
| **`CMP`**    | `CMP EAX, EBX`             | Compare operands, sets flags only  |
| **`MUL`**    | `MUL ECX`                  | Unsigned multiplication            |
| **`IMUL`**   | `IMUL ECX`                 | Signed multiplication              |
| **`DIV`**    | `DIV EBX`                  | Unsigned division                  |
| **`IDIV`**   | `IDIV ECX`                 | Signed division                    |

Example:
```asm
section .text
    add eax, 10           ; eax = eax + 10
    sub ebx, ecx          ; ebx = ebx - ecx
    inc ecx               ; ecx = ecx + 1
    dec edx               ; edx = edx - 1
    neg eax               ; eax = -eax
    cmp eax, ebx          ; compare eax and ebx
    imul ecx              ; eax = eax * ecx (signed)
```


## 3. Logic Instructions
| Mnemonic | Example          | Description                           |
|----------|------------------|---------------------------------------|
| **`AND`**    | `AND EAX, 0Fh`  | Bitwise AND operation              |
| **`OR`**     | `OR EAX, EBX`   | Bitwise OR operation               |
| **`XOR`**    | `XOR EAX, EBX`  | Bitwise XOR operation              |
| **`NOT`**    | `NOT EBX`       | Flip all bits of operand           |
| **`TEST`**   | `TEST EAX, 1`   | AND operation, updates flags only  |
| **`SHL`**    | `SHL EAX, 1`    | Shift bits left, insert 0 on right |
| **`SHR`**    | `SHR EAX, 1`    | Shift bits right, insert 0 on left |

Example:
```asm
section .text
    and eax, 0xFF          ; eax = eax AND 0xFF
    or eax, ebx            ; eax = eax OR ebx
    not ebx                ; flip all bits in ebx
    shl eax, 2             ; eax = eax << 2 
    shr ebx, 1             ; ebx = ebx >> 1 
```


## 4. String Instructions

| Mnemonic    | Description                                               |
|--------------|----------------------------------------------------------------|
| **`MOVS`**   | Copy data from source to destination (`MOVSB` = byte, `MOVSD` = dword) |
| **`CMPS`**   | Compare source with destination (`CMPSB`= byte, `CMPSD` = dword)      |
| **`LODS`**   | Load source to `EAX` (`LODSB` = byte, `LODSD` = dword)                |
| **`STOS`**   | Store EAX at destination (`STOSB` = byte, `STOSD` = dword)           |

Example:
```asm
section .data
    src: dd 0x12345678
    dest: dd 0

section .text
    lea esi, [src]           ; Source pointer
    lea edi, [dest]          ; Destination pointer
    movsd                    ; Move dword from [ESI] to [EDI]
    cmpsd                    ; Compare dword at [ESI] and [EDI]
    lodsd                    ; Load dword at [ESI] into EAX
    stosd                    ; Store EAX at [EDI]
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
    mov eax, 5
    mov ebx, 10
    cmp eax, ebx
    ja  greater_label    ; Jump if unsigned above (CF=0 and ZF=0)
    jb  less_label       ; Jump if unsigned below (CF=1)
    je  equal_label      ; Jump if equal (ZF=1)
greater_label:
    ; code for eax > ebx
    jmp done
less_label:
    ; code for eax < ebx
    jmp done
equal_label:
    ; code for eax == ebx
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
    mov eax, -5
    mov ebx, 10
    cmp eax, ebx
    jg  signed_greater    ; Jump if eax > ebx (signed)
    jl  signed_less       ; Jump if eax < ebx (signed)
    je  signed_equal      ; Jump if eax == ebx
signed_greater:
    ; code for eax > ebx (signed)
    jmp signed_done
signed_less:
    ; code for eax < ebx (signed)
    jmp signed_done
signed_equal:
    ; code for eax == ebx
signed_done:
```


## 7. Loop Instructions

| Mnemonic           | Description                                  |
|--------------------|----------------------------------------------|
| **`LOOP`**           | **Decrement ECX**, jump if `ECX ≠ 0`             |
| **`LOOPE`** / **`LOOPZ`**  | Decrement `ECX`, jump if `ECX ≠ 0` and `ZF = 1`  |
| **`LOOPNE`** / **`LOOPNZ`**| Decrement `ECX`, jump if `ECX ≠ 0` and `ZF = 0`  |

Example:
```asm
section .text
    mov     ecx, 5
loop_start:
    ; Loop body code here 
    dec     eax
    loop    loop_start     ; Decrement ECX, jump if not zero
    ; ECX == 0 here
```
