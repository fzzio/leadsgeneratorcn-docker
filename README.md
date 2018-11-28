# Leads Generator (Docker implementation)

[![N|Solid](http://www.cajanegra.com.ec/wp-content/uploads/2017/01/cropped-faviconCN-32x32.png)](http://www.cajanegra.com.ec)

Docker implementation for "Leads Generator" project with:

  - CentOS 7
  - Apache 2.4
  - PHP 7.2
  - MySQL 5.4

## Installation
This installation considers that you have previously installed Docker. After this the steps are the following:

### Create project structure
```sh
$ cd <path/to/your/project/folder>
$ mkdir docker
$ mkdir volumes
$ mkdir volumes/lg-server
$ cd docker
```

### Pull repo
```sh
$ git init
$ git remote add origin git@github.com:<your-github-user>/leadsgeneratorcn-docker.git
$ git pull origin master
```

### Build Docker configurations
This step takes a few minutes the first time because the Linux distro, the apache and all the dependencies of the configuration indicated in the Dockerfiles are being downloaded.
```sh
$ docker-compose build
```

### Up Docker
Start docker containers. Do not close this terminal:
```sh
$ docker-compose up
```

## Credits
This docker implementation:
  - Henry Lomas - <henry@cajanegra.com.ec>
  - Fabricio Orrala - <fabricio@cajanegra.com.ec>
