# Cusp Normal Form (CUSP)

This directory contains MATLAB scripts for generating the VB (Bifurcation Potential / resilience) fields associated with the **cusp normal form**, together with tools for overlaying bifurcation curves generated in MatCont.

The scripts reproduce the cusp VB fields presented in the Physica D paper:

> *“Bifurcation Potential Fields for Resilience Analysis of Dynamical Systems”*

---

## 1. Model

We consider the cusp normal form:

\[
\dot{x} = \alpha + \beta x + x^3 + g x^2
\]

In the paper, we use:

```
g = 1
```

The bifurcation structure in the \((\alpha, \beta)\) plane produces the classical cusp-shaped bistability wedge.

Within this wedge, the system possesses:

- Two stable equilibria  
- One saddle equilibrium  

The VB field measures the Euclidean distance between a selected stable equilibrium (low or high branch) and its bounding saddle.

---

## 2. Generating the VB Field

From within the `CUSP/` directory, run:

```matlab
cusp_make_vb("high","beta",[-0.5 1.5],"alpha",[-1.5 0.5],[350 350]);
```

or

```matlab
cusp_make_vb("low","beta",[-0.5 1.5],"alpha",[-1.5 0.5],[350 350]);
```
Note: in both the "high" and "low" cases, the final argument [350 350] generates a smooth publication grade VB field. Generating figures with this resolution can take hours to finish, however.  In exploratory work, it is often sufficient to use [50 50], which completes much more quickly.  
### Parameters Used in the Paper

```
beta  ∈ [-0.5, 1.5]
alpha ∈ [-1.5, 0.5]
g = 1
grid = 350 × 350
```

### Output

Running the script generates:

- Raw VB data in `mats/`
- A figure in `figs/`

---

## 3. Overlaying Bifurcation Boundaries

Bifurcation curves must first be generated in **MatCont**.

Recommended MatCont resource:

https://sourceforge.net/projects/matcont/

After computing the fold (limit point) curves in MatCont:

1. Copy the resulting `LP_LP(1).mat`, `LP_LP(2).mat` files into:

```
CUSP/mats/
```

2. Open the VB field figure in MATLAB.

3. Run:

```matlab
overlayBifurcationBoundary
```

The script automatically:

- Loads the appropriate curve files (as specified in `overlay_config.m`)
- Uses the configured MatCont parameter row mapping
- Overlays the bifurcation boundaries
- Saves the composite figure to:

```
CUSP/figs/
```

No manual copy-paste from MatCont is required.

---

## 4. Interpretation

Inside the cusp wedge:

- Two stable equilibria coexist.
- The VB field quantifies the geometric separation between a selected attractor and the intervening saddle.

As parameters vary, the wedge skews due to the quadratic term \( g x^2 \), introducing asymmetry relative to the classical symmetric cusp (g = 0).

The VB field therefore reflects:

- The shifting saddle location
- The geometry of bistability
- The resilience structure relative to the chosen equilibrium branch

---

## 5. Directory Structure

```
CUSP/
│
├── cusp_make_vb.m
├── cusp_vb_distance_at_params.m
├── find_real_eqa_cusp.m
├── classify_equilibria_cusp.m
├── overlayBifurcationBoundary.m
├── overlay_config.m
│
├── mats/
└── figs/
```

---

## 6. Notes

- The overlay script assumes MatCont-generated `.mat` files containing variable `x`.
- Parameter row mappings are defined in `overlay_config.m`.
- The VB field and bifurcation curves are kept modular by design.
- This directory is self-contained and does not depend on other model folders.

---

## 7. Reproducibility

To reproduce the composite figure:

1. Generate the VB field (350×350 grid).
2. Generate cusp fold curves in MatCont.
3. Copy the MatCont `.mat` files into `mats/`.
4. Run `overlayBifurcationBoundary`.

The resulting composite figure will match the one shown in the paper.

---
