
## `_quarto.yml`

This file on the project folder defines properties for all quarto documents. For example, `execute-dir: project` makes that all quarto notebooks use the project root directory as working directory.


```r
project:
  title: "dispatching-simulator"
  execute-dir: project
```

## Jupyter quarto notebooks options

```r
---
title: ""
format:
  html:
    code-fold: true
    standalone: true
    self-contained: true
    keep-ipynb: false
jupyter: python3
---
```

## Rendering equations as images

https://community.rstudio.com/t/rendering-equations-as-images-for-microsoft-output/13862/3 