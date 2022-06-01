
RISC-V
========================

## Table of Context <a name="toc"></a>

 - [RISC-V QEmu](#qemu)
 - [Compiler support](#compilers)
 - [Links](#links)
 - [port to v1.0](#port)

## Qemu <a name="qemu"></a>

 - QEmu support RVV 0.7.1 until 20211220
 - QEmu support RVV 0.10(~v1.0) from 2022021

## Compilers - Vector eXtension support <a name="compilers"></a>

 - https://github.com/riscv/riscv-gnu-toolchain - v0.10(~v1.0)/int
 - gcc - no
 - https://github.com/riscv-collab/riscv-gcc - basic (added 20211123)
 - clang -  v0.10(close to final)
 - xuante - v0.7.1

## Links <a name="links"></a>
 - https://gms.tf/riscv-vector.html
 - [debian-riscv](https://wiki.debian.org/RISC-V#Creating_a_riscv64_chroot)
 - [X11 riscv/qemu](https://zxnord.medium.com/launching-x11-risc-v-applications-on-qemu-debian-efa62b4c4657)
 - [xuantie-gcc-10](https://github.com/T-head-Semi/gcc)
 - [c910v vector samples](https://github.com/c-sky/xuantie-vector-demos)

## Port to v1.0 <a name="port"></a>

| v 0.8.0  | v 1.0    | description   |
|----------|----------|:--------------|
| vlb.v | vle8.v  |  8-bit load (signed) |
| vlh.v | vle16.v | 16-bit load (signed) |
| vlw.v | vle32.v | 32-bit load (signed) |
| vlbu.v | vle8.v  |  8-bit load (unsigned) |
| vlhu.v | vle16.v | 16-bit load (unsigned) |
| vlwu.v | vle32.v | 32-bit load (unsigned) |
| ---  | vle64.v | 64-bit load |

[back to top](#toc)
