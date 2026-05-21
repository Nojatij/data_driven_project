# Source Summary

## PDEBench paper

PDEBench is a benchmark for scientific machine learning on time-dependent PDE simulations. It provides datasets, generation code, baseline ML models and evaluation metrics. The relevant paper is:

https://arxiv.org/abs/2210.07182

Important points for this project:
- data-driven models are evaluated against numerical simulation ground truth;
- the benchmark includes 1D Advection and 1D Burgers;
- baseline models include FNO, U-Net and PINN;
- simple RMSE is not enough for PDE data, so nRMSE, max error, conserved quantities and Fourier-space errors are useful;
- the benchmark is designed for both forward prediction and inverse/identification style tasks.

## PDEBench GitHub

Repository:

https://github.com/pdebench/PDEBench

Important parts:
- `pdebench/data_download`: direct download and visualization utilities;
- `pdebench/data_download/pdebench_data_urls.csv`: exact data file URLs;
- `pdebench/models`: FNO, U-Net, PINN and metrics code;
- `pdebench/models/run_forward_1D.sh`: examples for 1D Advection/Burgers baseline runs;
- `pdebench/data_gen/notebooks/Analysis.ipynb`: example HDF5 inspection and plotting pattern.

## Dataset notes

DaRUS dataset:

https://darus.uni-stuttgart.de/dataset.xhtml?persistentId=doi:10.18419/darus-2986

The dataset uses HDF5. For the 1D Advection/Burgers files used here, the visualization code reads:
- `x-coordinate`;
- `tensor`, with sample/time/space/channel structure.

Recommended files:
- Burgers: `1D_Burgers_Sols_Nu0.01.hdf5`, direct URL `https://darus.uni-stuttgart.de/api/access/datafile/281363`;
- Advection: `1D_Advection_Sols_beta0.4.hdf5`, direct URL `https://darus.uni-stuttgart.de/api/access/datafile/255674`.

## Project interpretation

This is not just an ML benchmark reproduction. The course topic asks for data-driven methods:
- DMD is the dynamic prediction method;
- SINDy/PDE-FIND is the PDE identification method;
- PDEBench FNO/U-Net/PINN are comparison baselines.

The cleanest final story is:
1. Load and visualize PDEBench data.
2. Predict future dynamics with DMD.
3. Recover governing terms with SINDy/PDE-FIND.
4. Compare accuracy and runtime with a baseline.
5. Explain where DMD/SINDy work well and where they break.
