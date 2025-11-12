# Seven-Segment Display Driver using Verilog HDL

## Aim  
To design and simulate a Verilog HDL seven-segment display driver that converts a 4-bit binary input into the corresponding digits 0–9.

## Apparatus Required  
- **Vivado 2023.1**
- **Spartan 7 FPGA**  

## Procedure  

## 1. Launch Vivado 2023.1
- Open Vivado 2023.1 and create a new project.
- Select **RTL Project** and enable **Do not specify sources at this time**.

## 2. Create Verilog Design File
- Create a new Verilog design file.
- Type the Verilog code for the Seven Segment Display.
- The code should convert a 4-bit input into the corresponding seven-segment output.

## 3. Create Constraint File
- Create a new XDC constraint file.
- Assign the FPGA pins for input switches, output segments, and the common anode/cathode according to the Real Digital Boolean Board (XC7S50CSGA324-1) pin mapping.

## 4. Synthesize the Design
- Click on **Run Synthesis** to check for design correctness.
- Ensure there are no syntax or mapping errors.

## 5. Implement the Design
- After successful synthesis, click on **Run Implementation**.
- Verify timing and pin placement in the implementation summary.

## 6. Generate Bitstream
- Click **Generate Bitstream** to create the programming file.
- Wait for the process to complete.

## 7. Program the FPGA
- Connect the Boolean Board to your PC.
- Open **Hardware Manager**, click **Open Target → Auto Connect**, and program the device with the generated bitstream.

## 8. Observe the Output
- Use the 4-bit DIP switches to provide binary inputs.
- Observe the Seven Segment Display showing the corresponding digits 0–9.

---
## Logic Diagram

<img width="589" height="511" alt="bcd2 7 segment" src="https://github.com/user-attachments/assets/e6922e13-6ec0-4f40-87ec-47be8862204d" />


## Verilog Code for Seven-Segment Display  

```verilog
module BCD_7(
    input  wire [3:0] binary_input,     // DIP switches SW0-SW3
    output reg  [6:0] seg_output,       // Segments a-g (active-low)
    output reg  [3:0] an                // Anode control (active-low)
);

always @(*) begin
    an = 4'b1110;

    // Decode binary input to 7-segment pattern
    case (binary_input)
        4'd0: seg_output = 7'b1000000; // 0
        4'd1: seg_output = 7'b1111001; // 1
        4'd2: seg_output = 7'b0100100; // 2
        4'd3: seg_output = 7'b0110000; // 3
        4'd4: seg_output = 7'b0011001; // 4
        4'd5: seg_output = 7'b0010010; // 5
        4'd6: seg_output = 7'b0000010; // 6
        4'd7: seg_output = 7'b1111000; // 7
        4'd8: seg_output = 7'b0000000; // 8
        4'd9: seg_output = 7'b0010000; // 9
        default: seg_output = 7'b1111111; // Blank
    endcase
end
endmodule

```
## Constraint file for Seven-Segment Display
```
## DIP SWITCHES (SW0-SW3 for BCD input)
set_property -dict { PACKAGE_PIN V2 IOSTANDARD LVCMOS33 } [get_ports {bcd[0]}]
set_property -dict { PACKAGE_PIN U2 IOSTANDARD LVCMOS33 } [get_ports {bcd[1]}]
set_property -dict { PACKAGE_PIN U1 IOSTANDARD LVCMOS33 } [get_ports {bcd[2]}]
set_property -dict { PACKAGE_PIN T2 IOSTANDARD LVCMOS33 } [get_ports {bcd[3]}]

## 7-SEGMENT DISPLAY (a,b,c,d,e,f,g,dp)
set_property -dict { PACKAGE_PIN D7 IOSTANDARD LVCMOS33 } [get_ports {seg[0]}]
set_property -dict { PACKAGE_PIN C5 IOSTANDARD LVCMOS33 } [get_ports {seg[1]}]
set_property -dict { PACKAGE_PIN A5 IOSTANDARD LVCMOS33 } [get_ports {seg[2]}]
set_property -dict { PACKAGE_PIN B7 IOSTANDARD LVCMOS33 } [get_ports {seg[3]}]
set_property -dict { PACKAGE_PIN A7 IOSTANDARD LVCMOS33 } [get_ports {seg[4]}]
set_property -dict { PACKAGE_PIN D6 IOSTANDARD LVCMOS33 } [get_ports {seg[5]}]
set_property -dict { PACKAGE_PIN B5 IOSTANDARD LVCMOS33 } [get_ports {seg[6]}]
set_property -dict { PACKAGE_PIN A6 IOSTANDARD LVCMOS33 } [get_ports {seg[7]}]

## ANODE CONTROL (active-low)
set_property -dict { PACKAGE_PIN D5 IOSTANDARD LVCMOS33 } [get_ports {an[0]}]
set_property -dict { PACKAGE_PIN C4 IOSTANDARD LVCMOS33 } [get_ports {an[1]}]
set_property -dict { PACKAGE_PIN C7 IOSTANDARD LVCMOS33 } [get_ports {an[2]}]
set_property -dict { PACKAGE_PIN A8 IOSTANDARD LVCMOS33 } [get_ports {an[3]}]
```
## FPGA Implementation Output

![FPGA 7 SEG](https://github.com/user-attachments/assets/127e82fd-d524-4746-88c5-1d0ea89d696a)


---

## Conclusion
In this experiment, a seven-segment display driver was successfully implemented using Verilog HDL in FPGA.This experiment demonstrates the practical application of Verilog HDL in designing and controlling digital hardware components, highlighting its importance in developing reliable and efficient digital systems.
