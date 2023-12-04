## pyenv

Guide: https://github.com/pyenv/pyenv

Installation
```
brew install pyenv
```

```
pyversion=3.9.14
pyenv install $pyversion
# env PYTHON_CONFIGURE_OPTS="--enable-shared" pyenv install --verbose $pyversion
pyenv local $pyversion
pyenv exec python -m venv venv
```

## Artifactory 

It is possible to add a `PIP_INDEX_URL` using the following command.
```
export PIP_INDEX_URL=<username>:<password>@<myprivate_pypi>
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


Add packages
```
poetry add psycopg2-binary==2.9.9
```

