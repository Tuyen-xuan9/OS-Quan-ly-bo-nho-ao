# Virtual Memory Page Replacement Simulator

An application that visually simulates 3 classic virtual memory page replacement algorithms: **FIFO**, **LRU**, and **OPT (Optimal)**.

## Table of Contents

- [Main Features](#-main-features)
- [Folder Structure](#-folder-structure)
- [System Requirements](#-system-requirements)
- [Installation & Run](#-installation--run)
- [User Guide](#-user-guide)

## Main Features

| Category | Details |
|---|---|
| **3 Algorithms** | FIFO, LRU, OPT. |
| **Visual Gantt Chart** | **Step-by-step animation** with Play/Pause/Reset/End controls. |
| **Algorithm Comparison** | Comparison tab: Faults, Hits, Hit Rate, Exec Time. |
| **Flexible Input** | Load an existing CSV file or enter data manually. |
| **CSV Report Export** | 2 modes: export each algorithm individually, or export all 3 at once. |
| **Stress Test / Benchmark** | Standalone script that measures the runtime of all 3 algorithms with a reference string of up to 100,000 elements. |
| **Input Error Handling** | Automatically skips invalid characters and negative numbers, and validates `frame_size` within the 1–20 range. |


## 📁 Folder Structure
```
├── main.py                        # Entry point
│
├── algorithms/                    # Core page replacement algorithms
│   ├── base.py                    #   ABC PageReplacementAlgorithm
│   ├── fifo.py                    #   FIFO — deque
│   ├── lru.py                     #   LRU + LRUClock
│   ├── opt.py                     #   OPT/Belady
│   └── registry.py                #   AlgoRegistry
│
├── models/
│   └── step.py                    # Step — state of a single step (frames, fault/hit,
│                                   #        hit_rate, next_use, to_dict/to_csv_row...)
│
├── utils/
│   └── file_handler.py            # Reads input CSV, writes output CSV, generates sample/stress inputs
│
├── GUI/
│   ├── display.py                 # App (tk.Tk)
│   ├── gantt.py                   # GanttTab
│   ├── compare.py                 # CompareTab
│   └── widgets.py                 # Color palette (C), font helper (F), shared widgets
│
├── unit_tests/
│   ├── test_algorithms.py         # TestRunner
│   └── stress_runner.py           # Performance benchmark
│
├── input/                         # Input CSV files (samples + test cases)
│   ├── input.csv
│   ├── basic_testcase.csv
│   ├── belady_test.csv
│   ├── stress_test_1.csv / _2.csv / _3.csv
│   ├── testcase_no_page_fault.csv
│   ├── testcase_large_frames.csv
│   ├── testcase_extreme_page_fault.csv
│   ├── testcase_invalid_characters.csv
│   └── testcase_invalid_negative_frame.csv
│
└── output/                        # Sample result CSV files after export
    ├── output_FIFO.csv
    ├── output_LRU.csv
    └── output_OPT.csv
```

## System Requirements

- **Python 3.8+**
- **Tkinter** — usually included with standard Python.
  - Windows/macOS: included by default.
  - Linux: if missing, install with:
    ```bash
    sudo apt install python3-tk
    ```
- No additional external libraries required.


## Installation & Run

```bash
# 1. Clone / extract the project, then move into the root folder
cd OS_VME_08

# 2. (Optional) Create a virtual environment
python -m venv venv
source venv/bin/activate      # Linux/macOS
venv\Scripts\activate         # Windows

# 3. Run the program
python main.py
```

### Run Unit Tests Standalone (no GUI required)

```bash
python unit_tests/test_algorithms.py
```

### Run Stress Test / Benchmark

```bash
python unit_tests/stress_runner.py
```

Results are written to `output/stress_results.csv` and `output/stress_summary.txt`.

## User Guide

1. **Enter Data**
   - Click **📂 Load CSV file** to select an existing `.csv` file, or
   - Drag the **FRAME SIZE** slider (1–10) and type the reference string directly (comma-separated) into the **REFERENCE STRING** field.

2. **Run an Algorithm**
   - Click **▶ Run FIFO / LRU / OPT** to run a single algorithm individually → automatically switches to the **Gantt Chart** tab.
   - Click **⚡ Run ALL & Compare** to run all 3 at once → automatically switches to the **Comparison** tab.

3. **View the Gantt Chart**
   - Hover over each cell to see a detailed tooltip (frame state, fault/hit, next use, etc.).
   - Use the **⏮ Reset / ▶ Play / ⏸ Pause / ⏭ End** controls and the speed slider to watch the step-by-step page replacement animation.

4. **Compare (Comparison tab)**
   - View statistics cards, bar charts (Faults / Hits / Hit Rate), and a ranking table sorted by lowest fault count.

5. **Export Results**
   - **💾 Export FIFO/LRU/OPT CSV** — exports the results of one algorithm that has already run.
   - **📦 Export 3 CSVs** — exports all 3 algorithms at once (requires **Run ALL** to have been clicked first) into a folder of your choice.

6. **Unit Tests**
   - **Unit Tests** tab → click **▶ Run All Unit Tests** to see all test case PASS/FAIL results directly within the application.

7. **Team Info**
   - Click the **👥 Group 5 - Info** button in the top-right corner to view the list of team members.

<p align="center">
  <sub>OS_VME_08 — Group 5 — HCMUTRANS © 2026</sub>
</p>
