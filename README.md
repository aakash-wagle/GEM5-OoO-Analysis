# GEM5 Out-of-Order (OoO) CPU Analysis

This project explores the impact of different **Out-of-Order (OoO) core configurations** on CPU performance using the [gem5 simulator](https://www.gem5.org/). The analysis focuses on varying **pipeline width, branch predictor type, and reorder buffer (ROB) entries** to identify an optimized "GoodCore" configuration that balances performance and resource usage.

## Features

- **Simulation of OoO CPU Models**:
  - Uses `O3CPU` (Out-of-Order) models in gem5.
  - Evaluates different pipeline widths, branch predictors, and ROB sizes.

- **Benchmarking**:
  - Evaluates **Rodinia (BFS, Hotspot)** and **Stanford (Quicksort, Bubblesort)** benchmarks.

- **Performance Analysis**:
  - Measures **Instruction Per Cycle (IPC), execution time, cache hit/miss rates**, and **branch prediction accuracy**.

## Installation & Setup

1. **Clone the repository**:

   ```bash
   git clone https://github.com/aakash-wagle/GEM5-OoO-Analysis.git
   cd GEM5-OoO-Analysis
   ```

2. **Set up gem5**:

   - Follow the [gem5 installation guide](https://www.gem5.org/documentation/).
   - Ensure gem5 is built and accessible in your system's PATH.

3. **Compile Benchmarks**:

   Navigate to the `benchmarks` directory and compile the programs:

   ```bash
   cd benchmarks
   make
   ```

## Running Simulations

1. **Configure Simulation**:

   - Modify the CPU and system configuration scripts (`a4CPUConfig.py`, `a4O3CPUConfig.py`, `cse530_a4_sys_config.py`) to set desired simulation parameters.

2. **Execute Simulation**:

   - Run gem5 with the specified configuration:

     ```bash
     gem5.opt -d simulations/results/ a4O3CPUConfig.py --cse530-core-config=small --binfile=benchmarks/bubblesort
     ```

   - Adjust the output directory and configuration script as needed for different benchmarks or CPU models.

3. **Analyze Results**:

   - Use the `analysis.ipynb` notebook to process and visualize simulation data.

## Experimentation & Observations

1. **Core Configurations**:
   - The study compares **SmallCore (pipeline width = 2, ROB = 16, 2-bit branch predictor)** and **LargeCore (pipeline width = 8, ROB = 192, LTAGE branch predictor)**.
   - Intermediate configurations (`C1, C2, C3`) were tested to find an optimal **GoodCore** setup.

2. **Key Findings**:
   - **Pipeline width** significantly impacts **IPC**, but increasing it beyond a threshold gives diminishing returns.
   - **Branch predictor choice** affects **misprediction rates and execution time**.
   - **Reorder buffer size** has a strong impact on **instruction throughput** but leads to increased resource usage.

3. **Final GoodCore Configuration**:
   - After multiple experiments, an optimized **GoodCore** was identified that provides **most of the performance benefits of LargeCore while using fewer resources**.

## Documentation

For a **detailed analysis**, refer to the **[Project Report](./Report.pdf)**, which includes:

- Performance graphs showing **IPC improvements and execution time speedups**.
- Observations on **core parameter dependencies** and **benchmark characteristics**.
- Justifications for the **final GoodCore selection**.

Let me know if you need any refinements! 🚀
