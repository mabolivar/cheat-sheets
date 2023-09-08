## Install package from github repo (branch)

### HTTPS
```bash
pip install git+https://github.com/{user}/{repo_name}.git@{branch_name}
```

### SSH
```bash
pip install git+ssh://git@github.com/{user}/{repo_name}.git@{branch_name}
```

## pip version specifiers

Certainly! Here are various ways you can specify version ranges and other constraints in a `requirements.txt` file in pip:

### Version Specifiers

1. **Exact Version**
   ```
   numpy==1.21.0
   ```
   
2. **Greater Than or Equal to a Version**
   ```
   numpy>=1.21.0
   ```
   
3. **Less Than a Version**
   ```
   numpy<1.22.0
   ```
   
4. **Combining Specifiers**
   You can combine version specifiers to indicate a range of acceptable versions.
   ```
   numpy>=1.21.0,<=1.22.0
   ```

5. **Not Equal to a Version**
   ```
   numpy!=1.21.0
   ```

6. **Compatible Release**
   This will install the latest version that is compatible with the specified version (same major version for 1.0.0 and above, or same minor version for pre-1.0.0 releases).
   ```
   numpy~=1.21.0
   ```

7. **Wildcards**
   You can use wildcards to specify version patterns. However, this feature is supported only from `pip` version 20.3 onwards.
   ```
   numpy==1.21.*
   ```

### Installing from Various Sources

1. **Installing from PyPI**
   The usual case, where packages are fetched from the Python Package Index.
   ```
   numpy==1.21.0
   ```

2. **Installing from a Git Repository**
   You can install a package directly from a Git repository. Optionally specifying a branch, tag, or commit.
   ```
   git+https://github.com/user/repository.git@branch#egg=package_name
   ```

3. **Installing from a Local Directory**
   You can install a package from a local directory.
   ```
   ./local_directory/package_name/
   ```

4. **Installing from a URL**
   You can specify a direct URL to a package.
   ```
   https://example.com/path/to/package_name-1.0.0-py2.py3-none-any.whl
   ```

### Extras and Environment Markers

1. **Extras**
   You can specify extras (optional dependencies) that you want to install with a package.
   ```
   package_name[extra1, extra2]
   ```

2. **Environment Markers**
   Environment markers allow you to install packages only if certain conditions are met (e.g., Python version, OS).
   ```
   package_name; python_version < '3.8'
   ```

### Comments

1. **Inline Comments**
   You can add inline comments to explain the inclusion of a particular package or version.
   ```
   numpy==1.21.0  # Pinned due to compatibility issues with 1.22.0
   ```

2. **Separate Line Comments**
   You can also add comments on separate lines for more detailed explanations.
   ```
   # Installing numpy 1.21.0 due to compatibility reasons
   numpy==1.21.0
   ```

Remember to test your application thoroughly when upgrading dependencies, especially when using flexible version specifiers, as updates can sometimes introduce breaking changes.