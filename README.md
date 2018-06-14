# docker-php

## Docker Hub automated build
```
See : https://hub.docker.com/r/6d6c70/php/builds/
```

## Organistation:
```
nomage : [ php_version ] -> [ debian_version ] -> Dockerfile
```
the arguments at the beginning of the file are used by packer to know which dockerfile it have to use.
Then theses dockerfiles images are created by automated build on dockerhub platform.

## Run tasks
- the first one will install packages, addons and dependancies.
- this one will install composer : see https://getcomposer.org/download/
- third one will install less and bower.
- last one is dedicated to removed useless package, cache and documentation to get the lightest image.
- then we have to modify the entrypoint so that the container to work non stop


## To run manually

```
Clone the repository :
$> git clone https://github.com/MyLittleParis/docker-php.git && cd docker-php
```

```
go into the directory with docker image you want to build
$> cd php5.6/jessie
```

```
then build the docker image
$> docker build .
```

##
To add new desired package or configuration please contact <devops@mylittleparis.com>