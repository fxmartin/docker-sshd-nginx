# docker-sshd-nginx
Dockerfile for building docker container with passwordless sshd server and nginx serving static page. This is mostly a template for creating more useful docker images.

## About

This repository contains all needed resources to build a docker image with following features:
* sshd with passwordless login;
* nginx running and serving simple static page;
* services configured and runnign via supervisord.

For convenience there is a *./manage.sh* command for building, starting (with proper port mappings), stopping and connecting via ssh.

## Why forking the original viliusl/docker-sshd-nginx?

Mainly to apply [best practices](https://docs.docker.com/articles/dockerfile_best-practices) in order to optimize the building process and the resulting size of the image
* Ease later changes by sorting multi-line arguments alphanumerically
* Avoid RUN apt-get upgrade or apt-get dist-upgrade -y --no-install-recommends
* Don’t do RUN apt-get update on a single line  (but along with apt-get install)
* Do NOT use DEBIAN_FRONTEND=noninteractive

As a matter of fact it proved to reduce the image size by a mere 45 Mb (based on ubuntu/precise) for what it's worth.

REPOSITORY | TAG | IMAGE ID | CREATED | SIZE
---------- | --- | -------- | ------- | ----
fxmartin/ubuntu-sshd-nginx | latest | 3f48e0953b35 | About an hour ago | 270.4 MB
fxmartin/ubuntu-sshd-nginx-precise | latest | 349d75c7471c | 48 minutes ago | 214.9 MB
viliusl/ubuntu-sshd-nginx | latest | bae0d68cf679 | 22 months ago | 259.1 MB

## Usage
You can download [this image](https://hub.docker.com/r/fxmartin/docker-sshd-nginx/) from public [Docker Registry](https://hub.docker.com/).
A bash script is provided: manage.sh, which allows to manage the container, considering that it won't stop by itself due to supervisor daemon:
* start: to start the container
* stop: to stop the container
* build: build the docker image
* ssh: ssh to the container
* web: launch chrome with the IP automatically retrieved from the script
* proc: launch chrome with the supervisord web ui (user = admin, password = admin)

**Run using command:**
```
docker run -d -p 55522:22 -p 55580:80 fxmartin/ubuntu-sshd-nginx
or
manage.sh start
```

**Connect via ssh:**
```
manage.sh ssh
```
## Screenshots

Image 1 - nginx welcome page

![nginx welcome page](https://raw.github.com/fxmartin/docker-sshd-nginx/master/screenshots/nginx_welcome_page.png)

Image 2 - supervisord web ui to manage processes

![supervisord web ui](https://raw.github.com/fxmartin/docker-sshd-nginx/master/screenshots/supervisord_console.png)

## Notes
Just don't forget to add private key (yeah, I know) from **ssh_keys** folder to you '~/.ssh/' and add it via
```
ssh-add -K ~/.ssh/id_rsa_docker
```

*Removed docker calls via sudo as it is not best practice for a local docker installation.*

## Sources
Forked from [viliusl/docker-sshd-nginx](https://github.com/viliusl/docker-sshd-nginx)
