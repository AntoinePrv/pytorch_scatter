[pypi-image]: https://badge.fury.io/py/torch-scatter.svg
[pypi-url]: https://pypi.python.org/pypi/torch-scatter
[build-image]: https://travis-ci.org/rusty1s/pytorch_scatter.svg?branch=master
[build-url]: https://travis-ci.org/rusty1s/pytorch_scatter
[coverage-image]: https://codecov.io/gh/rusty1s/pytorch_scatter/branch/master/graph/badge.svg
[coverage-url]: https://codecov.io/github/rusty1s/pytorch_scatter?branch=master

# PyTorch Scatter

[![PyPI Version][pypi-image]][pypi-url]
[![Build Status][build-image]][build-url]
[![Code Coverage][coverage-image]][coverage-url]

<p align="center">
  <img width="50%" src="https://raw.githubusercontent.com/rusty1s/pytorch_scatter/master/docs/source/_figures/add.svg?sanitize=true" />
</p>

--------------------------------------------------------------------------------

**[Documentation](http://rusty1s.github.io/pytorch_scatter)**

This package consists of a small extension library of highly optimized sparse update (scatter) operations for the use in [PyTorch](http://pytorch.org/), which are missing in the main package.
Scatter operations can be roughly described as reduce operations based on a given "group-index" tensor.
The package consists of the following operations:

* [**Scatter Add**](https://rusty1s.github.io/pytorch_scatter/build/html/functions/add.html)
* [**Scatter Sub**](https://rusty1s.github.io/pytorch_scatter/build/html/functions/sub.html)
* [**Scatter Mul**](https://rusty1s.github.io/pytorch_scatter/build/html/functions/mul.html)
* [**Scatter Div**](https://rusty1s.github.io/pytorch_scatter/build/html/functions/div.html)
* [**Scatter Mean**](https://rusty1s.github.io/pytorch_scatter/build/html/functions/mean.html)
* [**Scatter Min**](https://rusty1s.github.io/pytorch_scatter/build/html/functions/min.html)
* [**Scatter Max**](https://rusty1s.github.io/pytorch_scatter/build/html/functions/max.html)

All included operations work on varying data types, are implemented both for CPU and GPU and include a backwards implementation.

## Installation

Ensure that at least PyTorch 0.4.1 is installed and verify that `cuda/bin` and `cuda/include` are in your `$PATH` and `$CPATH` respectively, *e.g.*:

```
$ python -c "import torch; print(torch.__version__)"
>>> 0.4.1

$ echo $PATH
>>> /usr/local/cuda/bin:...

$ echo $CPATH
>>> /usr/local/cuda/include:...
```

Then run:

```
pip install torch-scatter
```

If you are running into any installation problems, please create an [issue](https://github.com/rusty1s/pytorch_scatter/issues).
Be sure to import `torch` first before using this package to resolve symbols the dynamic linker must see.

## Example

```py
import torch
from torch_scatter import scatter_max

src = torch.tensor([[2, 0, 1, 4, 3], [0, 2, 1, 3, 4]])
index = torch.tensor([[4, 5, 4, 2, 3], [0, 0, 2, 2, 1]])

out, argmax = scatter_max(src, index)
```

```
print(out)
tensor([[ 0,  0,  4,  3,  2,  0],
        [ 2,  4,  3,  0,  0,  0]])

print(argmax)
tensor([[-1, -1,  3,  4,  0,  1]
        [ 1,  4,  3, -1, -1, -1]])
```

## Running tests

```
python setup.py test
```
