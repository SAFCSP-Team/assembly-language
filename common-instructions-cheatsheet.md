
# Common Instructions in 8086 Assembly CheatSheet

## 1. Transfer Instructions
| Mnemonic | Example          | Description                              |
|----------|------------------|------------------------------------------|
| `MOV`    | `MOV AX, BX`     | Copy data between registers/memory       |
| `PUSH`   | `PUSH AX`        | Push register/memory onto the stack      |
| `POP`    | `POP BX`         | Pop value from stack into register       |
| `XCHG`   | `XCHG AX, BX`    | Swap values between operands             |
| `LEA`    | `LEA BX, [SI]`   | Load effective address                   |


## 2. Arithmetic Instructions
| Mnemonic | Example          | Description                              |
|----------|------------------|------------------------------------------|
| `ADD`    | `ADD AX, 1`      | Add source to destination                |
| `ADC`    | `ADC AL, BL`     | Add source + carry flag to destination   |
| `SUB`    | `SUB BX, CX`     | Subtract source from destination         |
| `SBB`    | `SBB AX, 1`      | Subtract source + carry flag             |
| `INC`    | `INC CX`         | Add 1 to operand                         |
| `DEC`    | `DEC DX`         | Subtract 1 from operand                  |
| `NEG`    | `NEG AL`         | Two's complement (negate)                |
| `CMP`    | `CMP AX, BX`     | Subtract source from destination, set flags only |
| `MUL`    | `MUL CL`         | Multiply accumulator by source           |
| `IMUL`   | `IMUL CX`        | Signed multiplication                    |
| `DIV`    | `DIV BL`         | Divide accumulator by source             |
| `IDIV`   | `IDIV CX`        | Signed division                          |


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

| Mnemonic    | Description                                               |
|-------------|-----------------------------------------------------------|
| `MOVS`      | Copy data from source to destination (`MOVSB` = byte, `MOVSW` = word) |
| `CMPS`       | Compare source with destination (`CMPSB`= byte, `CMPSW` = word)              |
| `LODS`      | Load source to AL/AX (`LODSB` = byte, `LODSW` = word)                   |
| `STOS`      | Store AL/AX at destination (`STOSB` = byte, `STOSW` = word)                  


## 5. JUMPS (UNSIGNED)

| Mnemonic     | Condition           | Description                       |
|--------------|---------------------|-----------------------------------|
| `JMP`        | —                   | Jump to label or address          |
| `JE` / `JZ`  | ZF = 1              | Jump if result is zero            |
| `JNE` / `JNZ`| ZF = 0              | Jump if result is not zero        |
| `JA` / `JNBE`| CF=0 and ZF=0       | For unsigned, greater than        |
| `JAE`/ `JNB` | CF=0                | Unsigned, greater or equal        |
| `JB` / `JNAE`| CF=1                | Unsigned, less than               |
| `JBE`/ `JNA` | CF=1 or ZF=1        | Unsigned, less or equal           |
| `JC`         | CF=1                | Carry flag set                    |
| `JNC`        | CF=0                | Carry flag clear                  |
| `JPE`        | PF=1                | Parity flag even                  |
| `JPO`        | PF=0                | Parity flag odd                   |


## 6. JUMPS (SIGNED)
| Mnemonic      | Condition              | Description                           |
|---------------|------------------------|---------------------------------------|
| `JG` / `JNLE` | ZF=0 and SF=OF         |Signed, greater than                  |
| `JGE`/ `JNL`  | SF=OF                  |Signed, greater or equal              |
| `JL` / `JNGE` | SF≠OF                  |Signed, less than                     |
| `JLE`/ `JNG`  | ZF=1 or SF≠OF          |Signed, less or equal                 |
| `JS`          | SF=1                   |Sign flag set (negative)              |
| `JNS`         | SF=0                   |Sign flag clear (positive)            |
| `JO`          | OF=1                   |Overflow flag set                     |
| `JNO`         | OF=0                   |Overflow flag clear                   |


## 7. LOOP Instructions

| Mnemonic           | Description                                  |
|--------------------|----------------------------------------------|
| `LOOP`             | Decrement CX, jump if CX ≠ 0                 |
| `LOOPE` / `LOOPZ`  | Decrement CX, jump if CX ≠ 0 and ZF = 1      |
| `LOOPNE` / `LOOPNZ`| Decrement CX, jump if CX ≠ 0 and ZF = 0      |

