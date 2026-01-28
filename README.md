# FEM-Bridge-Simulator

<div align="center">

**A complete finite element analysis pipeline for bridge structural simulation**

[![C](https://img.shields.io/badge/language-C-blue.svg)](https://en.wikipedia.org/wiki/C_(programming_language))
[![Python](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![CMake](https://img.shields.io/badge/CMake-3.10+-064F8C.svg)](https://cmake.org/)
[![OpenGL](https://img.shields.io/badge/OpenGL-graphics-5586A4.svg)](https://www.opengl.org/)
[![Gmsh](https://img.shields.io/badge/Gmsh-4.12+-orange.svg)](https://gmsh.info/)

</div>

## Overview

FEM-Bridge-Simulator is an end-to-end finite element analysis (FEA) framework designed for simulating and visualizing structural behavior of bridges under various load conditions. The toolkit implements a complete FEM pipeline from mesh generation to real-time visualization, offering researchers and engineers a comprehensive tool for bridge structural analysis.

## Motivation

Understanding structural integrity is crucial in civil engineering, especially for complex structures like cable-stayed bridges. This project addresses the need for:

- **Accessible FEA Tools**: Providing an open-source alternative for educational and research purposes
- **Complete Pipeline**: Integrating preprocessing, solving, and postprocessing in a unified framework
- **Visual Insights**: Enabling real-time visualization of stress distributions and deformations
- **Performance Analysis**: Comparing different numerical methods and optimization strategies

## Key Features

- **Mesh Generation**: Interactive geometric modeling with Gmsh integration
- **Multiple Solvers**: Full and banded matrix solvers with various renumbering strategies
- **Real-time Visualization**: OpenGL-based rendering of displacement fields and stress distributions
- **Stress Analysis**: Von Mises stress, principal stresses (σxx, σyy, σxy)
- **Animation Support**: Time-based deformation and load movement visualization
- **Performance Optimization**: Reverse Cuthill-McKee (RCM) renumbering for bandwidth reduction

## Architecture

The toolkit is organized into three specialized modules:

```
FEM-Bridge-Simulator/
├── pre-processor/   # Mesh generation & problem definition
├── processor/      # FEM solver & computation engine
└── post-processor/  # Visualization & results analysis
```

### 1. PreProcessor

Generates computational meshes and defines boundary conditions:
- Interactive geometry creation using Gmsh
- Support for triangular and quadrilateral elements
- Plane stress, plane strain, and axisymmetric formulations
- Flexible boundary condition specification

### 2. Processor

Core FEM computation engine:
- Linear elasticity solver for structural analysis
- Multiple matrix solver implementations (full/banded)
- Node renumbering strategies (X/Y coordinate, RCM)
- Efficient sparse matrix operations

### 3. PostProcessor

Advanced visualization and analysis:
- Interactive 3D rendering with OpenGL
- Real-time stress field visualization
- Deformation animation capabilities
- Data export for external plotting (Python scripts included)

## Quick Start

### Prerequisites

```bash
# Required libraries
- CMake (>= 3.10)
- OpenGL
- GLFW
- Gmsh SDK
```

### Build & Run

```bash
# 1. PreProcessor - Generate mesh
cd pre-processor
mkdir build && cd build
cmake .. && make
./myFem

# 2. Processor - Solve FEM problem
cd ../../processor
mkdir build && cd build
cmake .. && make
./myFem

# 3. PostProcessor - Visualize results
cd ../../post-processor
mkdir build && cd build
cmake .. && make
./myFem
```

## Example Results

The toolkit can simulate various structural scenarios:

- **Cable-stayed Bridge**: Full bridge with pylons and stay cables
- **Simplified Bridge**: Basic deck structure for validation
- **Beam Analysis**: Classical beam bending with analytical comparison
- **Dynamic Loading**: Moving loads and time-dependent deformations

## Technical Details

### Solver Capabilities

- **Element Types**: 3-node triangles, 4-node quadrilaterals
- **Material Models**: Linear elastic (isotropic)
- **Problem Types**: Plane stress, plane strain, axisymmetric
- **Matrix Solvers**: Gaussian elimination (full/banded)

### Optimization Features

- **Node Renumbering**: Reduces matrix bandwidth for efficient solving
- **Sparse Storage**: Banded matrix format for memory efficiency
- **Parallel Visualization**: Non-blocking rendering pipeline

## Performance

The RCM renumbering algorithm typically reduces matrix bandwidth by 60-80%, significantly improving computational efficiency for large meshes.

## Documentation

Each module contains detailed README with:
- Build instructions
- Usage examples
- API documentation
- Configuration options

See module-specific READMEs in respective directories.

---

## Author

<div align="center">

<table>
  <tr>
    <td width="180" align="left">
      <img src="https://img.shields.io/badge/GitHub-mathisdelsart-black?logo=github" valign="middle"/>
    </td>
    <td align="left">
      <strong>Mathis DELSART</strong>
    </td>
  </tr>
  <tr>
    <td width="180" align="left">
      <img src="https://img.shields.io/badge/GitHub-beMang-black?logo=github" valign="middle"/>
    </td>
    <td align="left">
      <strong>Adrien ANTONUTTI</strong>
    </td>
  </tr>
</table>

</div>

## License

This project is developed for academic purposes as part of university coursework.

---

<div align="center">

**Built for LEPL1110 - Eléments finis @ UCLouvain** (Université catholique de Louvain).

*Built for structural engineering enthusiasts*

</div>