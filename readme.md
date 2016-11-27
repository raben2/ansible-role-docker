Role Name
=========

This Role can be used to install docker, docker-compose and other stuff.

Requirements
------------

- python-pip
- git
- urllib3

Role Variables
--------------
- docker_pkg: docker-engine for github installation or docker for OS package
- registry_url: Url to your docker registry 
* Leave empty to pull images from www
- registry_port: set to 443 you will need to install your registry certs from files. 
* DS-registry is used by default
- docker_images: you can define a hash of images to be pulled from the registry and put in a docker-compose.yaml
```
 docker_images:
   - name: db
     image: mysql/mysql
     version: latest
     ports: 
       - 3306
   - name: ps
     image: gliderlabs/alpine
     version: latest
     ports: 
       - 8040
     link: 
       - db
     environment:
       - "JAVA_OPTS: -Dspri....
```

```
- docker_user: ['root', 'horst']
```
- systemd_mode: combined | single
this option creates a systemd service for the whole compose stack (combined) or one for each docker container (single)
All users of the docker group are allowed to restart the service

* A list of users to be communicating with the docker daemon

Dependencies
------------
* centos7-base 

Components
------------
* /usr/sbin/docker_clean.sh * Shell script to remove unused docker volumes
* /usr/sbin/systemd_docker * Go script to create systemd docker files

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - { role: ansible-role-docker compose: True }


Author Information
------------------

Maintained by raben2 rabensteingeorg@gmail.com