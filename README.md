# Ubuntu 16.04 LTS (Xenial) Ansible Test Image

[![Docker Automated build](https://img.shields.io/docker/automated/buluma/docker-ubuntu1604-ansible.svg?maxAge=2592000)](https://hub.docker.com/r/buluma/docker-ubuntu1604-ansible/) [![Docker pulls](https://img.shields.io/docker/pulls/buluma/docker-ubuntu1604-ansible)](https://hub.docker.com/r/buluma/docker-ubuntu1604-ansible/) [![Docker Image CI](https://github.com/buluma/docker-ubuntu1604-ansible/actions/workflows/docker-image.yml/badge.svg)](https://github.com/buluma/docker-ubuntu1604-ansible/actions/workflows/docker-image.yml) [![Docker](https://github.com/buluma/docker-ubuntu1604-ansible/actions/workflows/docker-publish.yml/badge.svg)](https://github.com/buluma/docker-ubuntu1604-ansible/actions/workflows/docker-publish.yml) [![Github Build](https://github.com/buluma/docker-ubuntu1604-ansible/actions/workflows/build.yml/badge.svg)](https://github.com/buluma/docker-ubuntu1604-ansible/actions/workflows/build.yml) [![Build Status](https://travis-ci.com/buluma/docker-ubuntu1604-ansible.svg?branch=master)](https://travis-ci.com/buluma/docker-ubuntu1604-ansible)

Ubuntu 16.04 LTS (Xenial) Docker container for Ansible playbook and role testing.

## How to Build

This image is built on Docker Hub automatically any time the upstream OS container is rebuilt, and any time a commit is made or merged to the `master` branch. But if you need to build the image on your own locally, do the following:

  1. [Install Docker](https://docs.docker.com/engine/installation/).
  2. `cd` into this directory.
  3. Run `docker build -t ubuntu1604-ansible .`

## How to Use

  1. [Install Docker](https://docs.docker.com/engine/installation/).
  2. Pull this image from Docker Hub: `docker pull buluma/docker-ubuntu1604-ansible:latest` (or use the tag you built earlier, e.g. `ubuntu1604-ansible`).
  3. Run a container from the image: `docker run --detach --privileged --volume=/sys/fs/cgroup:/sys/fs/cgroup:ro buluma/docker-ubuntu1604-ansible:latest /lib/systemd/systemd` (to test my Ansible roles, I add in a volume mounted from the current working directory with ``--volume=`pwd`:/etc/ansible/roles/role_under_test:ro``).
  4. Use Ansible inside the container:
    a. `docker exec --tty [container_id] env TERM=xterm ansible --version`
    b. `docker exec --tty [container_id] env TERM=xterm ansible-playbook /path/to/ansible/playbook.yml --syntax-check`

## Notes

I use Docker to test my Ansible roles and playbooks on multiple OSes using CI tools like Jenkins and Travis. This container allows me to test roles and playbooks using Ansible running locally inside the container.

> **Important Note**: I use this image for testing in an isolated environment—not for production—and the settings and configuration used may not be suitable for a secure and performant production environment. Use on production servers/in the wild at your own risk!

## Author

Inspired by [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).
