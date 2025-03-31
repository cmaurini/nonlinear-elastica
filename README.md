[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/cmaurini/nonlinear-elastica/HEAD)
[![Open in Codespaces](https://github.com/codespaces/badge.svg)](https://github.com/codespaces/new/?repo=cmaurini/nonlinear-elastica)


# Nonlinear Beam Model: Elastica

This repository demonstrates the numerical solution of a nonlinear models inextensible, unshearable planar beam under external loading.
It illustrates the deformation of a cnatilever beam under a transverse tip load and its bukling under a compressive axial force


## Features

- Symbolic formulation with [CasADi](https://web.casadi.org/)
- Constrained optimization using [IPOPT](https://coin-or.github.io/Ipopt/)
- Two examples:
  - Vertical tip load without imperfection
  - Axial compression with initial curvature imperfection

## Mathematical Model

The beam minimizes the energy:

- Bending energy with inelastic curvature
- Work of vertical and axial tip forces

Inextensibility is enforced via nonlinear constraints between the orientation of the tangent vector and the derivative of the position vector.

## 📦 Installation

Install using conda:

```bash
conda env create -f environment.yml
conda activate elastica
jupyter notebook
```

## 📁 Files

- `elastica_buckling.ipynb`: Main notebook with simulations and plots
- `environment.yml`: Conda environment
