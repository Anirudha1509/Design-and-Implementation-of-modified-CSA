# Design and Implementation of Modified Carry-Select Adder and its Performance Analysis

Aim: to design a high speed, low power VLSI architecture-based adder circuit.

Problem Statement: The design of high-performance VLSI architectures demands efficient arithmetic units, particularly adders, which are critical for speed, power consumption, and area optimization. Conventional adder circuits, such as ripple carry adders and carry save adders, suffer from significant carry propagation delays, limiting their speed in high-performance applications like RISC processors, where single-cycle instruction execution is crucial. Additionally, power efficiency and area constraints further challenge the implementation of fast adders. Thus, there is a need to explore high-speed, low-power, and area-efficient adder architectures that minimize carry propagation delays while meeting the stringent requirements of modern processors and digital signal processing systems.

Methodology: This project involves design of four different variants of a CSA, namely-
•	Traditional CSA <br><br>
•	Modified/proposed CSA with 4 bit - BEC unit<br><br>
•	Modified/proposed CSA with alternate MUX approach<br><br>
•	Generic CSA – customized version<br><br>
Each version will be discussed in the following sections.<br><br>

Traditional Carry- Select Adder:
•	A CSA divides the words to be added into two blocks; hence two sums are calculated in parallel.
•	The first block calculates the sum, assuming that carry-in(cin) = 0.
•	The second block calculates the sum, assuming that carry-in(cin) = 1.
•	Finally, the sums (4-bit each) and carry-out (cout) (1-bit each) of each adder is concatenated respectively in the format {coutRCA, sumRCA} and given as input to a 2:1 multiplexer.
•	The select line for a Mux is the carry-out of the preceding Mux.
•	The carry-out of the adder is obtained through the Multiplexer present in the last stage {i.e, for inputs A [15:12] and B [15:12]}.
•	Each stage has a varying input sizes i.e, 2,3,4,5 bits.
•	The RCA are also designed according to the inputs.

 <img width="978" height="477" alt="Screenshot 2025-07-26 145157" src="https://github.com/user-attachments/assets/93fa9bc0-7f6c-4104-b13f-131247e02938" /><br><br>
Fig1: A traditional CSA with fixed input size <br><br>


<img width="1347" height="489" alt="Screenshot 2025-07-26 145302" src="https://github.com/user-attachments/assets/2e272091-8156-4766-8f48-fa2359e2f590" /><br><br>
Fig2: A traditional CSA with varying input size<br><br>


Modified/proposed CSA with 4 bit - BEC unit:
•	BEC refers to a Binary to Excess-One converter.
•	In this approach of designing the CSA, the BEC unit is replaced in place of RCA, in the traditional architecture, which works on cin = 1’b1.  
•	The Boolean expressions for a 4-bit BEC are stated as:
i.	X0 = ~B0
ii.	X1 = B0^B1
iii.	X2 = B2^(B0&B1)
iv.	X3 = B3^(B0&B1&B2)
•	Logic diagram of the same is as follows:

<img width="958" height="668" alt="Screenshot 2025-07-26 153139" src="https://github.com/user-attachments/assets/fdab2af6-0aab-462c-a7a8-1029407983fd" />
Fig3: A 4-bit BEC



Modified/proposed CSA with alternate MUX approach:
•	This approach involves designing separate Multiplexers which operate on carry-out and sums of the two RCAs respectively.
•	Select line, however remains the same foe both 2:1 Muxes, ie, the carry out of the preceding Mux.
•	By adapting this architecture, grouping of carry and sum, which are provided as inputs in former approaches can be avoided hence speeding up calculations.


<img width="1368" height="505" alt="Screenshot 2025-07-26 154055" src="https://github.com/user-attachments/assets/7fbd8fba-f149-4b93-b684-7cf220eedc56" />
Fig4: Modified CSA architecture with alternate MUX approach


Generic CSA – customized version:
•	This is a customized version of CSA, where 16,32,64,128,256… bit input can be given.
•	It involves usage of generate statement in coding the hardware, in Verilog.
•	An efficient, customizable way where it can be used in applications involving varying input bit lengths.
Results and Discussion:

