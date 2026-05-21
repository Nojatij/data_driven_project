# Project 12: PDEBench PDE Identification and Dynamic Prediction

Course project for applying data-driven methods to PDEBench data.

The project focuses on two 1D PDEBench datasets:

- 1D Burgers equation, `nu = 0.01`
- 1D Advection equation, `beta = 0.4`

The main notebook is prepared for Kaggle and can be run from top to bottom.

## Main Notebook

Open this notebook on Kaggle:

```text
notebooks/PDEBench_DMD_SINDy_Kaggle.ipynb
```

Recommended Kaggle settings:

- Accelerator: GPU, for example T4 or P100
- Internet: On, unless the HDF5 files are uploaded as a Kaggle Dataset
- Python notebook environment

The notebook automatically searches for data in:

- `/kaggle/input`
- `/kaggle/working/data`

If data is missing and internet is enabled, it downloads the required files from DaRUS.

## What The Notebook Does

The notebook covers the full project workflow:

1. Downloads or finds PDEBench HDF5 files.
2. Reads `tensor`, `x-coordinate`, and time coordinates.
3. Builds a manageable subset for Kaggle execution.
4. Visualizes `u(x,t)` and time slices.
5. Applies Dynamic Mode Decomposition (DMD) for future-state prediction.
6. Applies PDE-FIND / SINDy for sparse PDE identification.
7. Trains a compact FNO-style neural baseline on GPU.
8. Compares all methods using accuracy and runtime metrics.
9. Exports plots, metric tables, coefficient tables, and a short summary.

## Methods

### DMD

DMD fits a low-rank linear evolution operator:

```text
u_{k+1} ~= A u_k
```

It is fast, interpretable at the modal level, and useful as a classical data-driven baseline.

### PDE-FIND / SINDy

PDE-FIND identifies a sparse equation from candidate terms such as:

```text
u, u_x, u_xx, u_xxx, u*u_x, u*u_xx
```

Expected structures:

- Advection: `u_t = - beta u_x`
- Burgers: `u_t = - u u_x + nu u_xx`

### FNO-style Neural Baseline

The notebook includes a compact Fourier Neural Operator style model:

- spectral convolution in Fourier space;
- one-step autoregressive training;
- rollout over the test interval;
- GPU acceleration on Kaggle.

This satisfies the machine-learning baseline requirement without requiring the full official PDEBench training pipeline.

## Metrics

The notebook reports:

- RMSE
- normalized RMSE
- max error
- boundary RMSE
- conserved-value RMSE
- Fourier low/mid/high frequency errors
- training or fitting time

Exported metric table:

```text
/kaggle/working/results/metrics_table.csv
```

## Output Artifacts

After running the notebook, Kaggle writes results to:

```text
/kaggle/working/results
```

Important files:

- `metrics_table.csv`: comparison of all methods
- `pdefind_coefficients.csv`: identified PDE coefficients
- `final_summary.md`: short report draft
- `figures/*_overview.png`: dataset visualizations
- `figures/*_prediction_comparison.png`: truth vs predictions
- `figures/*_error_over_time.png`: forecast error curves
- `figures/*_fno_loss.png`: neural baseline training curves

## Data

The project uses files from PDEBench / DaRUS.

Main file:

```text
1D_Burgers_Sols_Nu0.01.hdf5
https://darus.uni-stuttgart.de/api/access/datafile/281363
```

Secondary file:

```text
1D_Advection_Sols_beta0.4.hdf5
https://darus.uni-stuttgart.de/api/access/datafile/255674
```

The HDF5 files are large and are intentionally ignored by git.

## Repository Structure

```text
Project_12_PDEBench/
  README.md
  requirements.txt
  notebooks/
    PDEBench_DMD_SINDy_Kaggle.ipynb
  data/
    README.md
  docs/
    references.md
    source_summary.md
    task_board.md
    roles.md
  results/
  src/
  presentation/
```

## How To Run On Kaggle

1. Create a new Kaggle notebook.
2. Upload `notebooks/PDEBench_DMD_SINDy_Kaggle.ipynb`.
3. Turn on GPU.
4. Turn on internet, or attach the HDF5 files as a Kaggle Dataset.
5. Run all cells.
6. Download `/kaggle/working/results` for the presentation.

## References

- PDEBench paper: https://arxiv.org/abs/2210.07182
- PDEBench GitHub: https://github.com/pdebench/PDEBench
- PDEBench DaRUS dataset: https://darus.uni-stuttgart.de/dataset.xhtml?persistentId=doi:10.18419/darus-2986
