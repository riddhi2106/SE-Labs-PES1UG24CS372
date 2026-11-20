## Known Issue Table

| Issue | Type | Line(s) | Description | Fix Approach |
|---|---|---|---|---|
| Missing module docstring | Code Quality | 1 | Module lacks a description of its purpose. | Add a module-level docstring. |
| Unused import | Code Quality | 2 | `logging` is imported but never used (Pylint W0611, Flake8 F401). | Remove the unused import or use it appropriately. |
| Missing function docstrings | Code Quality | 10, 15, 21, 29, 33, 39, 46, 50 | Functions lack documentation describing their purpose. | Add descriptive docstrings to all functions. |
| Mutable default argument | Bug | 10 | Default list `[]` is shared across function calls, potentially causing unexpected behaviour. | Change the default to `None` and initialise the list inside the function. |
| Bare except | Bug | 18 | Catches all exceptions without specifying an exception type, potentially hiding errors. | Use specific exception types such as `except ValueError:`. |
| Inefficient dictionary iteration | Code Quality | 23 | Iterating over dictionary keys and accessing values separately is less efficient. | Use `dictionary.items()` to access keys and values together. |
| Global statement | Code Quality | 30 | Modifying global variables creates dependencies and makes code harder to maintain. | Pass variables as function arguments and return updated values. |
| Unspecified file encoding | Code Quality | 34, 41 | Files are opened without explicitly specifying an encoding. | Specify `encoding="utf-8"` when opening files. |
| Missing context manager | Bug | 34, 41 | Files are opened without using `with`, risking improper resource handling. | Use `with open(...) as f:` to ensure files close automatically. |
| Invalid function naming | Code Style | 46 | `printAlerts()` does not follow Python's snake_case naming convention. | Rename it to `print_alerts()`. |
| Insecure temporary file creation | Security | 40 | `tempfile.mktemp()` can introduce race conditions and security vulnerabilities (Bandit B306). | Replace it with `tempfile.NamedTemporaryFile()` or another secure temporary-file creation method. |
| Assert used for validation | Security | 61 | Assertions may be removed when Python runs with optimisation enabled (Bandit B101). | Replace `assert` with an explicit `if` condition and raise an appropriate exception. |
| Incorrect blank lines | Code Style | 10, 15, 21, 29, 33, 39, 46, 50 | Functions are not separated by the required two blank lines (Flake8 E302). | Add two blank lines between top-level functions. |
| Line too long | Code Style | 11 | A line contains 98 characters, exceeding the 79-character limit (Flake8 E501). | Split the statement across multiple lines. |
| Incorrect blank lines after function | Code Style | 66 | Insufficient blank lines after a function definition (Flake8 E305). | Add two blank lines after the function definition. |