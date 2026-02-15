# Bifurcation-Potential-Fields
Matlab scripts for creating the Bifurcation Potential Fields in the Physica D - Nonlinear Phenomena paper, "Bifurcation Potential Fields for Resilience Analysis of Dynamical Systems"

# VB Fields and Bifurcation Overlays

This repository contains MATLAB code and bifurcation data used to reproduce the **VB (resilience) fields** and **bifurcation boundary overlays** presented in Bifurcation Potential Fields for Resilience Analysis in Dynamical Systems, published in  Physica D Nonlinear Phenomena.

The code implements a unified workflow across **six canonical models**, combining:
- parameter–space sweeps to compute VB fields, and  
- bifurcation curves generated using **MatCont**, overlaid directly onto the VB fields.

---

## Contents

The repository is organized by model, with shared utilities:

Bifurcation Potential Fields/
│
├── README.md
├── utilities/
│
├── SN/ (unfolded saddle-node)
├── CUSP/ (unfolded cusp)
├── DW/ (double-well potential)
├── DUFF/ (forced Duffing oscillator)
├── SBW/ (SBW model)
└── IGP/ (IGP model)


Each model directory contains:
- MATLAB scripts to compute the VB field,
- equilibrium-finding and classification routines,
- a `mats/` folder containing MatCont-generated bifurcation data (`*.mat`),
- a `figs/` folder for generated figures,
- a model-specific `overlay_config.m` file.

---

## What this repository provides

For each model, the repository allows a reader to:

1. **Reproduce the VB field**  
   by running the model’s `*_make_vb.m` script over the parameter ranges used in the paper.

2. **Overlay bifurcation boundaries**  
   after confirming the corresponding MatCont output files (`*.mat`) exist in the model’s `mats/` folder run:
   ```matlab
   overlayBifurcationBoundary(args)
   ```
See the model-specific README for usage (e.g., details about args).

The resulting composite figure (VB field + bifurcation curve) is saved automatically to the model’s figs/ directory.

Each model’s folder is self-contained and documents (via code and configuration) which parameters are swept and how the VB metric is defined.

What this repository does not provide

-Step-by-step instructions for generating bifurcation curves in MatCont’s GUI.
(MatCont is a mature, well-documented package; we assume basic familiarity. See the MatCont documentation and tutorials by its authors.)

-A general-purpose MatCont scripting interface.

Instead, we provide the actual MatCont output files used for the figures, together with a reproducible overlay mechanism.

This choice reflects the workflow used in the published work and ensures fidelity to the figures as presented.

Reproducing a figure (typical workflow)

For a given model (e.g. unfolded saddle-node, SN/):

1. Run the VB field script, e.g.

sn_make_vb("high","a",[-1.5 0.5],"b",[-0.5 1.5],[50 50]);  % 50x50 grid, fast for testing, coarse resolution, 350x350 grid, slow for publication, high resolution

2. Ensure the appropriate MatCont curve files (e.g. LP_LP(1).mat, LP_LP(2).mat) are present in:

SN/mats/

3. With the VB field figure open, run:

overlayBifurcationBoundary(args)

4. The composite figure is saved automatically to:

SN/figs/

MATLAB version and dependencies

MATLAB (tested on recent versions; no toolboxes required).

MatCont (used to generate bifurcation curves).  The bifurcation curves overlaid on VB fields were generated using MatCont, a MATLAB software package for numerical continuation and bifurcation analysis of dynamical systems. MatCont can be downloaded from:
https://sourceforge.net/projects/matcont/

Citation and future archival version

This repository is provided to satisfy reproducibility requests during peer review.

A longer-term, archival version (with a stable DOI, e.g. via Zenodo) may be created after publication.
If so, this README will be updated with the corresponding citation information.

Contact

For questions related to the code or its use in reproducing published figures, please contact the corresponding author.


