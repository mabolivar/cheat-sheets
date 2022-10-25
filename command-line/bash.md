# Bash cheat-sheet
---

## Setting environmetn variables from a file

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