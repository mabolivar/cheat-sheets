
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

```python
import urllib.parse
import re
import requests

def latex_img(latex:str, position:str='center') -> str:
    """
    Generates a Markdown image link for a given LaTeX expression.
    More details at: https://editor.codecogs.com/docs/4-LaTeX_rendering.php

    Parameters:
    latex (str): A raw string containing the LaTeX expression to be converted (i.e. r'<string>').
    position (str): 

    Returns:
    str: A Markdown image link if the request is successful, otherwise the LaTeX expression wrapped in dollar signs.
    
    Raises:
    ValueError: If the latex parameter is not a raw string.
    """

    # Generate the link to the LaTeX image
    base_url = r'https://latex.codecogs.com/png.latex?%5Clarge'
    encoded_latex = urllib.parse.quote(latex, safe='')
    link = base_url + encoded_latex.replace('=', '%3D')

    # Convert lowercase percent encoding to uppercase
    link = re.sub(r'(%..)', lambda x: x.group(1).upper(), link)
    
    # Check if the request to the generated link is successful
    try:
        response = requests.get(link)
        if response.status_code == 200:
            return f'![]({link})' + '{fig-align="' + position + '"}'
        else:
            return f'$$\n{latex}\n$$'
    except requests.RequestException:
        return f'$$\n{latex}\n$$'
```

Notebook code chunk example:

```{python}
#| output: asis
formula = r'''
E_{\pi_k}[Y] = E_{\pi_0}\left[ \frac{\pi_k(A|C)}{\pi_0(A|C)} Y \right].
'''

print(latex_img(formula))
```

Source: https://community.rstudio.com/t/rendering-equations-as-images-for-microsoft-output/13862/3 