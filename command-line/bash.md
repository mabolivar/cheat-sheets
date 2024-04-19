# Bash cheat-sheet
---

## Setting environment variables from a file

Given a `.env` file with a list of environmetn variables to be set, the envvars can be exported using the following code chunk ([more details at the docs](https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin.html)).
```bash
set -a
. ./.env
set +a
```

## Get values from a json string based on a key

Given a a `json_string ($1)` and a `key ($2)` as arguments, the following script returns the key's value (only works for string values):
```bash
#!/bin/bash  
json_string=$1  
key=$2  
  
if [[ $json_string =~ \"$key\":\"(([^\"\"]+))\" ]]  
then  
    echo ${BASH_REMATCH[1]}  
fi
```

## Package versions using `apt-get`

To find the versions of packages that you're installing via `apt-get`, you can use the `apt-cache policy` command, which will show you the version that will be installed from your current sources. For example, to find out the version of `curl`, `libmetis-dev`, `coinor-cbc`, and `coinor-libcbc-dev` that will be installed, you can add the following lines to your Dockerfile:

```bash
RUN apt-get update && apt-get upgrade -y \     
	&& apt-cache policy curl libmetis-dev coinor-cbc coinor-libcbc-dev
```
