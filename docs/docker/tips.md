# Docker tips

## Bind-mount current directory in Windows Git Bash

To work with `pwd` instead of full absolute path:

```bash
$ winpty docker run --rm -it -v /$(pwd):/backup --name busybox busybox
/ #
```

## Share images between machines with tar ball

Save the Docker image as a tar file, add filename (not just directory) with -o

```bash
docker save -o myfile.tar centos:16
```

Then copy your image to a new system with regular file transfer tools such as `cp` or `scp`. After that you will have to load the image into Docker:

```bash
docker load -i <path to image tar file>
```
