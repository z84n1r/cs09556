java c
CEG 2136 Lab 3 
LAB 3 Arithmetic Logic Unit 
1.   Purpose: In this lab students will design, simulate, build and test an Arithmetic Logic Unit (ALU),  employing Quartus II as a development environment and the Altera DE2-115 board as  experimental platform. ALU has to execute 16 different operations on two operands of 4  bits and will provide a 4-bit result along with 4 status bits (oVerflow, Zero, Negative,  Carry). The input operands will be generated by slide switches (or by “input_generator” component if you are testing your design remotely), while the result and the status bits will  be displayed on LEDs.
2.   Requirements of the Lab: 
The following will be submitted in your report.
* Functional and truth tables, equations and schematics of your design
* Log of what you did
* Screen shots of all schematics and waveform. diagrams
* Compilation, simulation and downloading messages (if any)
* Test results
3.   Equipment and Supplies: 
* Quartus II (student edition or web edition)
* Altera DE2-115 board with USB-Blaster cable and Power supply 12 VDC, 2A
4.   References: 
4.1. Chapter1 - 4 of the Textbook: Computer System Architecture, Morris Mano, 3rd Ed.
4.2.  Course notes and
4.3. DE2-115 User Manual posted  in  the Documentation section  under  the Laboratories tab of CEG2136 Virtual Campus.
5. PreLab - Design of the ALU 
5.1. ALU structure 
The Central Processing Unit (CPU) consists of a Control Unit (CU) and a Datapath (execution unit – EU) as shown in the block diagram of Figure 1.
The CPU’s datapath contains registers to store data (A, B, C) and control (S) / status (V,Z,N,Cy) information, along an Arithmetic and Logic Unit (ALU). You have to design CPU’s datapath that can perform. arithmetic, shift and logic operations. Your datapath module will handle two types of signals:
Data (inputs: A3-A0 and B3-B0, and outputs C3-C0) – marked in yellow
Control (operations codes) / status: S3-S0 / (V, Z, N, Cy) – marked in light blue in Fig. 1Figure 2(a) presents the ALU datapath. For testing purposes, since CU (the light-blue block in Figure 2) is not designed and built in this lab, CU is replaced and emulated by 4 DIP switches for generating the ALU control inputs (S3 - S0) and 4 LEDs to display the ALU’s state indicators (V,Z,S,O). Operands A and B are generated manually by 8 DIP switches, while the result C is displayed by other 4 LEDs.
Note: This term we will not use DIP switches to generate the test inputs (A, B) and control signals (S) for experimental verification of your ALU. Instead, we are going to use a pre-designed component named “input_ generator” which generates sequences of test vectors A, B, S. Figure 2(b) shows the block diagram of the datapath that we will use for this purpose. ALU is a combinational circuit which can execute any of the 16 micro-operations of Table 1. The operation to be performed is set by the control word (operation code) S3-S0 as explained below:
the control signal S3 selects either the Arithmetic Circuit (AC) or the Logic and Shifting Circuit (LSC) to perform. the operation and send the result to the output C;
the control signals S2, S1, and S0 define the operations to be performed by each circuit (AC or LSC).Both inputs and outputs are stored in buffer registers (D flip-flops synchronized with the same clock), A, B, and C, as shown in Figure 2. To operate at the highest speed, the ALU datapath should be provided with both operands (Aand B) and control bits (S3-S0) at every consecutive clock. To insure a correct operation of the datapath, the total delay introduced by the ALU’s circuits should be smaller than the clock’s period and, as such, the datapath can execute a micro-operation at every clock. The results (C3-C0) and V, Z, S, Cy are provided on the next pulse following the change of A, B and S.

