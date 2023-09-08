## Check container enviroment variables

The following command prints in console the container environment variables.
```bash
docker exec <container> /usr/bin/env
```

## Pass AWS credentials to containers

https://stackoverflow.com/questions/36354423/what-is-the-best-way-to-pass-aws-credentials-to-a-docker-container

## Know issues

### MacOS Ventura + Docker

For some unknown reason, only folders with the extended attributes:

```bash
com.apple.macl
com.docker.grpcfuse.ownership
```
To check if a folder has extended attributes, you can execute

```bash
 ls -ld <folder>
 # OR
 xattr <folder>
 # OR
 ls -l@ . 
```

Therefore, given a folder with appropriate attributes, these attributes can be transfer to other folder. This is an example.

```bash
#!/bin/bash

# Source Directory (with correct attributes)
SRC_DIR="./mysql-data"

# Target Directory
TARGET_DIR="./sql/initialization"

# Get Extended Attributes from Source Directory
MACL_ATTR=$(xattr -px com.apple.macl $SRC_DIR)
DOCKER_ATTR=$(xattr -px com.docker.grpcfuse.ownership $SRC_DIR)

# Apply Extended Attributes to Target Directory
xattr -wx com.apple.macl $MACL_ATTR $TARGET_DIR
xattr -wx com.docker.grpcfuse.ownership $DOCKER_ATTR $TARGET_DIR
```