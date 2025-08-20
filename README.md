<img width="1203" height="1023" alt="Screenshot 2025-08-20 204400" src="https://github.com/user-attachments/assets/0e55c1b8-f3b6-4073-a46d-6ecac1055a48" /><img width="1203" height="1023" alt="Screenshot 2025-08-20 204400" src="https://github.com/user-attachments/assets/c4f01a8e-32da-4a21-96d9-eed6e374379c" />


## ASIC Implementation of a Serial-Parallel Multiplier

This project demonstrates a complete **RTL-to-GDSII** flow for a custom 32-bit Serial-Parallel Multiplier (SPM) using the open-source [OpenLane2](https://github.com/efabless/openlane2) ASIC toolchain and the [Google-Skywater SKY130](https://skywater-pdk.readthedocs.io/) process node.

The implementation was performed on **Google Colab**, proving the feasibility of cloud-based ASIC design with open-source tools.



## 📁 Project Structure

├── src/verilog/spm.v # Source RTL for the multiplier
├── config/ # OpenLane configuration files
├── runs/sample_run/ # Sample output from a successful run
└── images/ # Screenshots of results




## 🧮 Architecture Overview

The multiplier is architected for area efficiency, using a bit-serial approach. The core consists of:
*   **Carry-Save Adders (CSAs):** Chained together to form the multiplication array, minimizing propagation delay.
*   **Terminal Cell (TCMP):** A custom-designed cell to handle the sign extension and final accumulation for the most significant bit.
*   **Pipelining:** All state elements are clocked, making the design synchronous.



## ⚙️ Toolflow & Implementation

The design was processed through the following steps in the OpenLane2 flow:

1.  **Synthesis:** Using `Yosys` to translate RTL to a gate-level netlist with `sky130` standard cells.
2.  **Floorplanning:** Defining the chip core and die area.
3.  **Placement:**
    *   **Global Placement:** Creating an optimal but illegal placement.
    *   **Detailed Placement:** Legalizing the placement onto the standard cell grid.
4.  **Clock Tree Synthesis (CTS):** Building a balanced clock tree to minimize skew.
5.  **Routing:**
    *   **Global Routing:** Planning the route guides for all nets.
    *   **Detailed Routing:** Implementing the physical wiring using `TritonRoute`.
6.  **Signoff:**
    *   **DRC:** Design Rule Checking with `Magic`.
    *   **LVS:** Layout vs. Schematic checking with `Netgen`.



## 🚀 How to Replicate

The flow was designed for Google Colab. You can find the complete notebook and instructions for running it here:  
**[Link to your Colab Notebook]** *(If you saved it to your GitHub, you can link it here)*

### Prerequisites
*   A Google account to access Colab.
*   Basic understanding of Verilog and ASIC design flow.

### Running the Flow
1.  Open the provided Colab notebook.
2.  Follow the cells sequentially to install OpenLane, run the flow, and view results.
3.  The final GDS and reports will be generated in the Colab runtime.




## 📊 Results

### Physical Layout
![Final GDSII Layout of the Multiplier](https://1drv.ms/i/c/0804a4e2c31682bf/EYP2K5VU9RtIjtaDThcUx5YBa2ACYVoRgpFw78CaNWZCZQ?e=FczSuN)
*Final GDSII layout of the 32-bit SPM, visualized in KLayout.*


### Performance Metrics
Key metrics from the final run (`runs/sample_run/reports/metrics.csv`):

| Metric          | Value | Unit |
|-----------------|-------|------|
| Core Area       | TBD   | µm²  |
| Die Area        | TBD   | µm²  |
| Standard Cells  | TBD   | #    |
| Worst Negative Slack (WNS) | TBD | ns |
| Total Power     | TBD   | mW   |

*(Replace TBD with actual values from your run's summary report)*




## ✅ Verification

*   **Functional Verification:** Pre-synthesis simulation testbench (not included) validated the RTL logic.
*   **LVS:** The final layout was verified to be functionally equivalent to the synthesized netlist. **CLEAN**.
*   **DRC:** The final GDSII passed all Sky130 design rules. **CLEAN**.


  

## 🔧 Technologies Used

*   **EDA Tools:** OpenLane2, Yosys, OpenROAD, Magic, Netgen
*   **PDK:** Skywater SKY130 Process Design Kit
*   **RTL:** Verilog/HDL
*   **Platform:** Google Colab
*   **Package Management:** Nix



## 👤 Author

Ganesh Kuppasta - [https://www.linkedin.com/in/ganesh-kuppasta-0677392ab/]



## 📜 License

This project is licensed under the **Apache 2.0 License** - see the [LICENSE](LICENSE) file for details. This project uses the Skywater SKY130 PDK, which is also open-source.




## 🙏 Acknowledgments

*   [EFabless](https://www.efabless.com/) and the OpenLane team.
*   [Google](https://opensource.googleblog.com/2020/06/announcing-collaboration-with-skywater.html) and [SkyWater Technology](https://www.skywatertechnology.com/) for the open-source PDK.
*   The open-source hardware community.
