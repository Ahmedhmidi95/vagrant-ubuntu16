
Vagrant.configure("2") do |config|
  
  config.vm.box = "ubuntu/xenial64"

  config.vm.provider "virtualbox" do |vb|
     vb.memory = "6144"
  end

  config.vm.network "forwarded_port", guest: 8080, host: 8080 # jenkins
  config.vm.network "forwarded_port", guest: 3000, host: 3000 # git
  config.vm.network "forwarded_port", guest: 8081, host: 8081 # application
  config.vm.network "forwarded_port", guest: 9001, host: 9001 # sonarqube
  config.vm.network "forwarded_port", guest: 9200, host: 9200 # ELK
  config.vm.network "forwarded_port", guest: 5601, host: 5601 # ELK
  config.vm.network "forwarded_port", guest: 8200, host: 8200 # ELK
  config.vm.network "forwarded_port", guest: 5672, host: 5672 # rabbitMQ  
  config.vm.network "forwarded_port", guest: 9000, host: 9000 # kafdrop
 
  config.vm.provision "shell", inline: <<-SHELL
     apt-get update -y
     apt-get upgrade -y
     apt-get install -y apache2
     apt-get install wget zip unzip vim git openjdk-8-jdk -y
     # Install docker and docker compose
     apt-get install apt-transport-https ca-certificates curl software-properties-common
     curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
     add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
     apt-get update -y
     apt-get install docker-ce -y
     # docker-compose
     curl -L "https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
     chmod +x /usr/local/bin/docker-compose
     docker-compose --version
     # update max_map_count used by sonarqube
     sudo sysctl -w vm.max_map_count=262144
  SHELL

  config.vm.provision "shell", privileged: false, inline: <<-SHELL
     curl -s "https://get.sdkman.io" | bash
     source $HOME/.sdkman/bin/sdkman-init.sh
     sdk version
     sdk install maven 3.6.0
     source .bashrc
     java -version
     mvn --version
   SHELL

   config.vm.provision "shell", inline: <<-SHELL
	   cd /vagrant/compose && docker-compose up
   SHELL

end
