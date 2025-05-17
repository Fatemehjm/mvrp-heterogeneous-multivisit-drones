# The Multi-Visit Vehicle Routing Problem with Heterogeneous Landing for Multiple Drones (mVRP-HmD)

This repository provides benchmark datasets and the full source code required to run the **mVRP-HmD solver**.  
The mVRP-HmD is a novel extension of the classical Vehicle Routing Problem (VRP), in which **multiple UAVs with multi-visit capabilities** collaborate with trucks to deliver parcels while minimizing the total makespan.

Unlike most existing models, drones in this problem are allowed to land on **any available truck**, not necessarily the one they launched from, enabling more flexible synchronization between UAVs and vehicles.

---

## Associated Article

This repository accompanies the following scientific article (under submission):

> **Fatemeh Jamshidian**, Mohammad Sadeghi, Saeed Yaghoubi *(Corresponding Author)*  
> *"The Multi-Visit Vehicle Routing Problem with Heterogeneous Landing for Multiple Drones"*, 2025.

---

##  Repository Contents

- `main_code.ipynb`: Jupyter-style notebook (executed using the Julia kernel in Visual Studio Code), implementing the metaheuristic algorithm based on Simulated Annealing.
- `dataset/`: Folder containing X–Y coordinates of benchmark customer locations:
  - `r101.txt`
  - `c101.txt`
  - `rc101.txt`
- `README.md`: This file.
- `LICENSE`: MIT License for open usage and distribution.

---

##  Problem Description

The mVRP-HmD problem includes:
- A depot and multiple customer nodes.
- One or more trucks.
- Multiple UAVs (drones) that can visit **more than one customer per route** (multi-visit).
- Drones can land on **any truck**, not just their launcher.
- Objective: **Minimize makespan**.

---

##  Compatibility

- Julia ≥ 1.8
- Visual Studio Code with:
  - Julia extension
  - Jupyter extension (for running `.ipynb` notebooks)
- Multi-threading supported (optional)

---

##  Prerequisites

The following Julia packages are required:

```julia
using DataStructures
using Graphs
using Random
using StatsBase
using LinearAlgebra
using Base.Threads

To install these, run the following in Julia's REPL:

using Pkg
Pkg.add(["DataStructures", "Graphs", "Random", "StatsBase"])

LinearAlgebra and Base.Threads are built-in modules and don’t need installation.

## Installation and Setup

To set up your environment:

    Install Julia (version 1.8 or later).

    Install Visual Studio Code.

    Install the following extensions in VS Code:

        Julia extension

        Jupyter extension

    Clone or download this repository.

## Download Problems and Source Code
Option 1: Download as ZIP

    Click the green “Code” button on this page.

    Choose Download ZIP.

    Extract the archive on your computer.

Option 2: Clone with Git

cd <your-directory>
git clone https://github.com/your-username/mvrp-heterogeneous-drones.git




This will execute the metaheuristic algorithm, generate solution routes, and display the final makespan.


## Running the Solver

1. Open the project folder in **VS Code**.
2. Open `main_code.ipynb` using the **Julia kernel** (you will be prompted to select a kernel at the top).
3. Run the cells in order.

This will execute the metaheuristic algorithm, generate solution routes, and display the final makespan.

##Adjustable Parameters
- The number of nodes (including depot and customers) is defined by the variable `nNodes` inside the notebook.
- Based on this value, the code automatically generates appropriate **distance matrices for both trucks and drones**.
- You may adjust `nNodes` to run the algorithm on a subset of customers (e.g., 6, 10, or all 100).

##Multithreading Note

This code is optimized to use **Julia's multithreading capabilities** for performance improvement during search and neighbor generation.

If your Julia setup does **not** support multithreading (or if you want to run the code single-threaded), you must do the following modifications inside the notebook:

- In **Line 38**, comment out the multithreaded line:
  ```julia
  # @threads for i in eachindex(1:nPop) 
And uncomment Line 39:
for i in 1:nPop

Similarly, in Line 74, comment out the multithreaded loop:
# @threads for i in eachindex(1:nPop) 

And uncomment Line 75:
for i in 1:nPop


## Dataset Format

Each file in dataset/ contains 101 lines in the format:

<x_coordinate> <y_coordinate>

The first line (ID 1) is the depot.

Lines 2–101 are customer nodes.


## Special Note on Depot Representation

Although the problem contains only one physical depot, the code defines two depot nodes in the distance matrix:

    Node 1 represents the starting depot.

    Node 102 is a duplicate of the depot and is used as the ending depot.

This structure simplifies route construction and makespan calculations.
As a result, the full distance matrix is of size 102 × 102, accounting for 100 customers + 2 depot nodes.

## License

This project is licensed under the MIT License.
Free for academic and commercial use with proper attribution.

## Contact

For questions or collaboration requests, please contact the corresponding author:
Saeed Yaghoubi
Yaghoubi@iust.ac.ir

