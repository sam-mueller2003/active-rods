# Active rods with HOOMD-blue

These notebooks introduce simulating active rods with [HOOMD-blue](https://hoomd-blue.readthedocs.io), starting from simple Brownian particles. Work through them in order.

## Setup

We'll help set this up. You need:

- A Python environment with `hoomd`, `gsd`, `numpy`, `matplotlib` and `freud`
- Jupyter (VS Code or JupyterLab)
- [OVITO](https://www.ovito.org) to view trajectories (`.gsd` files)

Check HOOMD works:

```python
import hoomd
print(hoomd.version.version, hoomd.version.gpu_enabled)
```

If you have no GPU, replace `hoomd.device.GPU()` with `hoomd.device.CPU()` in each notebook.

## The notebooks

1. **`simple_hoomd.ipynb`:** Brownian particles. Background on MD, Brownian dynamics and active Brownian particles, then 100 Lennard-Jones particles in a 2D box. Covers the basic HOOMD workflow.
2. **`rod.ipynb`:** passive rods. Each rod is a rigid chain of beads with a head bead `H`, starting on a lattice at area fraction `phi`. Covers rigid bodies and rotation.
3. **`active_rods.ipynb`:** active rods. The head bead pushes each rod along its axis with force `F0`, and the swimming direction diffuses with rate `D_r`. This is where the project starts.

## Running them

- Use "Restart" then "Run All" after changing anything. Running cells twice continues the old simulation.
- Each notebook overwrites its own `.gsd` files, so rename any you want to keep.
- Units are reduced: lengths in bead diameters $\sigma$, energies in $k_BT$, time in $\tau = \gamma\sigma^2/k_BT$.

## Looking at the results

- Open the `_trajectory.gsd` file in OVITO. For rods, colour by particle type and hide type `R` (the rod centres).
- In Python, read frames with `gsd.hoomd.open(filename)` and analyse them with `freud`.

## Simplifications

- The drag is the same in every direction, but real rods slide about twice as easily along their length.
- There are no hydrodynamic interactions.
- The rods start lined up on a lattice, so let them forget it before measuring anything.
