Docker is an Open source platform that helps to build, run and ship applications. It provides the ability to package and run an application in a loosely isolated environment called a container which makes software delivery process so easy and quick.
In this article, we are going to learn how to install Docker in Ubuntu 22.04 and run Nginx container. We are going to use cloud provider Linode for this.

Installing Docker in Ubuntu 22.04 is a straightforward and simple process. We need to update the Docker repository in Ubuntu, get the GPG key, and install docker packages and dependencies.

### Prerequisites
Freshly installed Ubuntu 22.04 <br>
Sudo privileged accounts to install packages.


### Install Docker in Ubuntu
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

### Run Nginx Container Using Docker
Running Nginx in a docker container is a very easy and simple process. You just need to pull an Nginx image from the docker hub and create an Nginx container that serves as a web server for static files. To pull the latest Nginx image from the docker hub, you have to run the following command:

```
sudo docker pull nginx
```

![4](https://user-images.githubusercontent.com/11027110/204241250-90b6c1a2-71cf-4f65-8a74-57d5096b0ef1.jpg)


To list the docker images, run the following command:

```
sudo docker images
```

To run a container from a pulled image, run the following command:

```
sudo docker run -d --name nginx-server -p 80:80 nginx
```

![5](https://user-images.githubusercontent.com/11027110/204242174-e11bd394-bbc0-401a-930e-60cdd4456f19.jpg)

where,

d = run the container in a detached mode

name = name of the container to be created

p = port the container will be mapped with host

The output shows the container id created using the Nginx image.

To list out the running container, run the command:
```
sudo docker ps -a
```
You can find container with the status in your terminal as below :

![6](https://user-images.githubusercontent.com/11027110/204242867-74988551-1609-43da-9b88-01f7b017e2d7.jpg)






