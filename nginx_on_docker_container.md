Docker is an Open source platform that helps to build, run and ship applications. It provides the ability to package and run an application in a loosely isolated environment called a container which makes software delivery process so easy and quick.
In this article, we are going to learn how to install Docker in Ubuntu 22.04 and run Nginx container. We are going to use cloud provider Linode for this.

Installing Docker in Ubuntu 22.04 is a straightforward and simple process. We need to update the Docker repository in Ubuntu, get the GPG key, and install docker packages and dependencies.

### Prerequisites
Freshly installed Ubuntu 22.04
Sudo privileged accounts to install packages.
Install Docker in Ubuntu
You can install the latest version of Docker using the official docker repository in Ubuntu 22.04. For this, you need to add the GPG key for the official Docker repository to your system and add the repository configuration to the APT source.

###### Download Docker GPG Key
Run following command to add GPG key
```
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
###### Add Docker GPG Key to System Repository
Add and configure the official docker repository on your server.
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```
###### Update System Repository
Now, update APT packages to include new Docker packages using following command:
```
sudo apt-get update
```

###### Install Docker
Now you can install docker packages using the following command:
```
sudo apt-get install docker-ce
```
During the docker packages installation, the installer package triggers systemd to automatically enable and start the docker service. Use the following command to check docker service status.
```
sudo systemctl status docker
```
![2](https://user-images.githubusercontent.com/11027110/203275654-dcb81437-90d0-4898-999f-0f1081559eb1.jpg)

Check docker version and other details using following command:
```
sudo docker version
```
![3](https://user-images.githubusercontent.com/11027110/203275302-80447898-eb21-4fec-aa42-cf171d58acb3.jpg)

### Start, Stop or Restart Docker Daemon
You can run following systemctl command to stop docker service
```
sudo systemctl stop docker
```
You can run following systemctl command to start docker service
```
sudo systemctl start docker
```
You can run following systemctl command to restart docker service
```
sudo systemctl restart docker
```