5.2. Hierarchical design Since both the input and the output signals of ALU have 4 bits, the most effective way to implement ALU is to devise it in a hierarchical manner. Files on the lowest level are 1-bit full adder and 1-bit logic and shift circuit (LSC). The intermediate files will consist of a 4- bit register, a 4-bit ari代 写CEG 2136 LAB 3 Arithmetic Logic Unit
代做程序编程语言thmetic circuit (AC), a 4-bit logic and shift circuit (LSC), and a state circuit. Finally, the file at the highest level will cover the complete circuit, loadable to the Altera DE2-115 board. The relation between these files is shown in figure 3. The parts in yellow will be explained further in this document. For the preparation of this lab, you are required to design and test the circuits coloured in green,i.e., the 1-bit LSC, the 4-bit LSC, the 4-bit AC, and the state circuit.
5.3. Design of Logic and Shift Circuit (LSC) 
LSC operates at the bit level, which means that, e.g. C = A AND B is interpreted as {C3, C2, C1, C0} = {A3 AND B3, A2 AND B2, A1 AND B1, A0 AND B0}.Design a circuit which implements all logic and shift functions as shown in the bottom half of Table 1 (with S3=1). LSC is built from four 1-bit Logic and Shift Circuit (LSC).   Such a 1-bit module has 3 control inputs (S2, S1, and S0), two logic inputs (Ai and Bi), two additional inputs for left and right shifts (Ai-1 and Ai+1), and an output (CL i) whose truth table is detailed below. A starting point for the logic diagram of 1-bit LSC is suggested below;5.3.1. Add all the logic gates that are required to complete the LSCi logic diagram of Fig. 4. 
5.3.2.   Use the 1-bit LSC module that you designed above to build a 4-bit logic and shift circuit LSC. Your final design should have 3 control inputs (S2 - S0), 8 data inputs (A3 - A0 and B3 - B0), and 4 data outputs (CL3 - CL0). Your design will be captured in the logiccircuit4bit file. 
5.4. Design of Arithmetic Circuit (AC) 
5.4.1.   The block diagram of the Arithmetic Circuit (AC) is shown in Fig. 5. AC consists of a 4-bit full adder (∑) which calculates the output CA as a function of operands op1 and op0, and of the micro-operation select bits S2, S1 and S0, as described in Table 1.
Complete the following truth table with the corresponding values derived from Table 1. 

5.4.2.  Note that the data inputs A3 - A0 and B3 - B0 should not be connected directly to the inputs of multiplexers for op1 and op2, since you might need some minimal logic to insure full compliance with the truth table. A trivial solution is to implement op1 and op0 with 8-to-1 multiplexers. Start your design by analyzing what inputs are to be brought to op1 and op0 for each combination of S2 and S1, only.
Derive a cost effective solution from this analysis using a 4-to-1 multiplexer. 
5.4.3. Derive the equation of Cy_in in terms of the select bits S2, S1 and S0.
5.4.4. Complete the block diagram of ACi of Fig. 6 with logic components that implement the conclusions you drew above (5.4.1 - 5.4.2):
●  replace the multiplexor symbols with the ones resulted at 5.4.2;
●  add more wires and other logic components between module’s inputs (Ai, Bi , S2, S1 and S0) and multiplexers’ inputs to implement the AC table;
●  implement Cy equation.
This ACi schematic will be later captured in the fulladder1bit.bdf file in Quartus II. Note: ∑i is based on the full adder shown in Figure 9.
The ALU Data Output is provided by AC or LSC as dictated by the control signal S3. The block diagram of Fig. 7 employs 2-to-1 multiplexers to select AC or LSC to be loaded into register C.Your final circuit of the ALU data flow should have 3 control inputs (S2 - S0), 8 data inputs (A3 - A0 and B3 - B0), 4 data outputs (C3 - C0) and the most significant carry bits,which will be used for the status circuit.
5.5. ALU status register 
The ALU results are characterized by four status bits (C, S, Z, and V), which are defined as follows:
Bit Cy (carry) is set to 1 only when the operation is an arithmetic operation and its carry output is 1. It is cleared to 0 if the carry is 0.
Bit S (sign) is set to 1 if the most significant bit of the result C3 is one.
Bit Z (zero) is set to 1 only if the output of the ALU contains all 0’s. It is set to 0 otherwise.
Bit V  (overflow)  is  set  to  1  only  when  an  overflow  occurs  when  performing operations on signed numbers in 2’s complement representation.
Derive the logic equations of the status bits and implement them with conventional gates. 

         
加QQ：99515681  WX：codinghelp
