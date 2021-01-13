# Pytest

## Features

- 自动发现test模块和方法
- pytest允许使用python标准的assert语句校验期望值和预期值

## Assert

### Assert exception and result

```python
# content of test_sample.py
def func(x):
    return x + 1


def test_answer():
    assert func(3) == 5
```

### Assert that a certain exception is raised

```python
# content of test_sysexit.py
import pytest


def f():
    raise SystemExit(1)


def test_mytest():
    with pytest.raises(SystemExit):
        f()
```
