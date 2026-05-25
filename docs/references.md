# References and Notes

## Topic From The Project Spreadsheet

Project 12: "Data-driven method application for PDE identification and dynamic prediction using PDEBench data".

Key requirements from the project table:

- parse, process, and visualize PDEBench data;
- understand or reproduce the machine-learning benchmark logic for pretrained or baseline models;
- analyze spatiotemporal data using DMD or a DMD modification;
- apply SINDy or a SINDy modification to test whether the original PDE structure can be reconstructed;
- analyze DMD and SINDy reconstruction results;
- compare machine-learning and data-driven methods by accuracy and computational efficiency;
- conclude which factors improve system identification and reconstruction.

## Main Sources

- PDEBench GitHub: https://github.com/pdebench/PDEBench
- PDEBench paper: https://arxiv.org/abs/2210.07182
- PDEBench datasets, DaRUS: https://darus.uni-stuttgart.de/dataset.xhtml?persistentId=doi:10.18419/darus-2986
- Analysis notebook: https://github.com/pdebench/PDEBench/blob/main/pdebench/data_gen/notebooks/Analysis.ipynb
- Data download README: https://github.com/pdebench/PDEBench/blob/main/pdebench/data_download/README.md
- Data URL CSV: https://github.com/pdebench/PDEBench/blob/main/pdebench/data_download/pdebench_data_urls.csv
- 1D forward baseline runner: https://github.com/pdebench/PDEBench/blob/main/pdebench/models/run_forward_1D.sh
- Metrics implementation: https://github.com/pdebench/PDEBench/blob/main/pdebench/models/metrics.py

## PDEBench Paper Notes

- PDEBench is a benchmark suite for time-dependent PDE simulations.
- It provides data and code for comparing new data-driven or machine-learning models against numerical simulations and ML baselines.
- The benchmark includes several PDE families, including 1D Advection and 1D Burgers.
- Baseline models in the paper and repository include FNO, U-Net, PINN, and a gradient-based inverse method.
- Data are stored in HDF5 format, typically as `[b, t, x1, ..., xd, v]`, where `b` is the sample dimension, `t` is time, `x` are spatial dimensions, and `v` is the channel dimension.
- PDEBench metrics go beyond standard RMSE and include nRMSE, maximum error, boundary error, conserved-value error, and Fourier-space errors.

## GitHub Repository Notes

- The PDEBench repository contains data generation code, download utilities, visualization scripts, and baseline training/evaluation scripts.
- The relevant 1D Advection/Burgers code is under `data_gen_NLE`.
- Data can be downloaded through `download_direct.py` or by using direct DaRUS URLs.
- `run_forward_1D.sh` lists FNO, U-Net, and PINN commands for the 1D baseline tasks.
- The 1D Burgers/Advection visualization utilities use the HDF5 keys `x-coordinate` and `tensor`.

## Project Data

Main file:

- PDE: Burgers
- Filename: `1D_Burgers_Sols_Nu0.01.hdf5`
- URL: https://darus.uni-stuttgart.de/api/access/datafile/281363
- PDEBench path: `1D/Burgers/Train/`
- MD5: `e6d9a4f62baf9a29121a816b919e2770`

Secondary file:

- PDE: Advection
- Filename: `1D_Advection_Sols_beta0.4.hdf5`
- URL: https://darus.uni-stuttgart.de/api/access/datafile/255674
- PDEBench path: `1D/Advection/Train/`
- MD5: `d595bbfd2c659df995a93cd40d6ea568`

## Proposed Experimental Design

1. Start with Burgers `Nu0.01` as the main nonlinear case.
2. Use a manageable subset first, for example 20-100 samples depending on memory.
3. Split time into training and forecast intervals:
   - training: first 60-70% of time steps;
   - test: remaining 30-40% of time steps.
4. Compare:
   - naive persistence baseline;
   - DMD prediction;
   - SINDy/PDE-FIND identification and rollout;
   - a compact FNO-style machine-learning baseline.
5. Repeat the DMD/SINDy sanity check on Advection `beta=0.4`.

## Presentation Story

1. Problem: learn and identify dynamics from PDE-generated data.
2. Data: PDEBench, HDF5, Burgers, and Advection.
3. Methods: DMD for dynamic prediction and SINDy/PDE-FIND for equation identification.
4. Baselines and metrics: RMSE, nRMSE, MAE, MAPE, and compute time.
5. Results: plots, coefficient tables, and metrics table.
6. Conclusion: what works, what fails, why it happens, and how the workflow can be improved.
