## sasview_docker

contains a dockerfile and a shell script to build [SasView](https://github.com/SasView/sasview) in a container

created to make it easy to run on various linux systems

### install
have docker installed
clone this repo
build the docker image
```
cd dockerfile && docker build -t sasview .
```

### run
put the 'sasview' script somewhere in your path

run it `sasview`

### notes
the Dockerfile has comments

if instead of ubuntu:22.04, you could try a GPU base image suitable for your GPU (e.g. those from [NVidia](https://hub.docker.com/u/nvidia)https://hub.docker.com/u/nvidia) and enable the openCL lines in the Dockerfile
