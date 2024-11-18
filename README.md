# Docker Image Tagger and Pusher

This project provides a simple shell script to re-tag a Docker image and push it to a Docker registry.

## Features

- Retags an existing Docker image with a new version.
- Logs in to a specified Docker registry.
- Pushes the newly tagged image to the registry.

## Requirements

- Docker must be installed on your system.
- You need access to the Docker registry and valid credentials.
- The source Docker image must already exist on your system or in your registry.

## Usage
#1
docker images

#2
docker tag <docker-hub>:0.0.0 <docker-hub>/:0.0.1

#3
docker login <docker-hub>

#4
docker push <docker-hub>/:0.0.1

---
tag_and_push.sh
```
#!/bin/bash

# 
OLD_TAG="...."
NEW_TAG="..."
REGISTRY="...."

echo "check ..."
docker images | grep "$(echo $OLD_TAG | cut -d':' -f1)"

if [ $? -ne 0 ]; then
  echo "not found Image: $OLD_TAG"
  exit 1
fi

echo ": $NEW_TAG"
docker tag $OLD_TAG $NEW_TAG

echo "login: $REGISTRY"
docker login $REGISTRY
if [ $? -ne 0 ]; then
  echo "error."
  exit 1
fi

echo "new image : $NEW_TAG"
docker push $NEW_TAG
if [ $? -eq 0 ]; then
  echo "success!"
else
  echo "error!"
  exit 1
fi

```


