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
* Do NOT use DEBIAN_FRONTEND=noninteractive, as per http://docs.docker.com/faq/

As a matter of fact it proved to reduce the image size by a mere 45 Mb for what it's worth.

## Usage
_*TODO: replace by own image link when it will have been committed*_
You can download [this image](https://index.docker.io/u/viliusl/ubuntu-sshd-nginx/) from public [Docker Registry](https://index.docker.io/).

**Run using command:**
```
docker run -d -p 55522:22 -p 55580:80 viliusl/ubuntu-sshd-nginx
```

**Connect via ssh:**
```
ssh root@localhost -p 55522
```

Just don't forget to add private key (yeah, I know) from **ssh_keys** folder to you '~/.ssh/' and add it via 'ssh-add'

## Sources
Inspired from [viliusl/docker-sshd-nginx](https://github.com/viliusl/docker-sshd-nginx)