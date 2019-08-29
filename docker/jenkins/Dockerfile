from jenkins/jenkins:2.190

RUN /usr/local/bin/install-plugins.sh blueocean workflow-aggregator

USER root

# Add docker dependencies
RUN apt-get update && apt-get install -y lxc libltdl7 && rm -rf /var/lib/apt/lists/*

# Install docker-compose
#RUN curl -L https://github.com/docker/compose/releases/download/`cuvagrantrl -I https://github.com/docker/compose/releases/latest | grep -Fi Location: | rev | cut -d/ -f1 | rev | tr -cd '[[:alnum:]]._-'`/docker-compose-`uname -s`-`uname -m` > /usr/bin/docker-compose && chmod +x /usr/bin/docker-compose

USER jenkins