## pyenv

Guide: https://github.com/pyenv/pyenv

Installation
```
brew install pyenv
```

```bash
pyversion=3.10.14
pyenv install --verbose $pyversion
# env PYTHON_CONFIGURE_OPTS="--enable-shared" pyenv install --verbose $pyversion
pyenv local $pyversion
pyenv exec python -m venv venv
```

In a docker container
```bash
FROM debian:buster-slim

RUN apt-get update
RUN apt-get install -y --no-install-recommends make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
RUN apt-get install -y mecab-ipadic-utf8

ENV HOME="/root"

WORKDIR $HOME
RUN apt-get install -y git
RUN git clone --depth=1 https://github.com/pyenv/pyenv.git .pyenv

ENV PYENV_ROOT="$HOME/.pyenv"
ENV PATH="$PYENV_ROOT/shims:$PYENV_ROOT/bin:$PATH"
RUN pyenv install 3.8.6
RUN pyenv global 3.8.6
```
## Artifactory 

It is possible to add a `PIP_INDEX_URL` using the following command.
```bash
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

**Note**: If this command fails, please check this [blog post](https://blog.frank-mich.com/python-poetry-1-0-0-private-repo-issue-fix/).

Add packages
```
poetry add psycopg2-binary==2.9.9
```

