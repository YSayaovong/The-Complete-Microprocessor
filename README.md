Lab 4: The Complete Microprocessor

Prerequisites : Before beginning this lab, you must:
• Understand how to use the tool flow (See the installation guide and Lab 0)
• Have completed Lab 1: Half Adder, Full Adder, 4-bit Incrementer and Adder.
• Have completed Lab 2: Multiplexers, Decoders, and the Arithmetic Logic Unit.
• Have completed Lab 3: Registers, Counters, and the “Brainless CPU”.

Equipment : Personal computer with the required software installed.
Files to copy from Lab 3 (do NOT copy from Lab 1 or Lab 2!):

alu.dig

and_add.dig

brainless.dig

four_bit_adder.dig

four_bit_mux.dig

four_bit_reg.dig

full_adder.dig

half_adder.dig

incrementer.dig

not_neg.dig

program_ctr.dig

program_ram.dig

two_bit_mux.dig
Files to download:

rom_vals.hex

ram_vals.hex

micro_top.v

micro_stim.v

Objectives : When you have completed this lab, you will be able to:

• Build a Memory Address Generator for a microprocessor.

• Design a ROM-based controller for a microprocessor.

• Create an instruction set for a microprocessor.

• Use the instruction set to write a program and enter it into a RAM.

• Execute programs in Digital and in Verilog.

Introduction
In this lab we will complete the microprocessor design by building a memory address generator
and a controller and adding them to your brainless microprocessor. We’ll also define an
instruction set for the controller. Finally, you will use the language inherent in your instruction
set to create a simple program, enter the program in your microprocessor’s memory and
execute the program. You will test the program first in Digital and then in Verilog.

Warning: Use the signal and circuit names provided! Verilog does not allow names to start
with a number or names that have dashes!

Create a folder named Lab4. Into that folder, copy the files listed above from Lab 3. Be sure to
only copy the required files. While it is tempting to do Lab 4 in the same directory where you
did a prior lab, it is advisable to start in a fresh directory in case something goes wrong. That
way, you still have the pristine prior lab results to copy again. In addition, this means that the
Lab4 folder will only have the files necessary for Lab 4.

Once you’ve copied the files from Lab 3, download the files provided for Lab 4 and place them
in the Lab4 folder. Now, you’re ready to start!

NOTE: You are required to design the circuits as presented in this document. Even though
Digital supplies many of the functions we will design, you are not to use them.

Task 4-1: Build and Test the Memory-Address-Generation Circuit

Now that your brainless microprocessor is working, we will add additional pieces of circuitry to
it and assemble the complete microprocessor. The first step is to modify the 4-bit incrementer
you built in Task 3-2 so that you can use it to generate the memory addresses for your CPU. The
memory address generation circuit is shown in Figure 1. The memory address generation circuit
is comprised of two independent pieces. One piece consists of a register and increment circuit,
which is your 4-bit incrementer, and is known as the Program Counter (PC). The other piece,
which accepts addresses from the data bus, is known as the Memory Address Register (MAR).
This register can be loaded from the data bus and holds the address of a storage location that
we want to access. This address does not have to be in sequence with the other addresses.
Thus, the MAR allows us to access a specific address and that address is usually obtained from
our RAM. In order to load the memory address from the data_bus to the MAR, we have an
enable signal that is called load_mar. The output of the address generation circuit is generated
by a mux, which controls whether the PC or MAR drives the address bus, addr_bus. The control
input to the mux, use_pc (short for Use Program Counter), is high when the PC values are
driving the address bus and low when the MAR contents are to be supplied to the address bus.

The memory address generation circuit will allow our processor to access memory locations
both in and out of sequential order. The circuit can:
• Automatically increment memory addresses after each instruction or operand is
retrieved by the CPU.

• Change the memory reference address so that we can store data to arbitrary memory
locations or read data from arbitrary memory locations.
