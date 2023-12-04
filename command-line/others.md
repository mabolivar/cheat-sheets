This contains others commands that are useful but they don't belong (yet) to any category in this folder. 

## Identify the Target of the Symlink

Use the `readlink` command to determine where the actual library file for a symlink is located.

```bash
readlink -f libipopt.so.3
```