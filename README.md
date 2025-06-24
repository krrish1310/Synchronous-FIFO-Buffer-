Here's a concise and clear `README.md` for your parameterized FIFO Verilog project:

---

#  Parameterized FIFO (First-In-First-Out) Buffer – Verilog Implementation

This project implements a **parameterized FIFO (First-In-First-Out)** buffer in Verilog, allowing for customizable data width and depth. The FIFO supports simultaneous push and pop operations, and includes status indicators for full and empty conditions.

## 🔧 Features

*  **Parameterized Design**: Set data width (`DATA_W`) and FIFO depth (`DEPTH`) via module parameters.
*  **Push and Pop Support**: Handles independent or simultaneous push (`push_i`) and pop (`pop_i`) requests.
*  **Full and Empty Flags**: Indicates whether FIFO is full or empty.
*  **Pointer Wrapping with Flags**: Handles pointer wrapping using wrapping flags to differentiate between full and empty states when read and write pointers are equal.
*  **Synchronous Memory Array**: FIFO data is stored in a synchronous memory array with `always_ff`.

# Module Interface

### Parameters

* `DATA_W` (default = 8): Width of the data.
* `DEPTH` (default = 4): Number of entries in the FIFO (must be a power of 2 ideally).

### Ports

| Signal Name   | Direction | Width        | Description                   |
| ------------- | --------- | ------------ | ----------------------------- |
| `clk`         | Input     | 1 bit        | Clock signal                  |
| `reset`       | Input     | 1 bit        | Active-high synchronous reset |
| `push_i`      | Input     | 1 bit        | Push (write) enable           |
| `push_data_i` | Input     | DATA\_W bits | Data to push into FIFO        |
| `pop_i`       | Input     | 1 bit        | Pop (read) enable             |
| `pop_data_o`  | Output    | DATA\_W bits | Data popped from FIFO         |
| `full_o`      | Output    | 1 bit        | Asserted when FIFO is full    |
| `empty_o`     | Output    | 1 bit        | Asserted when FIFO is empty   |

## 🔄 Internal Design

* **FIFO Array**: `fifo_data_q[DEPTH]` stores the data entries.
* **Pointers**: `rd_ptr_q` and `wr_ptr_q` track read and write locations.
* **Wrapped Flags**: `wrapped_rd_ptr_q` and `wrapped_wr_ptr_q` indicate wrap-around, distinguishing full and empty states when pointers are equal.
* **Pointer Logic**: Uses a 2-bit FSM-style case for handling push, pop, or both.
* **State Encoding**:

  * `ST_PUSH = 2'b10`
  * `ST_POP = 2'b01`
  * `ST_BOTH = 2'b11`

## 🧪 Test and Verification

Testbench should verify:

* Data integrity during normal operations.
* Behavior on simultaneous push and pop.
* Proper assertion of `full_o` and `empty_o`.
* Pointer wrap-around behavior.

## 📁 File Structure

```
├── qs_fifo.v        # Main Verilog FIFO module
├── qs_fifo_tb.v     # (Optional) Testbench (recommended to add)
└── README.md        # This documentation file
```

## 🛠️ Future Enhancements

*  Add asynchronous reset.
*  Add programmable thresholds for nearly full/empty.
*  Make FIFO depth support any value (not just powers of 2).
*  Add output valid signal for read stability.

##  Author

* **Krrish Kumar**
  Indian Institute of Technology, Kharagpur
  GitHub: [krrish1310](https://github.com/krrish1310)

---

