# Adaptive Bayesian Radar Scheduling for Small-Debris Population Mapping

This repository contains the ordered analysis notebooks for a radar-calibrated study of adaptive observation planning for small orbital-debris populations. The workflow combines the 2018 EISCAT Tromsø campaign, historical catalog propagation, NASA ORDEM response calculations, an active-satellite catalog, and paired known-truth Bayesian simulations.

## Scientific scope

The real radar campaign is used to select and audit the detector, consolidate detections, test catalog association, estimate count variation, and constrain the observation model. ORDEM supplies the initial population shape and elevation-dependent response library. Adaptive-versus-baseline policy comparisons are then performed in simulated campaigns where the hidden debris population is known.

The repository does not claim that the historical radar was adaptively controlled, reconstruct individual fragment trajectories, or produce operational collision warnings. Independent Svalbard processing is a planned external detector check and is not represented as completed here.

## Notebook order

| Order | Notebook | Purpose |
|---:|---|---|
| 00 | `00_prepare_tromso_archives.ipynb` | Inventory and split the original radar bundles into verified hourly archives. |
| 01 | `01_run_tromso_gmf_pipeline.ipynb` | Run the pinned generalized matched-filter pipeline for the 24-hour campaign. |
| 02 | `02_benchmark_radar_detectors.ipynb` | Compare detector operating points with raw-data injections and real backgrounds. |
| 03 | `03_generate_initial_catalog_candidates.ipynb` | Generate historical-catalog candidates for each detected fragment. |
| 04 | `04_consolidate_radar_events.ipynb` | Merge consistent fragments into unique radar events. |
| 05 | `05_associate_catalog_objects.ipynb` | Reassociate consolidated events and run time-shift controls. |
| 06 | `06_ingest_ordem_prior.ipynb` | Verify the baseline ORDEM archive and create the initial altitude prior. |
| 07 | `07_build_ordem_pointing_library.ipynb` | Build and audit the initial elevation/azimuth response library. |
| 08 | `08_audit_active_satellite_exposure.ipynb` | Propagate active satellites and measure exposure by altitude shell. |
| 09 | `09_run_fine_grid_bayesian_experiment.ipynb` | Compare adaptive and baseline policies on the refined elevation grid. |
| 10 | `10_validate_response_and_catalog_model.ipynb` | Test response misspecification, Bayesian calibration, and catalog recovery. |
| 11 | `11_audit_detector_size_and_inference.ipynb` | Test size sensitivity, contamination assumptions, and posterior calibration. |
| 12 | `12_evaluate_service_aware_scheduling.ipynb` | Evaluate service-aware scheduling against unweighted adaptive scheduling. |
| 13 | `13_generate_methodology_mini_plots.ipynb` | Generate compact, data-backed plots for the methodology diagram. |

## Running the notebooks

Run Jupyter from the repository root. Every notebook resolves `PROJECT_ROOT` from either the root or the `notebooks` directory, so no personal Drive path is required.

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter lab
```

The large and access-controlled inputs are not committed. Collaborators should place authorized copies in the relative locations below before running the dependent stages.

```text
data/tromso/raw_download_bundles/
data/tromso/hourly_archives/
ordem_raw/
inputs/cswim_v1/
phase0_outputs/catalog_matching/historical_catalog/
```

Generated products are written beneath `processed/`, `phase0_outputs/`, `phase1_outputs/`, `phase2_outputs/`, and `phase3_outputs/`. These directories are ignored because they contain large intermediate or derived files.

## Reproducibility checks

Notebook outputs and execution counters are cleared for version control. The audit verifies that code cells contain no comments or docstrings, no restricted project label, no personal Colab/Drive paths, no embedded credential assignments, and no Python syntax errors. Run:

```bash
python tools/audit_notebooks.py
```

The machine-readable notebook order and audit results are in `audit/`.
