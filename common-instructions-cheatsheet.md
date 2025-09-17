
# Common Instructions in 8086 Assembl CheatSheet

## 1. Transfer Instructions
| Mnemonic | Example          | Description                              |
|----------|------------------|------------------------------------------|
| `MOV`    | `MOV AX, BX`     | Copy data between registers/memory       |
| `PUSH`   | `PUSH AX`        | Push register/memory onto the stack      |
| `POP`    | `POP BX`         | Pop value from stack into register       |
| `XCHG`   | `XCHG AX, BX`    | Swap values between operands             |
| `LEA`    | `LEA BX, [SI]`   | Load effective address                   |


## 2. Arithmetic Instructions
| Mnemonic | Action                       | Example          | Description                              |
|----------|------------------------------|------------------|------------------------------------------|
| `ADD`    | Addition                     | `ADD AX, 1`      | Add source to destination                |
| `ADC`    | Addition with Carry          | `ADC AL, BL`     | Add source + carry flag to destination   |
| `SUB`    | Subtraction                  | `SUB BX, CX`     | Subtract source from destination         |
| `SBB`    | Subtract with Borrow         | `SBB AX, 1`      | Subtract source + carry flag             |
| `INC`    | Increment                    | `INC CX`         | Add 1 to operand                         |
| `DEC`    | Decrement                    | `DEC DX`         | Subtract 1 from operand                  |
| `NEG`    | Negation                     | `NEG AL`         | Two's complement (negate)                |
| `CMP`    | Compare                      | `CMP AX, BX`     | Subtract source from destination, set flags only |
| `MUL`    | Unsigned Multiply            | `MUL CL`         | Multiply accumulator by source           |
| `IMUL`   | Signed Multiply              | `IMUL CX`        | Signed multiplication                    |
| `DIV`    | Unsigned Divide              | `DIV BL`         | Divide accumulator by source             |
| `IDIV`   | Signed Divide                | `IDIV CX`        | Signed division                          |


## 3. Logic Instructions
| Mnemonic | Example          | Description                              |
|----------|------------------|------------------------------------------|
| `AND`    | `AND AL, 0Fh`    | Bitwise AND operation                    |
| `OR`     | `OR AX, BX`      | Bitwise OR operation                     |
| `XOR`    | `XOR AH, AL`     | Bitwise XOR operation                    |
| `NOT`    | `NOT BL`         | flip all bits of operand                 |
| `TEST`   | `TEST AX, 1`     | AND operation, update flags only         |
| `SHL`    | `SHL AL, 1`      | Shift bits left, insert 0 on right       |
| `SHR`    | `SHR AX, 1`      | Shift bits right, insert 0 on left       |

## 4. STRING Instructions

| Mnemonic    | Action                            | Description                                               |
|-------------|-----------------------------------|-----------------------------------------------------------|
| `MOVS`      | Move String                       | Copy data from source to destination (`MOVSB` = byte, `MOVSW` = word) |
| `CMPS`      | Compare String                    | Compare source with destination (`CMPSB`= byte, `CMPSW` = word)              |
| `LODS`      | Load String                       | Load source to AL/AX (`LODSB` = byte, `LODSW` = word)                   |
| `STOS`      | Store String                      | Store AL/AX at destination (`STOSB` = byte, `STOSW` = word)                  


## 5. JUMPS (UNSIGNED)

| Mnemonic     | Action                  | Condition             | Description                       |
|--------------|------------------------|------------------------|-----------------------------------|
| `JMP`        | Unconditional Jump     | —                      | Jump to label or address          |
| `JE` / `JZ`  | Jump if Equal/Zero     | ZF = 1                 | Jump if result is zero            |
| `JNE` / `JNZ`| Jump if Not Equal/Zero | ZF = 0                 | Jump if result is not zero        |
| `JA` / `JNBE`| Jump if Above          | CF=0 and ZF=0          | For unsigned, greater than        |
| `JAE`/ `JNB` | Jump if Above/Equal    | CF=0                   | Unsigned, greater or equal        |
| `JB` / `JNAE`| Jump if Below          | CF=1                   | Unsigned, less than               |
| `JBE`/ `JNA` | Jump if Below/Equal    | CF=1 or ZF=1           | Unsigned, less or equal           |
| `JC`         | Jump if Carry          | CF=1                   | Carry flag set                    |
| `JNC`        | Jump if Not Carry      | CF=0                   | Carry flag clear                  |
| `JPE`        | Jump if Parity Even    | PF=1                   | Parity flag even                  |
| `JPO`        | Jump if Parity Odd     | PF=0                   | Parity flag odd                   |


## 6. JUMPS (SIGNED)
| Mnemonic      | Action                 | Condition              | Description                           |
|---------------|-----------------------|------------------------|---------------------------------------|
| `JG` / `JNLE` | Jump if Greater       | ZF=0 and SF=OF         | Signed, greater than                  |
| `JGE`/ `JNL`  | Jump if Greater/Equal | SF=OF                  | Signed, greater or equal              |
| `JL` / `JNGE` | Jump if Less          | SF≠OF                  | Signed, less than                     |
| `JLE`/ `JNG`  | Jump if Less/Equal    | ZF=1 or SF≠OF          | Signed, less or equal                 |
| `JS`          | Jump if Sign          | SF=1                   | Sign flag set (negative)              |
| `JNS`         | Jump if Not Sign      | SF=0                   | Sign flag clear (positive)            |
| `JO`          | Jump if Overflow      | OF=1                   | Overflow flag set                     |
| `JNO`         | Jump if Not Overflow  | OF=0                   | Overflow flag clear                   |


## 7. LOOP Instructions

| Mnemonic        | Action                    | Description                                  |
|-----------------|--------------------------|----------------------------------------------|
| `LOOP`          | Loop with Counter         | Decrement CX, jump if CX ≠ 0                 |
| `LOOPE` / `LOOPZ`  | Loop While Equal/Zero    | Decrement CX, jump if CX ≠ 0 and ZF = 1      |
| `LOOPNE` / `LOOPNZ`| Loop While Not Equal/Zero| Decrement CX, jump if CX ≠ 0 and ZF = 0      |

