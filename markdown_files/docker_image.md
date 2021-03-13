# Docker Images

## The Layered Architecture

In the [first lesson](what_is_docker.md), we learned what is a dockerfile and how is it used, now we will understand how does docker actually builds these images. First, take a look at this Dockerfile gist: [CustomFastAPIDockerfile](https://gist.github.com/pratik-choudhari/fb3e45e3e0a116d6db77c696613c4f13), open it in a new tab for quick reference.

<br>

__Image creation flow:__
1. The Dockerfile is parsed line by line.
2. For each and every command, the docker-engine builds a seperate layer.
3. The number of layers would be equal to the number of commands specified in Dockerfile.
4. Every time the image is rebuilt docker just has to pull the already created layers, that way recreation of an image is a fast operation.
5. Only the following layers will be rebuilt in case of any change:
    - The layer with changes.
    - All the layers below the changed layer.

_Note: A docker image/container can be named by user or docker assigns a random name to the image/container. Along with name, docker follows the tag system wherein images/containers can be given the same name but different tag names to distinguish between different versions of the same image/container. Docker also assigns a unique ID to every unique image._

<br>

## Commands:

__List all images:__

Command:
<pre>- docker image ls
- docker images</pre>

__Building a docker image:__

Command: 
<pre>- docker image build [OPTIONS] PATH
- docker build [OPTIONS] PATH</pre>

Description: Generates a docker image from the dockerfile. By convention the docker file is named as `Dockerfile` however, this is not mandatory and it can be named anything. `-t` flag can be used to name and tag the image

Examples:   
- `docker image build .` - Dockerfile in same directory with name `Dockerfile`

- `docker image build -t my_image:latest code/mydockerfile.txt` 

<br>

__Deleting a docker image:__

Command: 
<pre>- docker image rm [OPTIONS] IMAGE [IMAGES..]
- docker rmi [OPTIONS] IMAGE [IMAGES..]</pre>

Description: Delete single or multiple images. Use `-f` flag to force delete an image.

Examples:
- `docker image rm -f nginx:1.1`
- `docker image rm redis:latest python:slim node:old`

<br>

__Remove unused images:__

Command:
<pre>docker image prune</pre>

Description: Deletes all unused images, after confirmation. Unused images are the one's which are not tagged. As these images are not used in any conatiner it is same to delete to delete them and reclaim the disk space.

<br>

__Show history of an image:__

Command:
<pre>- docker image history [OPTIONS] IMAGE
- docker history [OPTIONS] IMAGE</pre>

Description: Prints history of the image including layer creation history with time.

Examples:
- `docker image history objectdetection:pytorch`
- `docker image history `

<br>

__Inspect image:__

Command:
<pre>- docker image inspect [OPTIONS] IMAGE [IMAGES..]
- docker inspect [OPTIONS] IMAGE [IMAGES..]</pre>


Description: Prints all information single or multiple images in a JSON format. Information includes network info, image metadata, environment variables, layers, architecture type, size, etc.

Examples:
- `docker image inspect objectdetection:pytorch`

<br>

__Pull image:__

Command:
<pre>- docker image pull [OPTIONS] NAME[:TAG|@DIGEST]
- docker pull [OPTIONS] NAME[:TAG|@DIGEST]</pre>


Description: Pull images from docker hub. Docker hub is an online repository of docker images that are published by the community members and the official team.

Examples:
- `docker image pull postgres:latest`
- `docker pull postgres@sha256:d9b06fa8350e5ec95da29e2ef99be89c7599ef89646257b9a0fe0cee74428415`

<br>

__Push image:__

Command:
<pre>- docker image push [OPTIONS] NAME[:TAG]
- docker push [OPTIONS] NAME[:TAG]</pre>


Description: Push images to docker hub. Any user can push his own custom image for sharing or for future use. Users can push frequently used images and pull them whenever required to avoid image recreation.

Examples:
- `docker image push my_custom_go_image:development`