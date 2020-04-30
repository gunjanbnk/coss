# coss
CPU-Simulator Programs


Simulator Instruction Sub-set Inst Description 
===============================================

Data transfer instructions
--------------------------
MOV
	Move data to register; move register to register
	e.g.
	MOV #2, R01 moves number 2 into register R01
	MOV R01, R03 moves contents of register R01 into register R03
LDB
	Load a byte from memory to register
	e.g.
	LDB 1022, R03 loads a byte from memory address 1022 into R03
	LDB @R02, R05 loads a byte from memory the address of which is in R02
LDW
	Load a word (2 bytes) from memory to register
	Same as in LDB but a word (i.e. 2 bytes) is loaded into a register
STB
	Store a byte from register to memory
	STB R07, 2146 stores a byte from R07 into memory address 2146
	STB R04, @R08 stores a byte from R04 into memory address of which is in R08
STW
	Store a word (2 bytes) from register to memory
	Same as in STB but a word (i.e. 2 bytes) is loaded stored in memory
PSH
	Push data to top of hardware stack (TOS); push register to TOS
	e.g.
	PSH #6 pushes number 6 on top of the stack
	PSH R03 pushes the contents of register R03 on top of the stack
POP
	Pop data from top of hardware stack to register
	e.g.
	POP R05 pops contents of top of stack into register R05
	Note: If you try to POP from an empty stack you will get the error message “Stack underflow”.

Arithmetic instructions
-----------------------
ADD
	Add number to register; add register to register
	e.g.
	ADD #3, R02 adds number 3 to contents of register R02 and stores the result in register R02.
	ADD R00, R01 adds contents of register R00 to contents of register R01 and stores the result in register R01.
SUB
	Subtract number from register; subtract register from register
MUL
	Multiply number with register; multiply register with register
DIV
	Divide number with register; divide register with register 

Control transfer instructions
-----------------------------
JMP
	Jump to instruction address unconditionally
	e.g.
	JMP 100 unconditionally jumps to address location 100 where there is another instruction
	8 | P a g e
JLT
	Jump to instruction address if less than (after last comparison)
JGT
	Jump to instruction address if greater than (after last comparison)
JEQ
	Jump to instruction address if equal (after last comparison instruction)
	e.g.
	JEQ 200 jumps to address location 200 if the previous comparison instruction result indicates that the two numbers are equal, i.e. the Z status flag is set (the Z box will be checked in this case).
JNE
	Jump to instruction address if not equal (after last comparison)
MSF
	Mark Stack Frame instruction is used in conjunction with the CAL instruction.
	e.g.
	MSF reserve a space for the return address on program stack
	CAL 1456 save the return address in the reserved space and jump to subroutine in address location 1456
CAL
	Jump to subroutine address (saves the return address on program stack)
	This instruction is used in conjunction with the MSF instruction. You’ll need an MSF instruction before the CAL instruction. See the example above
RET
	Return from subroutine (uses the return address on stack)
SWI
	Software interrupt (used to request OS help)
HLT
	Halt simulation 

Comparison instruction
----------------------
CMP
	Compare number with register; compare register with register
	e.g.
	CMP #5, R02 compare number 5 with the contents of register R02
	CMP R01, R03 compare the contents of registers R01 and R03
	Note:
	If R01 = R03 then the status flag Z will be set, i.e. the Z box is checked.
	If R01 < R03 then none of the status flags will be set, i.e. none of the status flag boxes are checked.
	If R01 > R03 then the status flag N will be set, i.e. the N status box is checked. 

Input, output instructions
--------------------------
IN
	Get input data (if available) from an external IO device
OUT
	Output data to an external IO device
	e.g.
	OUT 16, 0 outputs contents of data in location 16 to the console (the second parameter must always be a 0)