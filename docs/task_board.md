# Task Board

## Week 1: data and baseline sanity

- [ ] Egor: create Python environment notes and minimal project runner.
- [ ] Egor: implement HDF5 loader for `tensor` and `x-coordinate`.
- [ ] Vitaliy: download/check Burgers `Nu0.01`, record size/hash if possible.
- [ ] Vitaliy: implement RMSE, nRMSE, max error, CPU timing.
- [ ] Daria: collect source notes from PDEBench paper/GitHub into slide outline.
- [ ] Daria: prepare first visualization plan and captions.
- [ ] Magomedrashad: write equations for advection and Burgers; define target recovered terms.
- [ ] Magomedrashad: choose derivative scheme and SINDy candidate library.

## Week 2: methods

- [ ] Egor: implement DMD reconstruction and rollout prediction.
- [ ] Egor: produce first DMD plots for Burgers.
- [ ] Magomedrashad: implement or guide SINDy/PDE-FIND fitting.
- [ ] Magomedrashad: validate coefficient recovery on synthetic/simple data first.
- [ ] Vitaliy: inspect PDEBench FNO/U-Net/PINN baseline feasibility.
- [ ] Vitaliy: create experiment table format.
- [ ] Daria: assemble data/method slides with real plots.

## Week 3: comparison and finalization

- [ ] Egor: run final DMD experiments on Burgers and Advection subset.
- [ ] Magomedrashad: interpret SINDy coefficients and failure modes.
- [ ] Vitaliy: produce final metrics table and baseline comparison.
- [ ] Daria: finish final presentation and result narrative.
- [ ] Whole team: rehearse conclusion and limitations.

## Definition of Done

- HDF5 data can be loaded reproducibly.
- At least one PDE dataset has DMD and SINDy/PDE-FIND results.
- Metrics table includes DMD, SINDy/PDE-FIND, and one baseline.
- Presentation has data, method, results, comparison, and conclusion.
- Every plot in the presentation is generated from project code or clearly sourced.
