Vagrant.configure("2") do |config|

  config.vm.box = "debian/jessie64"
  config.vm.network "forwarded_port", guest: 8080, host: 8080, host_ip: "127.0.0.1"
  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 2
  end

  # Guarantee installation of VirtualBox aditions to enable synchronization using VirtualBox shared folders.
  config.vm.provider :virtualbox do
      unless Vagrant.has_plugin?("vagrant-vbguest")
        raise "The vagrant-vbguest plugin is not installed. Run `vagrant plugin install vagrant-vbguest` then try again."
      end
  end

  # Override default rsync synchronization from debian/jessie64 by VirtualBox shared folders.
  config.vm.synced_folder "..", "/vagrant", type: "virtualbox"


  config.vm.provision "docker" do |d|

      d.build_image "/vagrant/vagrant-jenkins-docker/docker/jenkins",
            args: "-t kaja78/jenkins"


      d.run "kaja78/jenkins",
            name: "jenkins",
            args: "-v /vagrant:/vagrant -v /vagrant/vagrant-jenkins-docker/.jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -v $(which docker):/usr/bin/docker --group-add $(getent group docker | cut -d: -f3)  -p 8080:8080 -p 50000:50000"

   end

   # Restart containers which are using volume mapping to VirtualBox synced folders for every vagrant up.
   # Synced folders are not available in time starting docker daemon during vagrant box boot process.
   # This is required for subsequents start of vagrant box (reload, halt & up.).

   config.vm.provision "shell", inline: "docker restart jenkins", run: "always"
end
