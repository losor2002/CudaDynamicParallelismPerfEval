# CUDA Dynamic Parallelism Performance Evaluation

This repository contains the project developed for the *High Performance Computing* exam.  
The goal is to evaluate the **performance of CUDA Dynamic Parallelism (CDP)** through a set of benchmarks and a written report.

## 📄 Report
The report is written in LaTeX and provided as a PDF:
- **Title:** *CUDA Dynamic Parallelism Performance Evaluation*  
- **Contents:** introduction to GPUs, CUDA, and CDP; detailed description of the selected benchmarks; experimental setup; performance analysis; and conclusions.
- **Benchmarks analyzed:**
  1. **Mandelbrot Set (Adaptive Mesh Refinement)**  
     Based on NVIDIA’s CDP Mandelbrot example, comparing standard vs. CDP refinement.
  2. **N-Body Simulation**  
     Implemented with both **Direct-Sum** ($O(N^2)$) and **Barnes–Hut** ($O(N\log N)$) methods, the latter relying on CDP for recursive tree construction.
  3. **Quadtree Construction**  
     Implemented in two equivalent versions: **iterative (no CDP)** vs. **recursive (CDP)**, to isolate the overhead of device-side launches.

The final report (`Report_HPC.pdf`) summarizes methodology, results, and insights.

## 🖥️ Experimental Setup
- **CPU:** AMD Ryzen 7 6800H (8 cores, SMT, 3.2 GHz base, up to 4.7 GHz boost)  
- **GPU:** NVIDIA GeForce RTX 3060 Mobile (3840 CUDA cores, 900 MHz base, up to 1425 MHz boost)  
- **OS:** Windows 11, with WSL used for some experiments due to compatibility issues  
- **Compiler:** NVIDIA `nvcc`  
  - Windows: V12.8.93  
  - WSL: V12.9.41  
- **Compilation flags:**  
  - `-O3` for all builds  
  - `-rdc=true` required for CDP versions

## 📂 Repository Structure
├── mandelbrot-dyn/ # Standard and CDP algorithms for calculating the Mandelbrot set, taken from [Nvidia Blog](https://developer.nvidia.com/blog/introduction-cuda-dynamic-parallelism/)

├── N-body-simulation/ # Direct-Sum and Barnes–Hut algorithms for the N-body problem, taken from [Medium](https://medium.com/@hsinhungw/optimizing-n-body-simulation-with-barnes-hut-algorithm-and-cuda-c76e78228c28)

├── cdpQuadTree/ # Iterative and CDP versions of the algorithm for building a QuadTree, CDP version taken from [Nvidia](https://developer.download.nvidia.com/compute/DevZone/C/html_x64/samples.html)

├── Report_HPC.pdf # Final compiled report

└── README.md

## ▶️ How to Build and Run

### Requirements
- NVIDIA GPU with Compute Capability ≥ 3.5 (Kepler or newer, supports CDP)
- CUDA Toolkit ≥ 12.x
- Make or Visual Studio (depending on OS)

### Compilation and Execution
Each subfolder contains the respective README files that specify how to compile and run each project.

## 📊 Results Summary
- **Mandelbrot:** CDP outperforms standard only at very high resolutions (> 12k × 12k), while for small inputs the overhead dominates.
- **N-Body:** Barnes–Hut with CDP achieves up to 182× speedup vs. Direct-Sum for large *N*.
- **Quadtree:** Iterative version generally faster, but CDP becomes competitive at deeper trees (≈ depth 8) or with few points per node.

## 📌 Conclusion
CDP is a powerful but specialized feature:
- It greatly simplifies recursive and hierarchical algorithms.
- It is most effective for irregular/adaptive workloads.
- For regular problems with predictable parallelism, iterative approaches remain more efficient.
