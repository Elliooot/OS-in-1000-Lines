# Operating System in 1,000 Lines (RISC-V)

A minimal, bare-metal operating system kernel built from scratch for the 32-bit RISC-V architecture.

This project follows and is based on the tutorial and open-source project **[Operating System in 1,000 Lines](https://operating-system-in-1000-lines.vercel.app/)** by Seiya Nuta.

---

## Features Implemented

- **Bare-metal Bootstrapping**
  - Custom linker script ([`kernel.ld`](kernel.ld)) specifying the memory layout (base address `0x80200000`).
  - Kernel stack initialization (`sp`) with 128 KB allocated space.
  - Manual zeroing of the `.bss` section.
  - Power-efficient idle loop using the `wfi` (Wait For Interrupt) instruction.
- **OpenSBI Firmware Integration**
  - SBI interface wrapper (`sbi_call`) using the RISC-V `ecall` assembly instruction.
  - Character printing via OpenSBI console putchar.
- **Freestanding Runtime & Utilities**
  - Standard fixed-width types and common macros (`bool`, `uint32_t`, `size_t`, `paddr_t`, `vaddr_t`, `align_up`, etc.).
  - Memory and string routines: `memset`, `memcpy`, `strcpy`, and `strcmp`.
  - Formatted `printf` with variadic arguments (`%s`, `%d`, `%x`, `%%`), properly handling `INT_MIN` in two's-complement arithmetic.

---

## Prerequisites

- **Compiler**: `clang` and `lld` with RISC-V target support (e.g. LLVM via Homebrew)
- **Emulator**: `qemu-system-riscv32`

---

## Build & Run

Run the build script to compile the kernel and launch it in QEMU:

```bash
chmod +x run.sh
./run.sh
```

To exit QEMU, press `Ctrl + A` followed by `X`.

---

## Project Structure

```text
.
├── kernel.ld      # Linker script defining memory sections and addresses
├── kernel.h       # Kernel data structures (e.g., struct sbiret)
├── kernel.c       # Boot code, initialization, and kernel_main()
├── common.h       # Common type definitions, macros, and function prototypes
├── common.c       # Minimal standard library functions (memset, memcpy, printf, etc.)
├── run.sh         # Compilation and QEMU startup script
└── README.md      # Project documentation
```

---

## References

This implementation is based on:

- **Book / Tutorial**: [Operating System in 1,000 Lines](https://operating-system-in-1000-lines.vercel.app/) by [Seiya Nuta](https://github.com/nuta)
- **Original Repository**: [nuta/operating-system-in-1000-lines](https://github.com/nuta/operating-system-in-1000-lines)
