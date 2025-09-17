# SIMULATION AND IMPLEMENTATION OF 4:1 MULTIPLEXER

## AIM
To design and simulate a 4:1 Multiplexer (MUX) using Verilog HDL in four different modeling styles—Gate-Level, Data Flow, Behavioral, and Structural—and to verify its functionality through a testbench using the Vivado 2023.1 simulation environment. The experiment aims to understand how different abstraction levels in Verilog can be used to describe the same digital logic circuit and analyze their performance.

## APPARATUS REQUIRED
- **Vivado 2023.1**

## Procedure

1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** and give a name (e.g., `Mux4_to_1`).  
3. Add/create your Verilog files and testbench.  
4. Select an FPGA part (e.g., `xc7a35ticsg324-1L`).  
5. Run **Synthesis** to check for errors.  
6. Run **Simulation** → **Run Behavioral Simulation**.  
7. Observe the waveforms of inputs and outputs.  
8. Adjust simulation time if needed (e.g., 1000ns).  
9. Save the project and take screenshots of results.  
10. Close simulation.  

---

## Logic Diagram
![image](https://github.com/user-attachments/assets/d4ab4bc3-12b0-44dc-8edb-9d586d8ba856)

---

## Truth Table
![image](https://github.com/user-attachments/assets/c850506c-3f6e-4d6b-8574-939a914b2a5f)

---

## Verilog Code

### 4:1 MUX Gate-Level Implementation
```verilog
// Gate Level Modelling - Skeleton
`timescale 1ns / 1ps

module mux2(i,s,y);
input [3:0]i;
input [1:0]s;
output y;
wire [3:0]w;
and g1 (w[0],i[0],~s[1],~s[0]);
and g2 (w[1],i[1],~s[1],s[0]);
and g3 (w[2],i[2],s[1],~s[0]);
and g4 (w[3],i[3],s[1],s[0]);
or g5 (y,w[0],w[1],w[2],w[3]);
endmodule

```
### 4:1 MUX Gate-Level Implementation- Testbench
```verilog
// Testbench Skeleton
`timescale 1ns/1ps
module mux4_1_tb;
reg [3:0]i;
reg [1:0]s;
wire y;
mux2 uut(i,s,y);
initial
begin
i=4'b1011;
s=2'b00;
#10;
$display("Selection line is %b %b,Output is %b",s[1],s[2],y);
s=2'b01;
#10;
$display("Selection line is %b %b,Output is %b",s[1],s[2],y);
s=2'b10;
#10;
$display("Selection line is %b %b,Output is %b",s[1],s[2],y);
s=2'b11;
#10;
$display("Selection line is %b %b,Output is %b",s[1],s[2],y);
$finish;
end
endmodule
```
## Simulated Output Gate Level Modelling
<img width="1919" height="1079" alt="Screenshot 2025-08-25 170214" src="https://github.com/user-attachments/assets/293afa83-a50c-4abd-9060-459bdb0fce9e" />


---
### 4:1 MUX Data flow Modelling
```verilog
// Dataflow Modelling - Skeleton
`timescale 1ns / 1ps

module mux2(i,s,y);
input [3:0]i;
input [2:1]s;
output y;
wire [3:0]w;
assign w[0]=i[0] & (~s[2]) & (~s[1]);
assign w[1]=i[1] & (~s[2]) & s[1];
assign w[2]=i[2] & s[2] & (~s[1]);
assign w[3]=i[3] & s[2] & s[1];
assign y= w[0]|w[1]|w[2]|w[3];
endmodule 
```
### 4:1 MUX Data flow Modelling- Testbench
```verilog
// Testbench Skeleton
`timescale 1ns/1ps
module mux4_1_tb;
reg [3:0]i;
reg [1:0]s;
wire y;
mux2 uut(i,s,y);
initial
begin
i=4'b1111;
s=2'b00;
#10;
$display("Selection line is %b %b,Output is %b",s[1],s[2],y);
s=2'b01;
#10;
$display("Selection line is %b %b,Output is %b",s[1],s[2],y);
s=2'b10;
#10;
$display("Selection line is %b %b,Output is %b",s[1],s[2],y);
s=2'b11;
#10;
$display("Selection line is %b %b,Output is %b",s[1],s[2],y);
$finish; 
end
endmodule

```
## Simulated Output Dataflow Modelling
<img width="1919" height="1079" alt="Screenshot 2025-08-27 093417" src="https://github.com/user-attachments/assets/51f01ac6-dabd-4745-81a4-ea3c25e6dd72" />







---
### 4:1 MUX Behavioral Implementation
```verilog
`timescale 1ns / 1ps

module MUX4_1(i,s,y);
input[3:0]i;
input[1:0]s;
output reg y;
always @(i,s)
    begin
        case(s)
        2'b00:y=i[0];
        2'b01:y=i[1];
        2'b10:y=i[2];
        2'b11:y=i[3];
        endcase
    end
endmodule

```
### 4:1 MUX Behavioral Modelling- Testbench
```verilog
// Testbench Skeleton
`timescale 1ns/1ps
module mux4_1_tb;
reg [3:0]i;
reg [1:0]s;
wire y;
MUX4_1 uut(i,s,y);
initial
begin
i=4'b1001;
s=2'b00;
#10;
$display("Selection line is %b %b,Output is %b",s[1],s[2],y);
s=2'b01;
#10;
$display("Selection line is %b %b,Output is %b",s[1],s[2],y);
s=2'b10;
#10;
$display("Selection line is %b %b,Output is %b",s[1],s[2],y);
s=2'b11;
#10;
$display("Selection line is %b %b,Output is %b",s[1],s[2],y);
$finish;
end
endmodule
```
## Simulated Output Behavioral Modelling

<img width="1919" height="1079" alt="Screenshot 2025-08-22 120108" src="https://github.com/user-attachments/assets/ad266ac1-321c-4767-afe2-39e1779d70bf" />



### 4:1 MUX Structural Implementation

![image](https://github.com/user-attachments/assets/eea81c2c-7dfa-43aa-9cea-1ab4ed54db6c)


```verilog
`timescale 1ns / 1ps
module mux41_4(a,b,s,z);
input a,b,s;
output z;
wire w1,w2;
and g1(w1,a,~s);
and g2(w2,b,s);
or g3(z,w1,w2);
endmodule

module MUX41(i,s,y);
input [3:0]i;
input [1:0]s;
output y;
wire [2:1]w;
MUX41_4 M1(w[1],i[0],i[1],s[1]);
MUX41_4 M2(w[2],i[2],i[3]),s[1]);
MUX41_4 M3(y,w[1],w[2],s[0]);
endmodule

```
### Testbench Implementation
```verilog
`timescale 1ns / 1ps
module MUX_41_tb;
reg [3:0]i;
reg [1:0]s;
wire y;
MUX41 uut(i,s,y);
initial
begin
i=4'B1111;
s=2'b00; #10
$display("Selection is %b %b , output : %b ", s[1],s[0],y);
s=2'b01; #10
$display("Selection is %b %b , output : %b ", s[1],s[0],y);
s=2'b10; #10
$display("Selection is %b %b , output : %b ", s[1],s[0],y);
s=2'b11; #10
$display("Selection is %b %b , output : %b ", s[1],s[0],y);
$finish;
end
endmodule

```
## Simulated Output Structural Modelling

<img width="1919" height="1078" alt="Screenshot 2025-08-29 110030" src="https://github.com/user-attachments/assets/8a500ee2-83f8-4dd8-b46a-8b79af357872" />


---
### CONCLUSION

In this experiment, a 4:1 Multiplexer was successfully designed and simulated using Verilog HDL across four different modeling styles: Gate-Level, Data Flow, Behavioral, and Structural.The simulation results verified the correct functionality of the MUX, with all implementations producing identical outputs for the given input conditions.

