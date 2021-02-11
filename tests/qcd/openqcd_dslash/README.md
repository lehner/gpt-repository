# Open boundaries

Details about the definition of open boundaries a la Lüscher can be found in the the following papers

- https://arxiv.org/pdf/1105.4749.pdf
- https://arxiv.org/pdf/1206.2809.pdf
  
as well as most nicely written up in `doc/dirac.pdf` of the [openqcd code](https://luscher.web.cern.ch/luscher/openQCD/).

# Information about the contents of this directory

The fields in this directory were created with an openqcd binary that was coded up explicitly for this purpose. You can find it [here](https://github.com/DanielRichtmann/openqcd/blob/e4a33bf0f77d84669bf469ede97af521f9e3e19e/devel/dirac/compare_gpt.c). The binary creates a random source and gauge field, applies methods of the Dirac operator with open boundary conditions, and writes out all fields in binary format. It is largely based on `devel/dirac/time2.c` so diffing against it may help your understanding. 

The parameters used in this binary are:

| Parameter  | Value   |
|------------|---------|
| `cF`       | 1.3     |
| `cF_prime` | 1.3     |
| `cG`       | 1.0     |
| `cG_prime` | 1.0     |
| `beta`     | 5.5     |
| `csw`      | 1.978   |
| `kappa`    | 0.13500 |

The fields written by this binary are:

| Filename                  | Description                                                  |
|---------------------------|--------------------------------------------------------------|
| `gauge.bc_0.bin`          | Random gauge field                                           |
| `src.bc_0.bin`            | Source vector                                                |
| `dst_Dw_dble.bc_0.bin`    | Result of `Dw * src` (full Dirac operator)                   |
| `dst_Dwoo_dble.bc_0.bin`  | Result of `Dwoo * src` (diagonal part on odd sites)          |
| `dst_Dwee_dble.bc_0.bin`  | Result of `Dwee * src` (diagonal part on even sites)         |
| `dst_Dwoe_dble.bc_0.bin`  | Result of `Dwoe * src` (hopping term from even to odd sites) |
| `dst_Dweo_dble.bc_0.bin`  | Result of `Dweo * src` (hopping term from odd to even sites) |
| `dst_Dwdag_dble.bc_0.bin` | Result of `Dw^dag * src = g5 * M * g5 * src`                 |

Comments:

- The suffix `.bc_0` denotes the choice of boundary conditions (0 = open, 3 = anti-periodic).
- The results of half-grid operations are written as full grid fields.

# Steps to reproduce the fields

```
git clone git@github.com:DanielRichtmann/openqcd.git -b compare/gpt

cd openqcd/devel/dirac

export GCC=$(which gcc) # environment variable required by openqcd's Makefile

make

./compare_gpt -bc 0
```

