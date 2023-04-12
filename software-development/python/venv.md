## pyenv

Guide: https://github.com/pyenv/pyenv

Installation
```
brew install pyenv
```

```
pyenv install 3.8.6
pyenv local 3.8.6
pyenv exec python -m venv venv
```

## poetry

Within the venv:
```
pip install poetry
poetry install
```
  
For some of  packages, you might require to add you private repository credentials to `poetry`.

```
poetry config http-basic.<myprivate_pypi> <username> <password>
```

