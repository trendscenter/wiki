**Loading R 4.0**

Run the following commands to add R 4.0 to path.

`$ source /apps/Framework/MKL_2020/mkl/mkl/bin/mklvars.sh intel64`
`$ export PATH="/apps/Framework/R-4.0.0/Debug_Build/bin/:$PATH"`

**Loading other versions of R**

Find the other R modules:

`$ module avail 2>&1 | grep /R-`
`Framework/R/R-3.2.3-AVX`
`Framework/R/R-3.2.3-SSE3`
`Framework/R/R-3.2.10-AVX`
`Framework/R/R-3.2.10-SSE3-SLIB`
`Framework/R/R-3.2.10-SSE3`
`Framework/R/R-3.2.10`
`Framework/R/R-3.3.1`
`Framework/R/R-3.3.3-AVX`
`Framework/R/R-3.3.3-SSE3`
`Framework/R/R-3.4.2-GNU`
`Framework/R/R-3.5.1-MKL-Intel`
`Framework/R/R-3.6.1`
`Framework/R/R-3.6.2`

Load a module:

`$ module load Framework/R/R-3.6.2`

**Using R**

Once loaded, you can start the R console:

`$ R`
`>`

Or execute an R script:

`$ Rscript `<file name>