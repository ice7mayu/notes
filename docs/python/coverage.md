# Code coverage

Configure coverage by editing `.coveragerc`:

```toml
[run]
branch = True

# coverage data file path
data_file = output/.coverage

# omitted file patterns
omit = mylib/tests/*, mylib/tools/*

[html]
# html report output folder
directory = output/htmlcov
```

Use pytest to measure coverage for `mylib` package:

```bash
coverage run --source=mylib -m pytest tests/
```

To generate html report:

```bash
coverage html
```

View `output/htmlcov/index.html` in browser.

Done.
