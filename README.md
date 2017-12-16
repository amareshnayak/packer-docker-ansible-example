##Prerequirements:

- Install <a href="https://docs.docker.com/engine/installation/">docker engine</a>
- Install <a href="https://www.packer.io/docs/install/index.html">packer</a>
- Install <a href="http://docs.ansible.com/ansible/latest/intro_installation.html">ansible</a>

##Run build

packer build -var 'playbook=php' -var 'build=1.1' build.json

```
docker output will be in this color.
 
 ==> docker: Creating a temporary directory for sharing data...
 ==> docker: Pulling Docker image: centos:latest
     docker: latest: Pulling from library/centos
     docker: 85432449fd0f: Pulling fs layer
     docker: 85432449fd0f: Verifying Checksum
     docker: 85432449fd0f: Download complete
     docker: 85432449fd0f: Pull complete
     docker: Digest: sha256:3b1a65e9a05f0a77b5e8a698d3359459904c2a354dc3b25ae2e2f5c95f0b3667
     docker: Status: Downloaded newer image for centos:latest
 ==> docker: Starting docker container...
     docker: Run command: docker run -v /home/ashatunov/.packer.d/tmp/packer-docker449345607:/packer-files -d -i -t centos:latest /bin/bash
     docker: Container ID: 68cb7607c5b84f21f5c1bd08307f0f5a7abb69d068fe6f737adb1dff0a1f2c56
 ==> docker: Provisioning with Ansible...
 ==> docker: Executing Ansible: ansible-playbook --extra-vars packer_build_name=docker packer_builder_type=docker -i /tmp/packer-provisioner-ansible998569274 /var/www/shatu.nov.su/ansible/php.yml --private-key /tmp/ansible-key579507079
     docker:
     docker: PLAY [Install php] *************************************************************
     docker:
     docker: TASK [Gathering Facts] *********************************************************
     docker: ok: [default]
     docker:
     docker: TASK [common : Install EPEL repo.] *********************************************
     docker: changed: [default]
     docker:
     docker: TASK [common : Install EPEL repo GPG key] **************************************
     docker: changed: [default]
     docker:
     docker: TASK [php-fpm : Install Remi base repo.] ***************************************
     docker: changed: [default]
     docker:
     docker: TASK [php-fpm : Install Remi php repo.] ****************************************
     docker: changed: [default]
     docker:
     docker: TASK [php-fpm : Install REMI repo GPG key] *************************************
     docker: changed: [default]
     docker:
     docker: TASK [php-fpm : Install php] ***************************************************
     docker: changed: [default] => (item=[u'php-fpm'])
     docker:
     docker: RUNNING HANDLER [common : update packages] *************************************
     docker: changed: [default]
     docker:
     docker: PLAY RECAP *********************************************************************
     docker: default                    : ok=8    changed=7    unreachable=0    failed=0
     docker:
 ==> docker: Committing the container
     docker: Image ID: sha256:16c905562bd30475192438f6d2fc27639b02e5471e4fcb662e4687ac114226cd
 ==> docker: Killing the container: 68cb7607c5b84f21f5c1bd08307f0f5a7abb69d068fe6f737adb1dff0a1f2c56
 ==> docker: Running post-processor: docker-tag
     docker (docker-tag): Tagging image: sha256:16c905562bd30475192438f6d2fc27639b02e5471e4fcb662e4687ac114226cd
     docker (docker-tag): Repository: php:1.0
 Build 'docker' finished.
 
 ==> Builds finished. The artifacts of successful builds are:
 --> docker: Imported Docker image: sha256:16c905562bd30475192438f6d2fc27639b02e5471e4fcb662e4687ac114226cd
 --> docker: Imported Docker image: php:1.0
```

##When build is done see your new images:

docker images

```
REPOSITORY          TAG                 IMAGE ID            CREATED              SIZE
php                 1.0                 16c905562bd3        About a minute ago   404 MB
centos              latest              3fa822599e10        2 weeks ago          204 MB
```