# processor

**Finite element computation engine for structural analysis**

## Overview

The Processor is the core computation module that solves linear elasticity problems using the finite element method. It reads mesh and problem definitions, assembles stiffness matrices, applies boundary conditions, and solves for displacement fields.

## Features

- Linear elasticity solver for 2D problems
- Multiple matrix solver implementations (full/banded)
- Node renumbering algorithms for performance optimization
- Support for triangular and quadrilateral elements
- Efficient sparse matrix operations

## Requirements

- [CMake](https://cmake.org/) (>= 3.10)
- Standard C compiler (GCC/Clang)

## Build Instructions

```bash
mkdir build
cd build
cmake ..
make
```

## Usage

```bash
./myFem [OPTIONS]
```

### Command Line Options

| Option | Description |
|--------|-------------|
| `-s`   | Use bridge without stay cables and pylon |
| `-u`   | Use U-shaped example mesh |
| `-b`   | Use beam mesh |
| `-t`   | Enable execution timing |
| `-a`   | Generate 50 animation frames (deformation) |
| `-x`   | Generate 50 animation frames (moving load) |
| `-h`   | Display help message |

## Solver Configuration

### Matrix Solver Types

Modify `typeSolver` in `main.c`:

```c
femSolverType typeSolver = FEM_FULL;   // Full Gaussian elimination
femSolverType typeSolver = FEM_BAND;   // Banded matrix solver
```

### Element Types

Set `elementType` in `main.c`:

```c
femElementType elementType = FEM_TRIANGLE;  // or FEM_QUAD
```

### Renumbering Strategies

Configure `renumType` in `main.c`:

```c
femRenumType renumType = FEM_NO;     // No renumbering
femRenumType renumType = FEM_XNUM;   // Sort by X coordinate
femRenumType renumType = FEM_YNUM;   // Sort by Y coordinate
femRenumType renumType = FEM_RCMK;   // Reverse Cuthill-McKee
```

**Recommended**: Use `FEM_RCMK` with `FEM_BAND` for optimal performance on large meshes.

## Input Files

Default paths (customizable in `main.c`):

- `../data/mesh.txt`: Mesh geometry and connectivity
- `../data/problem.txt`: Boundary conditions and loads

## Output Files

- `../data/UV.txt`: Displacement solution (U, V components)

## Performance Optimization

The RCM renumbering algorithm significantly reduces matrix bandwidth:

```bash
# Without renumbering
./myFem -t

# With RCM renumbering (faster)
./myFem -t  # (set renumType = FEM_RCMK in main.c)
```

Typical bandwidth reduction: 60-80% for complex geometries.

## Algorithm Details

### Solver Pipeline

1. **Mesh Import**: Read nodes and elements from `mesh.txt`
2. **Renumbering**: Optimize node ordering (optional)
3. **Assembly**: Build global stiffness matrix
4. **BC Application**: Apply displacement and force boundary conditions
5. **Solution**: Solve K·U = F using Gaussian elimination
6. **Export**: Write displacement field to `UV.txt`

### Supported Problem Types

- **Plane Stress**: Thin structures (plates, membranes)
- **Plane Strain**: Thick structures with constrained out-of-plane deformation
- **Axisymmetric**: Rotationally symmetric problems

## Example Workflow

```bash
# Solve beam bending problem with timing
./myFem -b -t

# Generate animation frames for bridge deformation
./myFem -a

# Solve with moving load animation
./myFem -x
```

## Troubleshooting

**Singular matrix error**: Check boundary conditions - system must be properly constrained.

**Memory issues**: Use banded solver (`FEM_BAND`) for large problems.

**Slow performance**: Enable RCM renumbering for bandwidth reduction.