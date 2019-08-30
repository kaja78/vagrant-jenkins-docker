# Docker & Jenkins vagrant box

Vagrant box running Jenkins in docker container. Jenkins docker file is based on official jenkins/jenkins:2.190 image with minimal changes allowing using docker agent in pipelines. 
Preinstalled plugins:
* workflow-aggregator (Pipelines)
* blueocean

## Usage

* Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
* Install [Vagrant](https://www.vagrantup.com/downloads.html)
* `git clone https://github.com/kaja78/vagrant-jenkins-docker.git`
* `cd vagrant-jenkins-docker`
* `vagrant up`
* Go to [Jenkins](http://localhost:8080) or [Blueocean](http://localhost:8080/blue)
* Initial password may be found in `.jenkins_home/secrets/initialAdminPassword`.

## Notes

* Jenkins home directory is mapped to `.jenkins_home` in project directory to persist Jenkins configuration and job definitions. 
* Project parent directory is mapped to `/vagrant` in Vagrant box and Jenkins container. So all projects stored in parent directory are accesible in Jenkins using custom workspace or using local git url (just the filesystem path to project directory).
* To create testing pipeline using local git url, just create new pipeline, use Definition: `Pipeline script from SCM`, SCM: `Git`, repository url: `/vagrant/vagrant-jenkins-docker`. Save and run job to see last 5 commits of this project.
