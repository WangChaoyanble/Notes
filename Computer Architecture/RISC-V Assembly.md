# RISC-V Assembly
Below is a C program: declare a variable `a`
```c
void _start()
{
    int a=10;
}
```
Use riscv-gnu-toolchain compile it into assembly:`riscv32-unknown-elf-gcc -S testbench.c -o testbench.S`

Then we get the assembly below:

```as
	.file	"testbench.c"
	.option nopic
	.attribute arch, "rv32i2p1"
	.attribute unaligned_access, 0
	.attribute stack_align, 16
	.text
	.align	2
	.globl	_start
	.type	_start, @function
_start:
	addi	sp,sp,-32
	sw	s0,28(sp)
	addi	s0,sp,32
	li	a5,10
	sw	a5,-20(s0)
	nop
	lw	s0,28(sp)
	addi	sp,sp,32
	jr	ra
	.size	_start, .-_start
	.ident	"GCC: () 13.2.0"

```
- First allocate 32 byte for stack
- Save the value of s0(frame pointer) on stack
- Save the original stack top to s0
- Declare variable a
- Restore the original value of s0 from the stack
- Restore the stack pointer sp to its original position
- Jump to the address saved in the return address register (ra)

Change the source file to:

```c
void test()
{
    int a=10;
}
void _start()
{
    int a=10;
    test();
}
```
Then the assembly becomes like:
```as
	.file	"testbench.c"
	.option nopic
	.attribute arch, "rv32i2p1"
	.attribute unaligned_access, 0
	.attribute stack_align, 16
	.text
	.align	2
	.globl	test
	.type	test, @function
test:
	addi	sp,sp,-32
	sw	s0,28(sp)
	addi	s0,sp,32
	li	a5,10
	sw	a5,-20(s0)
	nop
	lw	s0,28(sp)
	addi	sp,sp,32
	jr	ra
	.size	test, .-test
	.align	2
	.globl	_start
	.type	_start, @function
_start:
	addi	sp,sp,-32
	sw	ra,28(sp)
	sw	s0,24(sp)
	addi	s0,sp,32
	li	a5,10
	sw	a5,-20(s0)
	call	test
	nop
	lw	ra,28(sp)
	lw	s0,24(sp)
	addi	sp,sp,32
	jr	ra
	.size	_start, .-_start
	.ident	"GCC: () 13.2.0"

```


Extracted from [RISC-V Manual](https://github.com/riscv-non-isa/riscv-asm-manual/blob/main/riscv-asm.md):

RISC-V registers:

| Register | ABI Name | Description | Saved by Calle- |
| :--: | :--: | :--: | :--: |
 | x0 | zero | hardwired zero | - |
| x1 | ra | return address | -R |
 | x2 | sp | stack pointer | -E |
 | x3 | gp | global pointer | - |
| x4 | tp | thread pointer | - |
 | x5~x7 | t0~t3 | temporary register 0~2 | -R |
| x8 | s0 / fp | saved register 0 / frame pointer | -E |
| x9 | s1 | saved register 1 | -E |
| x10 | a0 | function argument 0 / return value 0 | -R |
| x11 | a1 | function argument 1 / return value 1 | -R |
 | x12~x17 | a2~a7 | function argument 2~7 | -R |
| x18~x27 | s2~s11 | saved register 2~11 | -E |
| x28~x31 | t3~t6 | temporary register 3~6 | -R |


The following table lists assembler directives:

Directive    | Arguments                      | Description
:----------- | :-------------                 | :---------------
.align       | integer                        | align to power of 2 (alias for .p2align)
.file        | "filename"                     | emit filename FILE LOCAL symbol table
.globl       | symbol_name                    | emit symbol_name to symbol table (scope GLOBAL)
.local       | symbol_name                    | emit symbol_name to symbol table (scope LOCAL)
.comm        | symbol_name,size,align         | emit common object to .bss section
.common      | symbol_name,size,align         | emit common object to .bss section
.ident       | "string"                       | accepted for source compatibility
.section     | [{.text,.data,.rodata,.bss}]   | emit section (if not present, default .text) and make current
.size        | symbol, symbol                 | accepted for source compatibility
.text        |                                | emit .text section (if not present) and make current
.data        |                                | emit .data section (if not present) and make current
.rodata      |                                | emit .rodata section (if not present) and make current
.bss         |                                | emit .bss section (if not present) and make current
.string      | "string"                       | emit string
.asciz       | "string"                       | emit string (alias for .string)
.equ         | name, value                    | constant definition
.macro       | name arg1 [, argn]             | begin macro definition \argname to substitute
.endm        |                                | end macro definition
.type        | symbol, @function              | accepted for source compatibility
.option      | {arch,rvc,norvc,pic,nopic,relax,norelax,push,pop} | RISC-V options. Refer to [.option](#.option) for a more detailed description.
.byte        | expression [, expression]*     | 8-bit comma separated words
.2byte       | expression [, expression]*     | 16-bit comma separated words
.half        | expression [, expression]*     | 16-bit comma separated words
.short       | expression [, expression]*     | 16-bit comma separated words
.4byte       | expression [, expression]*     | 32-bit comma separated words
.word        | expression [, expression]*     | 32-bit comma separated words
.long        | expression [, expression]*     | 32-bit comma separated words
.8byte       | expression [, expression]*     | 64-bit comma separated words
.dword       | expression [, expression]*     | 64-bit comma separated words
.quad        | expression [, expression]*     | 64-bit comma separated words
.float       | expression [, expression]*     | 32-bit floating point values, see [Floating-point literals](#fp-literal) for the value format.
.double      | expression [, expression]*     | 64-bit floating point values, see [Floating-point literals](#fp-literal) for the value format.
.quad        | expression [, expression]*     | 128-bit floating point values, see [Floating-point literals](#fp-literal) for the value format.
.dtprelword  | expression [, expression]*     | 32-bit thread local word
.dtpreldword | expression [, expression]*     | 64-bit thread local word
.sleb128     | expression                     | signed little endian base 128, DWARF
.uleb128     | expression                     | unsigned little endian base 128, DWARF
.p2align     | p2,[pad_val=0],max             | align to power of 2
.balign      | b,[pad_val=0]                  | byte align
.zero        | integer                        | zero bytes
.variant_cc  | symbol_name                    | annotate the symbol with variant calling convention
.attribute   | name, value                    | RISC-V

