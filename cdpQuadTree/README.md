# cdpQuadTree

This project contains two implementations of a **quadtree construction algorithm** designed to evaluate the impact of **CUDA Dynamic Parallelism (CDP)**.

- **Iterative version (`quadtree.cu`)**  
  Implements quadtree construction using a **loop of kernel launches** through the levels of the quadtree.
  This version does not rely on CDP and highlights the efficiency of a flat parallel approach.

- **CDP version (`cdpQuadtree.cu`)**  
  Implements the same algorithm but uses **recursive kernel launches** enabled by CDP.
  Each node dynamically spawns a child kernel for its quadrants, expressing the algorithm more naturally but incurring device-side launch overhead.

## Purpose
The two implementations allow a **direct comparison** between:
- The same algorithm expressed in a **traditional iterative style**.
- The **recursive CDP style**, which can simplify code structure but may introduce runtime costs.

This benchmark isolates the effect of **device-side kernel launches** on performance, since both versions solve the exact same problem with identical logic.
  
## Building
In the Visual Studio x64 Native Tools Command Prompt

Iterative:
```shell
cd src\quadtree
nvcc -O3 -arch=sm_80 -std c++17 -I ../../common/inc -o quadtree.exe quadtree.cu
.\quadtree.exe
```

CDP:
```shell
cd src\cdpQuadtree
nvcc -O3 -arch=sm_80 -rdc=true -std c++17 -I ../../common/inc -o cdpQuadtree.exe cdpQuadtree.cu
.\cdpQuadtree.exe
```

To modify the algorithm's execution parameters, in both cases you need to modify the three constants at the beginning of the cdpQuadtree function:
- **num_points:** the number of point to be generated
- **max_depth:** the maximum depth of the quadtree
- **min_points_per_node:** number of points below which a node is considered a leaf

## Debugging
```shell
nvcc -G -g -lineinfo -rdc=true --std c++17 -I ../../common/inc cdpQuadtree.cu -o quadtree_dbg
compute-sanitizer --tool memcheck .\quadtree_dbg
```

## Attribution

The CDP implementation was taken from [Nvidia](https://developer.download.nvidia.com/compute/DevZone/C/html_x64/samples.html).