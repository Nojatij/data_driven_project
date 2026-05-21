# Источники и заметки

## Тема из Excel

Project 12: "Data-driven method application for PDE identification and dynamic prediction using PDEBench data".

Ключевые требования из таблицы:
- parsing, processing, visualization;
- повторить или понять ML benchmark на pretrained ML models;
- DMD или модификация DMD для анализа spatiotemporal data;
- SINDy или модификация SINDy для восстановления исходной PDE;
- сравнить reconstruction/prediction results;
- сравнить с ML baseline по accuracy и CPU time;
- сделать выводы о факторах, улучшающих system identification and reconstruction.

## Основные ссылки

- PDEBench GitHub: https://github.com/pdebench/PDEBench
- PDEBench paper: https://arxiv.org/abs/2210.07182
- PDEBench datasets, DaRUS: https://darus.uni-stuttgart.de/dataset.xhtml?persistentId=doi:10.18419/darus-2986
- Analysis notebook: https://github.com/pdebench/PDEBench/blob/main/pdebench/data_gen/notebooks/Analysis.ipynb
- Data download README: https://github.com/pdebench/PDEBench/blob/main/pdebench/data_download/README.md
- Data URL CSV: https://github.com/pdebench/PDEBench/blob/main/pdebench/data_download/pdebench_data_urls.csv
- 1D forward baseline runner: https://github.com/pdebench/PDEBench/blob/main/pdebench/models/run_forward_1D.sh
- Metrics implementation: https://github.com/pdebench/PDEBench/blob/main/pdebench/models/metrics.py

## Что важно из статьи PDEBench

- PDEBench это benchmark suite для time-dependent PDE simulations.
- В нем есть готовые данные и код для сравнения новых data-driven/ML моделей с numerical simulations и ML baselines.
- В benchmark входят разные PDE, включая 1D Advection и 1D Burgers.
- Baseline models в статье/репозитории: FNO, U-Net, PINN, Gradient-Based Inverse Method.
- Данные лежат в HDF5 формате, обычно как `[b, t, x1, ..., xd, v]`, где `b` это samples, `t` время, `x` spatial dimensions, `v` channels.
- Метрики шире стандартного RMSE: nRMSE, max error, boundary error, conserved value error, Fourier-space errors.

## Что важно из GitHub

- Репозиторий содержит генерацию данных, загрузчики, download scripts, visualization scripts и baseline training/evaluation.
- Для 1D Advection/Burgers есть `data_gen_NLE`.
- Для скачивания данных рекомендуют `download_direct.py`, но можно брать прямые DaRUS URLs.
- Для baseline в `run_forward_1D.sh` уже перечислены FNO/U-Net/PINN команды и имена файлов.
- Для визуализации 1D Burgers/Advection в `visualize_pdes.py` используются ключи `x-coordinate` и `tensor`.

## Данные для проекта

Основной файл:
- PDE: Burgers
- Filename: `1D_Burgers_Sols_Nu0.01.hdf5`
- URL: https://darus.uni-stuttgart.de/api/access/datafile/281363
- Path in PDEBench: `1D/Burgers/Train/`
- MD5: `e6d9a4f62baf9a29121a816b919e2770`

Второй файл:
- PDE: Advection
- Filename: `1D_Advection_Sols_beta0.4.hdf5`
- URL: https://darus.uni-stuttgart.de/api/access/datafile/255674
- Path in PDEBench: `1D/Advection/Train/`
- MD5: `d595bbfd2c659df995a93cd40d6ea568`

## Предлагаемый экспериментальный дизайн

1. Start with Burgers `Nu0.01`.
2. Use a small subset first: e.g. 20-100 samples, depending on memory.
3. Split time:
   - train: first 60-70% time steps;
   - test: remaining 30-40% time steps.
4. Compare:
   - naive persistence baseline;
   - DMD prediction;
   - SINDy/PDE-FIND simulation or one-step derivative fit;
   - optional PDEBench FNO/U-Net/PINN baseline.
5. Repeat the simplest DMD/SINDy sanity-check on Advection `beta0.4`.

## Presentation story

1. Problem: learn/identify dynamics of PDE-generated data.
2. Data: PDEBench, HDF5, Burgers and Advection.
3. Methods: DMD for dynamic prediction, SINDy/PDE-FIND for equation identification.
4. Baselines and metrics: RMSE/nRMSE/max error/CPU time.
5. Results: plots and metrics table.
6. Conclusion: what works, what fails, why, and how to improve.
