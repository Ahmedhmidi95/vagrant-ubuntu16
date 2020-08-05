# vagrant-ubuntu16
## Requirements:
- Virtualization provider (I use VirtualBox)
- Vagrant

## Run the VM:
vagrant up
## Access VM via SSH:
vagrant ssh
## If an error occured while running the machine try re-running the provision part with:
vagrant provision 
Or run:
vagrant halt && vagrant up --provision

# See running docker containers:
sudo docker ps

## Installed tools:
- Jenkins
- Gogs
- PostgreSQL
- SonarQube
- Java 8
- Maven
- SDK
- Docker
- Docker Compose
