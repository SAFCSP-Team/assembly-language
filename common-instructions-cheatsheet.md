
# Common Instructions in 8086 Assembly CheatSheet

## 1. Transfer Instructions
| Mnemonic | Example          | Description                              |
|--------------|----------------------------|----------------------------------------|
| **`MOV`**    | `MOV RAX, RBX`             | Copy data between registers/memory |
| **`PUSH`**   | `PUSH RAX`                 | Push value onto the stack|
| **`POP`**    | `POP RBX`                  | Pop value from stack into register |
| **`XCHG`**   | `XCHG RAX, RBX`            | Swap values** between operands       |
| **`LEA`**    | `LEA RBX, [RDI]`           | Load effective address             |


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


## 4. String Instructions

| Mnemonic    | Description                                               |
|--------------|----------------------------------------------------------------|
| **`MOVS`**   | Copy data from source to destination (`MOVSB` = byte, `MOVSQ` = quadword) |
| **`CMPS`**   | Compare source with destination (`CMPSB`= byte, `CMPSQ` = quadword)      |
| **`LODS`**   | Load source to `RAX` (`LODSB` = byte, `LODSQ` = quadword)                |
| **`STOS`**   | Store RAX at destination (`STOSB` = byte, `STOSQ` = quadword)           |

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

## 7. Loop Instructions

| Mnemonic           | Description                                  |
|--------------------|----------------------------------------------|
| **`LOOP`**           | **Decrement RCX**, jump if `RCX ≠ 0`             |
| **`LOOPE`** / **`LOOPZ`**  | Decrement `RCX`, jump if `RCX ≠ 0` and `ZF = 1`  |
| **`LOOPNE`** / **`LOOPNZ`**| Decrement `RCX`, jump if `RCX ≠ 0` and `ZF = 0`  |