<img width="1864" height="292" alt="Screenshot 2025-07-26 202901" src="https://github.com/user-attachments/assets/09573222-fa9b-4c83-980d-e7cf1ec80d01" />
Fig5: Traditional CSA architecture waveforms

<img width="1863" height="381" alt="Screenshot 2025-07-26 203253" src="https://github.com/user-attachments/assets/0e520abe-762a-4432-998b-e5c42bda7a38" />
Fig6: proposed CSA with 4-bit BEC waveforms


<img width="1869" height="286" alt="Screenshot 2025-07-26 203730" src="https://github.com/user-attachments/assets/34964f4a-5c86-44eb-b8b2-4cf4e2e8b466" />
Fig7: proposed CSA with alternate Mux approach waveforms

<img width="1867" height="325" alt="Screenshot 2025-07-26 222011" src="https://github.com/user-attachments/assets/246aba97-8346-4935-850b-f8523130f08c" />
Fig7: proposed generic CSA with N=256 waveforms


Observation and Inference:
•	The Area and delay report for each design is as follows:


<img width="746" height="329" alt="image" src="https://github.com/user-attachments/assets/88c494c6-d360-4c1d-8684-55bacb095664" />
Table 1: Area Report

•	Resource usage on Artix-7 FPGA is as follows:

<img width="907" height="350" alt="image" src="https://github.com/user-attachments/assets/6a930e84-fdc9-4f8f-ba3d-bb7d350ba0a9" />
Table 2: Analysis of resource usage on Artix-7 FPGA

•	The Mux report (also called Macro reports), extracted from Xilinx ISE, post synthesis, is as follows:
1.	Traditional CSA:
<img width="1920" height="964" alt="Macro_report-regular_csa" src="https://github.com/user-attachments/assets/57325f52-c634-463d-8408-3757216cd5f8" />

2.	Modified/proposed CSA with 4 bit - BEC unit:
<img width="1920" height="964" alt="Macro_report-proposed_csa_a" src="https://github.com/user-attachments/assets/38a41c18-0dc7-4354-9ce5-5d8f5371f329" />

3.	Modified/proposed CSA with alternate MUX approach:
<img width="1920" height="964" alt="Macro_report-proposed_csa_b" src="https://github.com/user-attachments/assets/7b6e98e2-c0c1-46e7-bf15-8e6bfdea5729" />

4.	Generic CSA – customized version with N = 256:
<img width="1920" height="964" alt="Macro_report-proposed_csa_customized" src="https://github.com/user-attachments/assets/7575ee3f-c297-4e53-809b-e8d089788505" />
















•	Conclusion:

     From table 2, it can be observed that when compared to the traditional approach, CSA with 4-bit BEC architecture has consumed more LUT slices. The estimated increase in area can be calculated as (35-26)/35 * 100% i.e., almost equal to 25.7% increase in area. On the other side, we notice a decrease in combinational delay taken by CSA with 4-bit BEC architecture compared to the traditional approach i.e., around (5.902-4.006)/5.902 * 100% almost equal to 32.12% lesser. Hence, we can infer that “reduction in delay comes by compromising area consumed by the architecture”. There exists a trade-off between delay and area. This may also be interpreted as a future scope for this project.


•	References and Citations:
[1]  S. Sakthikumaran, S. Salivahanan, V. S. K. Bhaaskaran, V. Kavinilavu, B. Brindha and C. Vinoth, "A very fast and low power carry select adder circuit," 2011 3rd International Conference on Electronics Computer Technology, Kanyakumari, India, 2011, pp. 273-276, doi: 10.1109/ICECTECH.2011.5941604.

[2] B. Ramkumar and H. M. Kittur, "Low-Power and Area-Efficient Carry Select Adder," in IEEE Transactions on Very Large Scale Integration (VLSI) Systems, vol. 20, no. 2, pp. 371-375, Feb. 2012, doi: 10.1109/TVLSI.2010.2101621.


