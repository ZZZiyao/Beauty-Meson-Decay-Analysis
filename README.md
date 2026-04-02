# Bs -> K*0 K*0bar Decay Analysis

A complete analysis pipeline for the decay **B_s^0 -> K\*^0 K\*^0bar -> K+ pi- K- pi+** using proton-proton collision data collected by the LHCb detector.

## Overview

This project implements the full signal extraction and spectroscopic analysis workflow:

1. **BDT Selection** -- Train an XGBoost classifier on topological features to separate signal from combinatorial background. Includes hyperparameter grid search, overtraining checks (KS tests), and efficiency-based figure-of-merit optimisation.
2. **Peaking Background Identification** -- Detect contributions from misidentified decays (Lambda_b -> p pi- K- pi+, B0 -> pi+ pi- K- pi+, etc.) via four-body mass-hypothesis swapping, and apply PID vetoes.
3. **Mass Fit** -- Perform an extended maximum-likelihood fit to the B_s invariant mass spectrum using Crystal Ball + Gaussian (signal), a fixed B0 component, Bernstein polynomial (combinatorial), and ARGUS convolved with Gaussian (partially reconstructed background).
4. **sWeights** -- Extract per-event signal weights from the mass fit for background-subtracted studies.
5. **Spectroscopy** -- Produce sWeighted intermediate resonance mass distributions (K*0, K*0bar), Dalitz plots, and 2-body/3-body mass spectra.

## Data

The analysis requires two ROOT files placed in `data/`. Download them from the LHCb open data portal:

```bash
cd data
wget https://mkenzie.web.cern.ch/mphil/assignment/2526/data.root
wget https://mkenzie.web.cern.ch/mphil/assignment/2526/mc.root
```

| File | Description |
|------|-------------|
| `data.root` | Real LHCb proton-proton collision data |
| `mc.root` | Signal Monte Carlo simulation |

A full description of the branch variables is provided in [`data/info.md`](data/info.md).

## Setup

Install dependencies:

```bash
pip install -r requirements.txt
```

## Running

Open and run `analysis.ipynb` from top to bottom. All intermediate results (plots, fit parameters, sWeights) are produced inline.

## Report

The full analysis write-up is available in [`Beauty_Meson_Decay_Analysis.pdf`](Beauty_Meson_Decay_Analysis.pdf).

