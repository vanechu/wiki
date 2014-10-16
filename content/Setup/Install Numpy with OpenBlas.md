---
title: "Install Numpy with OpenBlas"
layout: page
date: 2014-10-16 00:00
---

# Reference #

[How to link ATLAS/MKL to existing Numpy without rebuilding?](http://stackoverflow.com/questions/21671040/link-atlas-mkl-to-an-installed-numpy)
[How to check blas/lapack linkage in numpy/scipy?](http://stackoverflow.com/questions/9000164/how-to-check-blas-lapack-linkage-in-numpy-scipy)
[Compiling numpy with OpenBLAS integration](http://stackoverflow.com/questions/11443302/compiling-numpy-with-openblas-integration)

## Anaconda ##
`Anaconda` is a Python distribution with scitific libraies installed, and atlas is already packaged without configuration althrough it is not fast as OpenBLAS.



## Check OpenBLAS installed correctly ##

Creat test_BLAS.py with:

```
import numpy
import sys
import timeit

try:
    import numpy.core._dotblas
    print 'FAST BLAS'
except ImportError:
    print 'slow blas'

print "version:", numpy.__version__
print "maxint:", sys.maxint
print

x = numpy.random.random((1000,1000))

setup = "import numpy; x = numpy.random.random((1000,1000))"
count = 5

t = timeit.Timer("numpy.dot(x, x.T)", setup=setup)
print "dot:", t.timeit(count)/count, "sec"
```

Then Comare `OMP_NUM_THREADS=1 python test_BLAS.py` with `OMP_NUM_THREADS=8 python test_BLAS.py`
