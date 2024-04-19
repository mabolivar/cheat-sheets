
## set up
https://pre-commit.com/

## .pre-commit-config.yaml

The following is an example of the pre-commit file.

```yaml
repos:  
- repo: https://github.com/timothycrosley/isort  
rev: 5.12.0  
hooks:  
- id: isort  
args: ["--profile", "black"]  
  
- repo: https://github.com/psf/black  
rev: 22.8.0  
hooks:  
- id: black  
language_version: python3.9  
  
- repo: https://github.com/pycqa/flake8  
rev: 5.0.4  
hooks:  
- id: flake8  
additional_dependencies: [flake8-bugbear]
```


