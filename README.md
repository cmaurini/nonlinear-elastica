# 🧰 Nonlinear Elastica Beam

This repository demonstrates nonlinear deformation and buckling of an inextensible, unshearable planar beam under external loading.

## 📘 Features

- Symbolic formulation with [CasADi](https://web.casadi.org/)
- Constrained optimization using [IPOPT](https://coin-or.github.io/Ipopt/)
- Two examples:
  - Vertical tip load without imperfection
  - Axial compression with initial curvature imperfection

## 🧠 Mathematical Model

The beam minimizes the energy:

- Bending energy with inelastic curvature `k0`
- Work of vertical and axial tip forces

Inextensibility is enforced via nonlinear constraints on the tangent vector.

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
