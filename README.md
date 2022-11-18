# CI/CD utilities

This repository contains reusable workflows for build proper CI/CD pipelines.

## Preface

This repository must to be public, because only public repositories can contain reusable workflows. Feel free to use this repository, but I strongly recommend you to fork it before use it, we can't guarantee the backward compatibility or any notifications before breaking changes.

## Parameters and secrets

The resuable workflows can receive parameters and secrets. New secret can be added at "Settings/Security/Secrets/Actions"

## Reusable workflows

### Push docker to JFrog artifactory

The `push_docker_to_jfrog.yml` contains a workflow that builds a docker image and pushes it to the JFrog artifactory.

When triggered from non-master branch, the docker gets a `-beta` after its version. Beta versions of containers can be overwritten by this pipeline. From master branch the docker image will have only its version but it will check its existence in the Artifactory. It won't overwrite an already existing version.

Parameters:
* `docker_artifact`: The path to the artifact containing the Dockerfile and the needed files
* `docker_repository`: The URL to docker repository. For example acme-docker-local
* `container_name`: The name of the new container
* `container_version`: The version of the container. For example `2.1.4`

Secrets:
* `JFrog_TOKEN`: An auth token generated by JFrog. Can be generated under Edit profile / Generate an Identity Token 
* `JFrog_URL`: The URL to JFrog. An example for JFrog cloud: acme.jfrog.io
* `JFrog_USER`: The username for JFrog. An example: acme@gmail.com