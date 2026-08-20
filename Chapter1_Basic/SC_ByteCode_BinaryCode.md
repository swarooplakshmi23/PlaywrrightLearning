# Source Code vs Byte Code vs Binary Code

This document explains the differences between **Source Code**, **Byte Code**, and **Binary Code** using the example file `HelloWorld.js`:

```javascript
console.log("Hello, World!");
```

---

## 1. Definitions

### Source Code
The code written by a **human programmer** in a high-level programming language (JavaScript, Python, Java, C, etc.). It is human-readable and must be translated before the computer can execute it.

### Byte Code
An **intermediate representation** between source code and machine code. It is produced by a compiler (e.g., the V8 engine compiles JavaScript to bytecode) and is executed by a **virtual machine** (VM). It is not tied to a specific CPU architecture, which makes it **portable**.

### Binary Code (Machine Code)
The **lowest-level** code consisting of `0`s and `1`s that the **CPU executes directly**. It is hardware-specific — each CPU architecture (x86, ARM, etc.) has its own machine code. Also called *machine code* or *native code*.

---

## 2. Comparison Table

| Feature            | Source Code                          | Byte Code                          | Binary Code (Machine Code)              |
|--------------------|--------------------------------------|------------------------------------|------------------------------------------|
| **Who writes it**  | Humans                               | Compiler (generated)               | Compiler / JIT (generated)               |
| **Readability**    | Human-readable                       | Partially readable                 | Not human-readable (0s and 1s)           |
| **Example**        | `console.log("Hello, World!");`      | `0x26 0x20 0x03 0x00 ...`          | `01001000 01100101 01101100 ...`         |
| **Execution**      | Cannot run directly                  | Runs on a Virtual Machine (VM)     | Runs directly on the CPU                 |
| **Portability**    | Portable (any platform with runtime) | Portable across CPU architectures  | Tied to a specific CPU/OS                |
| **Performance**    | Slowest (interpreted step-by-step)   | Faster than source, slower than native | Fastest                               |
| **Level**          | High-level                           | Intermediate-level                 | Low-level                                |
| **File extension** | `.js`, `.py`, `.java`, `.c`         | `.class` (Java), `.pyc` (Python), V8 bytecode | `.exe`, `.out`, `.bin` (compiled) |

---

## 3. Walkthrough with `HelloWorld.js`

The journey of our example through the three stages:

```
Source Code                 Byte Code                 Binary Code
console.log(...)   ───►    VM bytecode      ───►      0s and 1s
(JavaScript,               (V8 engine                 (CPU native
 human written)            internal format)            instructions)
```

### Step 1 — Source Code
```javascript
console.log("Hello, World!");
```
Written by a developer. The browser's **V8 JavaScript engine** parses this text.

### Step 2 — Byte Code
V8 (like other JIT-compiled engines) first compiles the source into **bytecode** — a compact intermediate format understood by the V8 virtual machine. It looks like cryptic instruction tokens, e.g.:

```
0x26 0x20 0x03 0x00 0x41 0x00 0x10 0x03
```

### Step 3 — Binary Code (Machine Code)
When the function runs frequently ("hot"), the V8 **JIT compiler (TurboFan)** converts the bytecode into **native machine code** — actual binary instructions the CPU can execute:

```
01001000 01100101 01101100 01101100 01101111
```
(or `48 65 6C 6C 6F` in hex — the ASCII bytes for "Hello")

---

## 4. Analogy

| Concept        | Analogy                                        |
|----------------|------------------------------------------------|
| Source Code    | Recipe written in a language only a chef understands |
| Byte Code      | Translated step list in a portable, standard kitchen manual |
| Binary Code    | The physical muscle movements the chef's hands actually make |

---

## 5. Key Takeaways

1. **Source code** = what **humans write**.
2. **Byte code** = what **virtual machines run** (portable, platform-independent).
3. **Binary code** = what **CPUs execute** (fastest, hardware-specific).
4. JavaScript (like Java, Python, C#) goes: **Source → Bytecode → Machine Code**, usually with a **JIT compiler** handling the final step at runtime.
5. A compiled language like C goes directly: **Source → Machine Code** (no bytecode step).
