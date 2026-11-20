# Reflections

This lab provided practical experience with static code analysis and its role in improving Python software quality. Using Pylint, Bandit and Flake8 helped me understand how automated analysis tools detect code quality violations, potential security vulnerabilities and deviations from PEP 8 standards.

A key learning was understanding the distinction between different categories of issues. Pylint highlighted problems involving code structure, variable scope, exception handling and maintainability. Bandit identified security risks such as unsafe temporary file creation and the use of assertions for runtime validation. Flake8 enforced coding conventions through checks for unused imports, line length and whitespace.

The correction process also reinforced several important Python practices, including avoiding mutable default arguments, using context managers for resource management, specifying file encodings, handling exceptions explicitly and minimising unnecessary global state.

Another important takeaway was that static analysis tools complement each other rather than serving as replacements for one another. Passing their checks improves code quality and reduces potential defects, but does not guarantee functional correctness. Unit testing and runtime validation remain necessary.

Overall, the lab demonstrated how static analysis can be integrated into the development workflow to identify defects early, enforce coding standards and produce more secure, maintainable and reliable software.