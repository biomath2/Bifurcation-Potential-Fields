# Intraguild Predation Model (IGP)

This directory contains MATLAB scripts for generating VB (Bifurcation Potential / resilience) fields for the Intraguild Predation (IGP) model, together with tools for overlaying bifurcation curves computed in MatCont.  

The IGP model is an ecological system in which species compete and prey upon one another simultaneously. It exhibits bistability and fold bifurcations in parameter space, providing a higher-dimensional ecological analogue of the normal forms studied elsewhere in this repository.  The model was first introduced in K. L. S. Drury, D. M. Lodge, Using mean first passage times to quantify equilibrium resilience in perturbed intraguild predation systems, Theoretical Ecology 2 (1) (2009) 41–55. doi:10.1007/s12080-008-0027-z.

---

## 1. Model

The intraguild predation model describes interactions among:

- An prey that competes with its predator for a shared resource
- A predator that competes with its prey for a shared resource 

(See the manuscript for the exact functional forms used.)

Under appropriate parameter regimes, the system admits:

- A low-predator equilibrium
- A high-predator equilibrium
- A saddle equilibrium separating the basins

This structure produces bistability wedges in parameter space.

---

## 2. Parameter Plane

The VB field is computed in a selected two-parameter plane.

In the paper, the parameter pair varied was:

- **Horizontal axis:** predator suppression of prey population growth via competition, \beta  
- **Vertical axis:** (e.g.) prey suppression of predator population growth via competition, \alpha
 
\alpha \in [0 1], \beta \in [0 1]

Typical grid resolution:

```
exploratory: 50 x 50
publication quality: 350 × 350
```

---

## 3. Definition of the VB Metric

Because the IGP model is two-dimensional, equilibria are points in \((x,y)\)-space.

At each parameter value, the VB metric is defined as:

> The Euclidean distance between a selected stable equilibrium and its bounding saddle equilibrium in phase space.

\[
VB = \| \mathbf{x}_{stable} - \mathbf{x}_{saddle} \|
\]

This generalizes the one-dimensional saddle distance used in SN, CUSP, DW, and SBW.

---

## 4. Generating the VB Field

From within the `IGP/` directory, run:

```matlab
igp_make_vb("high","b",[min1 max1],"a",[min2 max2],[350 350]);
```

This generates:

- Raw VB data in `mats/`
- A VB field figure in `figs/`

Smaller grids may be used for testing.

---

## 5. Overlaying Bifurcation Boundaries

Bifurcation curves are computed in **MatCont**.

MatCont project page:

https://sourceforge.net/projects/matcont/

After computing fold (limit point) curves:

1. Copy the resulting `.mat` files into:

```
IGP/mats/
```

The curves used in the paper are already in the mats directory.

2. Open the VB field figure.

3. Run:

```matlab
overlayBifurcationBoundary
```

The script:

- Loads curve files specified in `overlay_config.m`
- Uses configured parameter-row mapping
- Overlays the bifurcation boundary
- Saves the composite figure to:

```
IGP/figs/
```

---

## 6. Interpretation

The IGP model illustrates several important themes:

- Bistability persists in higher-dimensional ecological systems.
- Fold bifurcations delimit parameter regions where coexistence states exist.
- Basin geometry can shift substantially within the bistable region.
- Stability margins are not determined solely by proximity to the bifurcation boundary.

As parameters approach the fold curve:

- A stable equilibrium collides with a saddle.
- The VB metric approaches zero.
- The ecological state becomes increasingly fragile to perturbation.

This model connects abstract bifurcation geometry to multi-species ecological interactions.

---

## 7. Directory Structure

```
IGP/
│
├── igp_make_vb.m
├── find_real_eqa_igp.m
├── classify_equilibria_igp.m
├── overlayBifurcationBoundary.m
├── overlay_config.m
│
├── mats/
└── figs/
```

---

## 8. Reproducibility Checklist

To reproduce the composite figure:

1. Generate the VB field (350×350 grid).
2. Compute fold curves in MatCont.
3. Copy `.mat` files into `mats/`.
4. Run `overlayBifurcationBoundary`.

The resulting composite figure matches the one presented in the manuscript.

---
