# Data

HDF5 files are large and should stay local. Do not commit them.

Recommended first download:

```powershell
Invoke-WebRequest `
  -Uri "https://darus.uni-stuttgart.de/api/access/datafile/281363" `
  -OutFile "C:\Egor\skoltech\data driven\Project_12_PDEBench\data\1D_Burgers_Sols_Nu0.01.hdf5"
```

Optional second dataset:

```powershell
Invoke-WebRequest `
  -Uri "https://darus.uni-stuttgart.de/api/access/datafile/255674" `
  -OutFile "C:\Egor\skoltech\data driven\Project_12_PDEBench\data\1D_Advection_Sols_beta0.4.hdf5"
```

Each file is large, so start with Burgers only unless there is enough disk space and time.
