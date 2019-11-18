# Xenon pre-commit hook

`pre-commit` hook for calculating cyclomatic complexity using Radon.

This hook uses the `Xenon` wrapper around `Radon` to calculate complexity, and will exit with a non-zero exit code if the complexity exceeds given value ('A-F', where 'A' is least complex (most desirable) and 'F' is most complex).

#### Usage

For examples of Xenon itself, see the official documentation: https://xenon.readthedocs.io/en/latest/

Below is a sample `.pre-commit-config.yaml` that includes this hook:

```yaml
repos:
-   repo: https://github.com/pre-commit/mirrors-pylint
    rev: v2.4.4
    hooks:
    - id: pylint
      args: ["--rcfile=.pylintrc-pre"]
-   repo: https://github.com/pre-commit/mirrors-isort
    rev: v4.3.21
    hooks:
    - id: isort
-   repo: https://github.com/ambv/black
    rev: 19.10b0
    hooks:
    - id: black
      language_version: python3.7
-   repo: https://github.com/prettier/prettier
    rev: 1.19.1
    hooks:
    - id: prettier
      args: ["--config=.prettierrc"]
-   repo: https://github.com/pycqa/pydocstyle
    rev: 4.0.1
    hooks:
    - id: pydocstyle
-   repo: https://github.com/yunojuno/pre-commit-xenon
    rev: cc59b0431a5d072786b59430e9b342b2881064f6
    hooks:
    - id: xenon
      args: ["--max-average=A", "--max-modules=C", "--max-absolute=C"]
```

And this is an example output:

```
(platform) ➜  platform git:(feature/deepsource) ✗ pre-commit run xenon --all-files
[INFO] Installing environment for https://github.com/yunojuno/pre-commit-xenon.
[INFO] Once installed this environment will be reused.
[INFO] This may take a few minutes...
Xenon (Radon CI).........................................................Failed
hookid: xenon

ERROR:xenon:block "tests/test_views.py:76 test_get_list" has a rank of D
```
