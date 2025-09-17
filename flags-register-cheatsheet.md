# Flags Register Cheatsheet

### What are Flags?
- **Flags** are **special bits** in the **FLAGS register** that indicate the **status of the processor** or the **result of operations**.
- They are used for **conditional jumps**, **arithmetic**, and **logic** operations.

## FLAGS Register Layout
<img width="3368" height="2382" alt="FLAGS register" src="https://github.com/user-attachments/assets/40954fc4-29ad-43d7-8857-2b27a94238f5" />

> [!IMPORTANT]
> In **64-bit mode**, the **FLAGS register** is extended to `RFLAGS`, which includes additional reserved bits for future processor extensions. However, the functionality of the main flags remains the same.


## Main Flags

| Flag  | Name                | Bit | Description                                                    |
|-------|---------------------|-----|----------------------------------------------------------------|
| **CF**| Carry Flag       | 0       | Set if the **arithmetic operation** generates a **carry/borrow** out. |
| **PF**| Parity Flag      | 2       | Set if the number of **1 bits** in the result is **even**.      |
| **AF**| Auxiliary Carry  | 4       | Used in **BCD (binary-coded decimal)** operations.             |
| **ZF**| Zero Flag        | 6       | Set if the result is **zero**.                                 |
| **SF**| Sign Flag        | 7       | Set if the result is **negative** (**MSB set**).               |
| **TF**| Trap Flag       | 8       | Used for **single-step debugging**.                            |
| **IF**| Interrupt Flag | 9       | If set, **interrupts are enabled**.                            |
| **DF**| Direction Flag   | 10      | Determines **string operation direction** (`0` = **increment**, `1` = **decrement**). |
| **OF**| Overflow Flag   | 11      | Set if an **arithmetic operation** overflows a **signed number**. |

> [!NOTE]
>  Bits **1**, **3**, **5**, and **12-15** are either **reserved** or **unused**.

## Common Instructions Affecting Flag

| Instruction | CF | PF | AF | ZF | SF | OF | Description                                  |
|-------------|----|----|----|----|----|----|----------------------------------------------|
| `ADD`       | ✓  | ✓  | ✓  | ✓  | ✓  | ✓  | Adds two values                              |
| `SUB`       | ✓  | ✓  | ✓  | ✓  | ✓  | ✓  | Subtracts one value from another             |
| `INC`       |    | ✓  | ✓  | ✓  | ✓  | ✓  | Increments a value                           |
| `DEC`       |    | ✓  | ✓  | ✓  | ✓  | ✓  | Decrements a value                           |
| `MUL`       | ✓  |    |    |    |    | ✓  | Unsigned multiplication (**sets CF/OF** if result too large) |
| `DIV`       |    |    |    |    |    |    | Unsigned division (raises **exception on overflow**)         |
| `AND`       |    | ✓  |    | ✓  | ✓  |    | Clear **CF** and **OF**                              |
| `OR`        |    | ✓  |    | ✓  | ✓  |    | Clear **CF** and **OF**                              |
| `XOR`       |    | ✓  |    | ✓  | ✓  |    | Clear **CF** and **OF**                              |
| `CMP`       | ✓  | ✓  | ✓  | ✓  | ✓  | ✓  | Compares two values                          |
| `TEST`      |    | ✓  |    | ✓  | ✓  |    | Logical AND                                  |


## How to Use the Flags

### 1. Conditional Jumps Based on Flags

| Instruction| Description                           |
|------------------|--------------------------------------------|
| `JE`/`JZ`        | Jump if **Zero Flag** is set (**ZF = 1**)  |
| `JNE`/`JNZ`      | Jump if **Zero Flag** is clear (**ZF = 0**)|
| `JC`             | Jump if **Carry Flag** is set (**CF = 1**) |
| `JNC`            | Jump if **Carry Flag** is clear (**CF = 0**)|
| `JS`             | Jump if **Sign Flag** is set (**SF = 1**)  |
| `JNS`            | Jump if **Sign Flag** is clear (**SF = 0**)|
| `JO`             | Jump if **Overflow Flag** is set (**OF = 1**)|
| `JNO`            | Jump if **Overflow Flag** is clear (**OF = 0**)|
| `JP`/`JPE`       | Jump if **Parity Flag** is set (**PF = 1**)|
| `JNP`/`JPO`      | Jump if **Parity Flag** is clear (**PF = 0**)|



### 2. Flag Manipulation Instructions

| Instruction | Description                     |
|-------------|---------------------------------|
|`STC`        | Set Carry flag **(CF = 1)**         |
|`CLC`        | Clear Carry flag **(CF = 0)**       |
|`CMC`        | Complement Carry flag **(CF = ~CF)**|
|`STD`        | Set Direction flag **(DF = 1)**     |
|`CLD`        | Clear Direction flag **(DF = 0)**   |
|`STI`        | Set Interrupt flag **(IF = 1)**     |
|`CLI`        | Clear Interrupt flag **(IF = 0)**   |



### 3. Stack Operations
| Instruction |Description                        |
|------------------|------------------------------|
|`PUSHF`| Pushes the FLAGS register onto the stack|
|`POPF` | Pops the FLAGS register from the stack  |





