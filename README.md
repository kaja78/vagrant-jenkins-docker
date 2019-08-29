# Docker & Jenkins vagrant box

Vagrant box running Jenkins in docker container. Jenkins docker file is based on official jenkins/jenkins:2.190 image with minimal changes allowing using docker agent in pipelines. 
Preinstalled plugins:
* workflow-aggregator (Pipelines)
* blueocean

## Notes

* Jenkins home directory is mapped to .jenkins_home in project directory to persist Jenkins configuration and job definitions. Initial password may be found in .jenkins_home/secrets/initialAdminPassword.
* Project parent directory is mapped to /vagrant in Vagrant box and Jenkins container. So all projects stored in parent directory are accesible in Jenkins using custom workspace or using local git url.
* To create testing pipeline using local git url, just create new pipeline, use Definition: "Pipeline script from SCM", SCM: Git, repository url: /vagrant/vagrant-jenkins-docker. Save and run job to see last 5 commits.