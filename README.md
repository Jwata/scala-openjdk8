# Scala Dockerfile
This repository has Dockerfile to build container with Scala on openjdk8.

# Base docker Image
[OpenJDK8](https://registry.hub.docker.com/u/jwata/debian-openjdk8/)
[Debian Jessie-backports](https://registry.hub.docker.com/_/debian/)

# How to use
```
docker pull jwata/scala:2.11.1
docker run -it -rm jwata/scala
```
