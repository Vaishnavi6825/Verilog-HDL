# Verilog-HDL
Digital CLock

`It is required to implement a digital lock that will accept a specific bit sequence “101100” through an input button “b_in” serially in synchronism with the negative edge of an input clock, and will generate an “unlock” signal “1” as output; for any other bit sequence the “unlock” signal will remain at logic “0”. An active low “clear” signal is used to asynchronously reset the lock in its initial/default state.`

Write a Verilog module to implement the specification as Moore machine using the following template:
module dlock (unlock, b_in, clear, clk);

`AIM:`
To stimulate and synthesis digital lock using Vivado.

`Software Required:`
vivado 2023.2 software.

`Procedure:`
STEP:1 Start the vivado software, Select and Name the New project.

STEP:2 Select the device family, device, package and speed.

STEP:3 Select new source in the New Project and select Verilog Module as the Source type.

STEP:4 Type the File Name and module name and Click Next and then finish button. Type the code and save it.

STEP:5 Select the run simulation and then run Behavioral Simulation in the Source Window and click the check syntax.

STEP:6 Click the simulation to simulate the program and give the inputs and verify the outputs as per the truth table.

STEP:7 compare the output with truth table.

`PROGRAM`
module lock_FSM(B0,B1,Reset,Clk,PASS,FAIL);
input B0,B1,Reset,Clk;
output reg PASS,reg FAIL;
reg [3:0] present_state, next_state;
parameter S0 = 4'b0000, S1 = 4'b0001, S2 = 4'b0010, S3 = 4'b0011, S4 = 4'b0100;
parameter E1 = 4'b0101, E2 = 4'b0110, E3 = 4'b0111, E4 = 4'b1000;
always @(posedge Clk, posedge Reset)
begin
if(Reset == 1)
present_state = S0;
end
always @(posedge B0, posedge B1)
begin
present_state = next_state;
end
always @ (present_state, B0, B1)
begin
if(B0 == 0 && B1 == 0)
next_state = present_state;
else
case (present_state)
S0 : next_state = B1 ? S1 : E1;
S1 : next_state = B0 ? S2 : E2;
S2 : next_state = B1 ? S3 : E3;
S3 : next_state = B0 ? S4 : E4;
E1 : next_state = E2;
E2 : next_state = E3;
E3 : next_state = E4;
endcase
end
always@(present_state)
begin
case(present_state)
S4: begin PASS = 1; FAIL = 0; end
E4: begin PASS = 0; FAIL = 1; end
default : begin PASS = 0; FAIL = 0; end
endcase
end
endmodule

`OUTPUT`

![image](https://github.com/user-attachments/assets/36e8d876-ae68-42fd-adcb-3b6e6d62bed0)

`RESULT:`
Thus the verilog program for digital lock has been simulated and verified successfully
