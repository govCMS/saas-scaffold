# GovCMS Project Scaffolding

## Known Issues

* This repository is still a Work-in-Progress, and may be subject to slight alterations
* This process only applies to the [7.x-3.x](https://github.com/govCMS/govcms/tree/7.x-3.x) branch of GovCMS

## Requirements and Preliminary Setup

* [Docker](https://docs.docker.com/install/) - Follow documentation at https://docs.amazee.io/local_docker_development/local_docker_development.html to configure local development environment.

* [Mac/Linux](https://docs.amazee.io/local_docker_development/pygmy.html) - Make sure you don't have anything running on port 80 on the host machine (like a web server):

        gem install pygmy
        pygmy up

* [Windows](https://docs.amazee.io/local_docker_development/windows.html):    

        git clone https://github.com/amazeeio/amazeeio-docker-windows amazeeio-docker-windows; cd amazeeio-docker-windows
        docker-compose up -d; cd ..

* [Ahoy (optional)](http://ahoy-cli.readthedocs.io/en/latest/#installation) - The commands are listed in `.ahoy.yml` all include their docker-compose versions for use on Windows, or on systems without Ahoy.

## Project Setup

1. Checkout project repo and confirm the path is in Docker's file sharing config (https://docs.docker.com/docker-for-mac/#file-sharing):

        Mac/Linux: git clone https://www.github.com/govcms/govcms7-scaffold.git {INSERT_PROJECT_NAME} && cd $_
        Windows:   git clone https://www.github.com/govcms/govcms7-scaffold.git {INSERT_PROJECT_NAME}; cd {INSERT_PROJECT_NAME}

2. Build and start the containers:

        Mac/Linux:  ahoy up
        Windows:    docker-compose up -d

3. Install GovCMS:

        Mac/Linux:  ahoy install
        Windows:    docker-compose exec -T test drush si -y govcms

4. Login to Drupal:

        Mac/Linux:  ahoy login
        Windows:    docker-compose exec -T test drush uli

## Commands

Additional commands are listed in `.ahoy.yml`, or available from the command line `ahoy -v`

## Development

* You should create your theme(s) in folders under `/themes`
* Tests specific to your site can be committed to the `/tests` folders
* The files folder is not (currently) committed to GitLab.
* Do not make changes to `docker-compose.yml`, `lagoon.yml`, `.gitlab-ci.yml` or the Dockerfiles under `/.docker` - these will result in your project being unable to deploy to GovCMS SaaS

## Image inheritance

This project is designed to provision a Drupal 8 project onto GovCMS SaaS, using the GovCMS8 distribution, and has been prepared thus

1. The vanilla GovCMS (7.x-3.x) Distribution is available at [Github Source](https://github.com/govcms/govcms) and as [Public DockerHub images](https://hub.docker.com/r/govcms)
2. Those GovCMS images are then customised for Lagoon and GovCMS, and are available at [Github Source](https://github.com/govcms/govcmslagoon) and as [Public DockerHub images](https://hub.docker.com/r/govcmslagoon)
3. Those GovCMSlagoon images are then retrieved in this scaffold repository.
