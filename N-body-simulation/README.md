# N-body-simulation

## About the Project

This project implements N-body simulations for both CPU and CUDA versions, using both the direct sum and Barnes-Hut algorithms. The simulations include spiral galaxy, random body initializations, galaxy collision, and our solar system.

[Blog](https://medium.com/@hsinhungw/optimizing-n-body-simulation-with-barnes-hut-algorithm-and-cuda-c76e78228c28)
[Paper](https://hsin-hung.github.io/N-body-simulation/report.pdf)

## Introduction

N-body simulation is a computational technique used in astrophysics to simulate the evolution of a system of particles, such as stars or galaxies, under the influence of gravitational forces. This project implements two different algorithms for N-body simulation: direct sum and Barnes-Hut. The direct sum algorithm is a simple but computationally expensive method that calculates the gravitational force between all pairs of particles. The Barnes-Hut algorithm is a more efficient method that uses a hierarchical tree structure to approximate the gravitational force between distant particles.

## Simulations

The project includes several N-body simulations, including:

* **[Spiral galaxy](https://youtu.be/Sap3lGzhlzE)**: Simulates a spiral galaxy over time.
* **Random body initializations**: Simulates a system of randomly initialized bodies and their interactions.
* **[Galaxy Collision](https://youtu.be/Krb5nEYRVaM)**: Simulates the collision of two galaxies and their resulting interactions.
* **Solar system**: Simulates the movement of the planets in our solar system (Sun, Mercury, Venus, Earth, Mars).

## Getting Started

To run the simulations, you will need an NVIDIA GPU with CUDA support for the CUDA version. Instructions for building and running the simulations are provided in the README.md file in each simulation directory. You can find them inside the `src` directory.