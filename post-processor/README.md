# post-processor

**Real-time visualization and analysis module for finite element results**

## Overview

The PostProcessor provides interactive 3D visualization of finite element analysis results. It renders mesh geometry, displacement fields, and stress distributions using OpenGL, offering real-time exploration of structural behavior.

## Features

- Interactive 3D mesh rendering with OpenGL
- Displacement field visualization with configurable scaling
- Stress component visualization (σxx, σyy, σxy, von Mises)
- Animation support for time-dependent simulations
- Color-mapped contour plots
- Data export for external plotting (Python scripts included)

## Requirements

- [CMake](https://cmake.org/) (>= 3.10)
- [OpenGL](https://www.opengl.org/)
- [GLFW](https://www.glfw.org/)
- [Python 3](https://www.python.org/) (for plotting scripts)

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
| `-r`   | Disable result visualizer |
| `-p`   | Disable plot generation |
| `-a`   | Enable animation mode |
| `-u`   | Load U-shaped example |
| `-b`   | Load beam example |
| `-s`   | Load simplified bridge example |
| `-h`   | Display help message |

## Interactive Keyboard Controls

### View Modes

| Key | Function |
|-----|----------|
| `V` | Mesh and displacement magnitude |
| `D` | Domain/material visualization |
| `N` | Highlight next domain |

### Stress Visualization

| Key | Component |
|-----|-----------|
| `U` | σxx (Normal stress X) |
| `I` | σyy (Normal stress Y) |
| `O` | σxy (Shear stress) |
| `P` | Von Mises stress |

### Force Display

| Key | Function |
|-----|----------|
| `X` | Show horizontal forces |
| `Y` | Show vertical forces |
| `S` | Display stiffness matrix |

## Configuration

### Solver Settings

Modify in `main.c`:

```c
femSolverType typeSolver = FEM_FULL;   // or FEM_BAND
femRenumType renumType = FEM_RCMK;     // Renumbering strategy
```

### Animation

Enable with `-a` flag or set in code:

```c
int enableAnimation = 1;  // 0 for static visualization
```

## Python Plotting Scripts

Located in `src/`:

### beam_plot.py

Compares FEM results with analytical solution for beam bending:

```bash
python src/beam_plot.py
```

Plots displacement at beam midpoint vs. analytical curve.

### constrains_plot.py

Visualizes constraint forces on the complete bridge structure:

```bash
python src/constrains_plot.py
```

Displays reaction forces at support points.

### convergence_plot.py

Analyzes mesh convergence for the beam example:

```bash
python src/convergence_plot.py
```

Shows error vs. mesh refinement level.

### solver_plot.py

Performance comparison of different solver configurations:

```bash
python src/solver_plot.py
```

Compares execution time and accuracy for various renumbering strategies.

## Input Files

Expected in `../data/`:

- `mesh.txt`: Mesh geometry
- `problem.txt`: Boundary conditions
- `UV.txt`: Displacement solution

## Visualization Features

### Color Mapping

Results are color-mapped from blue (minimum) to red (maximum) for intuitive interpretation.

### Displacement Scaling

Deformations are scaled for visibility. Adjust in the UI or modify:

```c
double scaleFactor = 10.0;  // In visualization code
```

### Animation

Frame-by-frame playback of time-dependent results. Use arrow keys to control:

- **Right Arrow**: Next frame
- **Left Arrow**: Previous frame
- **Space**: Play/Pause

## Example Workflows

### Visualize Beam Results

```bash
# Generate and view beam analysis
./myFem -b
# Press 'V' for displacement, 'P' for von Mises stress
```

### Create Convergence Study

```bash
# Run processor with different mesh sizes
cd ../processor
./myFem -b -t  # Multiple times with varying mesh density

# Analyze convergence
cd ../post-processor
python src/convergence_plot.py
```

### Animate Bridge Deformation

```bash
# Generate animation frames in Processor
cd ../processor
./myFem -a

# Visualize animation
cd ../post-processor
./myFem -a
```

## Performance Tips

- Use banded solver (`FEM_BAND`) for large meshes
- Enable RCM renumbering for faster computation
- Disable plots (`-p`) for faster iteration

## Troubleshooting

**OpenGL errors**: Ensure graphics drivers are up to date.

**Missing results**: Check that `UV.txt` exists in `../data/`.

**Slow rendering**: Reduce mesh density or disable animation.

# plot.py

Plot the results of a structure with various parameters. Check the help message for more information.