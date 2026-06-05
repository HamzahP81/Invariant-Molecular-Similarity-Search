# Invariant-Based Molecular Similarity Search

An alignment-free molecular similarity search system for PubChem conformers, 
built on isometry invariants (SRD and SPD) with empirical Lipschitz continuity 
validation and a fully interactive browser-based molecular map. Explore 1,223 conformers across 250 unique molecules plotted in invariant space. Switch between eight geometric axis configurations, search by molecule name or formula, upload any PubChem molecule by name in real time or run a nearest-neighbour search to find structurally similar compounds.

## Overview

Standard molecular similarity search relies on RMSD, which requires explicit 
molecular alignment and is undefined for molecules of different sizes. This project 
addresses those limitations by developing and validating an approach based on 
geometric invariants which are mathematical descriptors unchanged under any combination of translation, rotation and reflection.

**Key results:**
- 82.7% average search space reduction via a two-stage KDTree filtration pipeline 
  across 1,223 PubChem conformers (maximum 95.0% in the 33-atom group)
- Lipschitz continuity validated empirically for both invariants using the L-infinity 
  norm across 50 molecules and 7 perturbation magnitudes  
  (K ≈ 1.045 for SRD, K ≈ 1.592 for SPD)
- Moderate positive Pearson correlation (r = 0.502) between SPD distance and RMSD 
  across 11 atom-count-matched molecular pairs
- Interactive molecular map with 8 configurable geometric axes, 3 colour modes, 
  real-time molecule upload, and nearest-neighbour search — all browser-side,  
  no server required

## Repository Structure
├── main.py              # Single reproducible pipeline script
├── index.html           # Standalone interactive visualisation (hosted above)
├── dissertation.pdf     # Full technical write-up
├── molecules/           # SDF files for all downloaded conformers
└── conformers.db        # SQLite database of computed invariants

## Technical Stack

Python 3.11 · RDKit · NumPy · pandas · scipy (KDTree) · Plotly · SQLite ·  
HTML/JavaScript (browser-side SRD computation, real-time PubChem API integration,  
nearest-neighbour search)

## Background

Final-year BSc dissertation at the University of Liverpool, supervised by  
Dr Vitaliy Kurlin (Geometric Data Science group). The project extends prior work  
by Chatterjee (2025) which demonstrated invariant-based filtration at production  
scale on the BARKLA HPC cluster. It added full interactivity, empirical Lipschitz  
validation of SRD and SPD (conducted here for the first time) and external  
validation against RMSD.

A continuation toward publication is under discussion with researchers at the  
Materials Innovation Factory, University of Liverpool.

## Running the Pipeline

```bash
pip install rdkit numpy pandas scipy plotly
python main.py
```
The script fetches conformers from PubChem, computes invariants, runs filtration,  
generates the interactive map, and outputs Lipschitz and RMSD validation results.  
If the `molecules/` directory is already populated, the download stage is skipped.

## Citation
Patel, H. (2026). *Invariant-Based Molecular Similarity Search: An Interactive Map  
and Empirical Validation of Geometric Descriptors for PubChem Conformers*.  
BSc Dissertation, University of Liverpool.
