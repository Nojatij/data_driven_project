# Role Distribution

The workload is designed to be roughly balanced while respecting the team's stated preferences. Egor focuses on programming and is not the main owner of the presentation. Magomedrashad owns the mathematical identification part. Daria leads the presentation and source narrative, but her contribution is not limited to slide formatting. Vitaliy owns an independent technical evaluation block.

## Balakin Egor

Role: code and experiment pipeline lead.

Responsibilities:

- maintain the project structure, environment notes, and reproducible execution workflow;
- implement the HDF5 loader for PDEBench data;
- implement the DMD reconstruction and prediction pipeline;
- keep scripts and notebooks runnable by the rest of the team;
- help export plots for the presentation without owning the final presentation work.

Expected artifacts:

- `src/data_loader.py`, if the notebook is later split into modules;
- `src/dmd.py`, if the notebook is later split into modules;
- DMD experiment notebook or equivalent script;
- README instructions for running the code.

## Ismailov Magomedrashad

Role: mathematical modeling and identification lead.

Responsibilities:

- review the governing equations for 1D Burgers and 1D Advection;
- define which terms SINDy/PDE-FIND should recover;
- design the candidate library for sparse PDE identification;
- choose or review numerical derivative and regularization settings;
- interpret the identified coefficients and explain whether the recovered model is physically reasonable.

Expected artifacts:

- mathematical notes for DMD and SINDy/PDE-FIND;
- method description for the final report;
- coefficient interpretation table;
- short sensitivity check for derivative and threshold choices.

## Daria Prochukhan

Role: presentation, paper synthesis, and visual results lead.

Responsibilities:

- synthesize the PDEBench paper and GitHub materials into a clear project narrative;
- organize the final presentation structure;
- select and caption the most important visual results, including heatmaps, time slices, prediction comparisons, and error curves;
- ensure that the final story is coherent: data, methods, metrics, results, and conclusion.

Expected artifacts:

- final slide deck in `presentation/`;
- source summary and presentation outline;
- list of figures and final captions;
- final "what worked / what did not work" comparison.

## Egorov Vitaliy

Role: baseline and evaluation lead.

Responsibilities:

- inspect the PDEBench FNO, U-Net, and PINN baseline scripts;
- decide which baseline comparison is realistic for the project scope;
- implement or review metrics such as RMSE, nRMSE, MAE, MAPE, maximum error, and compute time;
- maintain the experiment comparison table;
- help validate the data split and result consistency.

Expected artifacts:

- `src/metrics.py`, if the notebook is later split into modules;
- baseline evaluation notebook or equivalent script;
- `results/metrics_table.csv`;
- short conclusion on accuracy versus compute time.

## Workload Summary

- Egor: approximately 25%, focused on core code and DMD.
- Magomedrashad: approximately 25%, focused on mathematics and SINDy/PDE-FIND.
- Daria: approximately 25%, focused on sources, visualization, and presentation.
- Vitaliy: approximately 25%, focused on baseline evaluation, metrics, and comparison tables.

These roles are independent but connected: Egor provides the working pipeline, Magomedrashad validates the PDE identification, Vitaliy produces the evaluation comparison, and Daria turns the results into a coherent final presentation.
