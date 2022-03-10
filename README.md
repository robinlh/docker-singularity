# docker-singularity container
Run singularity from within a docker container. The intention here is mainly for building images, it's bit more portable if not using a Limux machine or Singularity isn't installed (not as straighforward as Docker). This container was originally developed for use in a CircleCI pipeline but can be used anywhere that has Docker installed.

## Get and build Docker image
```
git clone https://github.com/robinlh/docker-singularity.git
docker build -t your_tag docker-singularity/singularity/
```
## Build Singularity image
Singularity command to build an image would be:
```
sudo singularity build your_image.simg your_recipe.def
```
Building in Singularity needs root permissions so use `--privileged` flag when using `docker run`. Also need a volume shared between host and container to share Singularity files and write the Singularity image to. Note the host folder that gets mounted should have your Singularity files in it:
```
docker run --privileged -v /container_folder/:/host_folder/ your_tag build /host_folder/your_image.simg /host_folder/your_recipe.def
```
