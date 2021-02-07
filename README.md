# SageMath

## About SageMath

   "Creating a Viable Open Source Alternative to
    Magma, Maple, Mathematica, and MATLAB"

   Copyright (C) 2005-2021 The Sage Development Team

   https://www.sagemath.org

## Variant 1: Installing Julia and SageMath from conda

1. Install SageMath in a conda environment as explained in https://github.com/sagemath/sage/blob/develop/src/doc/en/installation/conda.rst;
   we will use the conda environment name `julia-sage` as an example,
   so replace `conda create -n sage ...` by `conda create -n julia-sage ...`.

2. Activate the environment and add Julia:
   ```
   $ conda activate julia-sage
   $ conda install julia
   ```
   Solving environment: failed .....



## Variant 2: Using an existing Julia installation, creating a standalone conda installation for SageMath

1. Set up SageMath in a conda environment as explained in https://github.com/sagemath/sage/blob/develop/src/doc/en/installation/conda.rst

   We use the conda environment name `sage` as an example.

2. Configure ``PyCall`` to use this conda environment:
   ```
   julia> ENV["PYTHON"]=rstrip(read(`conda run -n sage command -v python3`, String))
   julia> using Pkg
   julia> Pkg.build("PyCall")
   ```

3. Import and use sage:
   ```
   julia> using PyCall
   julia> sage_all = pyimport_conda("sage.all", "sage", "conda-forge")
   julia> sage_all.ZZ("17")
   PyObject 17
   julia> sage_all.polytopes.cube()
   PyObject A 3-dimensional polyhedron in ZZ^3 defined as the convex hull of 8 vertices
   ```

4. Run tests:
   ```
   julia> sage_doctest_control = pyimport("sage.doctest.control")
   julia> options = sage_doctest_control.DocTestDefaults()
   julia> DC = sage_doctest_control.DocTestController(options, ["somefile.py"])
   julia> DC.run()
   ```

In the instructions above, we do not activate the conda environment.
Thus many tests that use external programs will fail.  This will need work as described in https://trac.sagemath.org/ticket/30818


## Variant 3: Using a Julia-specific Python distribution

Configure `PyCall` to use a Julia-specific Python
distribution via the `Conda.jl` package:
```
    ENV["PYTHON"]=""
    using Pkg
    Pkg.build("PyCall")
```

First manual tests:
```
    pyimport_conda("sage.features", "sage", "conda-forge")
    ---> errors apparently caused by channel priority
```

[![Build Status](https://github.com/mkoeppe/SageMath.jl/workflows/CI/badge.svg)](https://github.com/mkoeppe/SageMath.jl/actions)
