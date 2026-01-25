# pre-processor

**Mesh generation and problem definition module for finite element analysis**

## Overview

The PreProcessor is responsible for creating computational meshes and defining boundary conditions for structural analysis problems. It provides an interactive interface for geometric modeling and mesh generation using the Gmsh library.

## Features

- Interactive geometry creation and manipulation
- Triangle and quadrilateral mesh generation
- Multiple problem formulations (plane stress, plane strain, axisymmetric)
- Visual mesh preview with OpenGL
- Export to standardized mesh format

## Requirements

- [CMake](https://cmake.org/) (>= 3.10)
- [Gmsh SDK](https://gmsh.info/) (>= 4.12)
- [OpenGL](https://www.opengl.org/)
- [GLFW](https://www.glfw.org/)

## Build Instructions

```bash
mkdir build
cd build
cmake ..
make
```

**Note**: Ensure the Gmsh SDK path is correctly configured in `CMakeLists.txt`.

## Usage

```bash
./myFem [OPTIONS]
```

### Command Line Options

| Option | Description |
|--------|-------------|
| `-m`   | Disable mesh visualizer |
| `-s`   | Generate bridge without stay cables and pylon |
| `-u`   | Generate U-shaped example mesh |
| `-b`   | Generate beam mesh |
| `-h`   | Display help message |

## Configuration

### Element Types

Modify the `elementType` variable in `main.c`:

```c
femElementType elementType = FEM_TRIANGLE;  // or FEM_QUAD
```

### Problem Formulations

Set the `theCase` variable in `main.c`:

```c
femProblemCase theCase = PLANAR_STRESS;  // PLANAR_STRAIN, AXISYM
```

## Output Files

- `mesh.txt`: Node coordinates and element connectivity
- `problem.txt`: Boundary conditions and material properties

## Default Behavior

Without arguments, the program generates a complete cable-stayed bridge geometry with plane stress formulation.

## Interactive Controls

When the visualizer is enabled:
- **Rotate**: Mouse drag
- **Zoom**: Mouse wheel
- **Pan**: Shift + Mouse drag

## Example

Generate a simple beam mesh:

```bash
./myFem -b
```

This creates mesh and problem files in the configured output directory.