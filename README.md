[![CI](https://github.com/cmaurini/nonlinear-elastica/actions/workflows/ci.yml/badge.svg)](https://github.com/cmaurini/nonlinear-elastica/actions/workflows/ci.yml)
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/cmaurini/nonlinear-elastica/HEAD?labpath=elastica_buckling_casadi.ipynb)

# Nonlinear Beam Model: Elastica

Numerical solution of the nonlinear model of an inextensible, unshearable planar beam (Euler elastica), clamped at one end and loaded at the other.
Two notebooks solve the same problems with two tools: they compute the large deflection of a cantilever under a transverse tip load, and its buckling and post-buckling under an axial compressive load, up to the boundary layer that forms at the clamp at large loads.

## Contents

- `elastica_buckling_casadi.ipynb`, the version used in the course: the energy in the position $\underline{x}(s)$ and the angle $\theta(s)$, finite differences, the inextensibility constraint imposed at each node, symbolic derivatives with [CasADi](https://web.casadi.org/) and constrained minimization with [IPOPT](https://coin-or.github.io/Ipopt/).
- `elastica_buckling_fenicsx.ipynb`: the energy in the angle alone, after eliminating the position, solved with [FEniCSx](https://fenicsproject.org) (dolfinx 0.11): P2 finite elements, residual and Jacobian derived from the energy by UFL, Newton's method (PETSc SNES).

Both notebooks contain:

- Vertical tip load, compared with linear beam theory.
- Critical load of the clamped-free beam, $\pi^2 EI/4L^2$ (computed from the eigenvalues of the second variation with SLEPc in the FEniCSx version).
- Axial compression with a natural-curvature imperfection $k_0$, up to $50\,F_{\text{crit}}$: bifurcation diagram, and boundary layer of width $\sqrt{EI/P}$ compared with the separatrix $\theta = \pi - 4\arctan(e^{-s/\ell})$.
- An exercise: buckling of a vertical beam under its own weight.

## Mathematical model

In the FEniCSx version, the beam minimizes the potential energy

$$
\mathcal{E}(\theta) = \int_0^L \Big[\frac{EI}{2}\big(\theta' - k_0\big)^2 - F_x\cos\theta - F_y\sin\theta\Big]\,ds, \qquad \theta(0) = 0,
$$

obtained from the bending energy and the work of the tip load $(F_x, F_y)$ by eliminating the position with the inextensibility constraint $\underline{x}' = \cos\theta\,\underline{e}_1 + \sin\theta\,\underline{e}_2$.

## Running the notebook

Online: click the Binder badge above. The first start after a push can take several minutes while mybinder.org builds the image; the CI triggers this build on every push to `main`.

Locally, with conda:

```bash
conda env create -f environment.yml
conda activate elastica
jupyter lab
```

## Files

- `elastica_buckling_casadi.ipynb`: CasADi version (course)
- `elastica_buckling_fenicsx.ipynb`: FEniCSx version
- `environment.yml`: full conda environment for both notebooks, used by the CI
- `.binder/environment.yml`: lightweight environment for the CasADi notebook opened by the Binder badge
- `.github/workflows/ci.yml`: executes both notebooks in the conda environment, then prebuilds the Binder image
