# Information about the contents of this directory

The fields in this directory were created with an openqcd binary that was coded up explicitly for this purpose. You can find it [here](https://github.com/DanielRichtmann/openqcd/blob/e4a33bf0f77d84669bf469ede97af521f9e3e19e/devel/dirac/compare_gpt.c). The binary creates a random source and gauge field, applies methods of the Dirac operator with open boundary conditions, and writes out all fields in binary format. It is largely based on `devel/dirac/time2.c` so diffing against it may help your understanding. 

# Steps to reproduce the fields

```
git clone git@github.com:DanielRichtmann/openqcd.git -b compare/gpt

cd openqcd/devel/dirac

export GCC=$(which gcc) # environment variable required by openqcd's Makefile

make

./compare_gpt -bc 0
```
