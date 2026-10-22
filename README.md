# APB Protocol Verification using UVM

This project verifies an APB (Advanced Peripheral Bus) slave design using a UVM testbench written in SystemVerilog.

Based on the APB UVM testbench by Kittu K Patel:
https://www.edaplayground.com/x/ZxB9

## About the Design (design.sv)
- APB slave module with a clock (PCLK) and an active-low reset (PRESETn)
- Inputs: PSEL, PENABLE, PWRITE, PADDR (8-bit), PWDATA (8-bit)
- Outputs: PRDATA (8-bit), PREADY, PSLVERR
- Has an 8x8-bit internal memory
- Has a parameter N that sets the number of wait states
- Supports write (PWRITE = 1) and read (PWRITE = 0) transfers

## Testbench Architecture
The testbench is built with UVM and follows this flow:

Sequence -> Sequencer -> Driver -> DUT -> Monitor -> Scoreboard
                                                       ^
                                          Reference Model

## Files
| File | What it does |
|------|--------------|
| design.sv | APB slave design (DUT) |
| testbench.sv | Top module that connects the design and the testbench |
| APB_INTERFACE.sv | Interface that holds the APB signals |
| APB_DEFINE.sv | Common definitions |
| APB_TRANS.sv | Transaction (sequence item) with address, data and read/write |
| APB_SEQUENCE.sv | Creates the transactions |
| APB_SEQUENCER.sv | Sends transactions to the driver |
| APB_DRIVER.sv | Drives the signals onto the APB interface |
| APB_MONITOR.sv | Watches the interface and collects the actual transactions |
| APB_AGENT.sv | Groups the driver, monitor and sequencer |
| APB_reference_model.sv | Predicts the expected output (golden model) |
| APB_SCOREBOARD.sv | Compares the DUT output with the reference model |
| APB_ENV.sv | Environment that connects all the components |
| APB_TEST.sv | Test that runs the sequences |
| APB_PKG.sv | Package that includes all the testbench files |

## How to Run
1. Open the EDA Playground link above
2. Select SystemVerilog/Verilog and UVM 1.2
3. Choose a simulator and click Run

## Tools
- SystemVerilog
- UVM 1.2
- EDA Playground
