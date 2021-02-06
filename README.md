# SageMath

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
