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

Nginx is running in a docker container with port 80. You can verify Nginx installation by navigating to the URL http://your-server-ip in your browser.
![7](https://user-images.githubusercontent.com/11027110/204244102-9641c916-944a-49d1-9c36-65d98363fd12.jpg)

### Create Docker Volume for Nginx
The container we just created is keeping all the Nginx configuration and static files inside the container itself. If we need to change anything or replace files, we need to access docker container every time. Similarly, in case if we delete the container, all the files and configuration files also get deleted. To resolve this issue, we need to create a docker volume in the host and map it with a container to protect configuration and web data files. In this example, we are going to create a volume with name as nginx-data. 

To create a docker volume run the following command:

```
sudo docker volume create nginx-data
```
![8](https://user-images.githubusercontent.com/11027110/204246512-d788af61-8abf-4152-8a64-29040a087412.jpg)

Get the docker volume information by running the following command:
```
sudo docker volume inspect nginx-data
```
![8](https://user-images.githubusercontent.com/11027110/204247886-7dfeddba-ac37-44a8-ab13-305f567b1b1f.jpg)

For easy access, you can create a symlink of the docker volume directory. To create symlink run the following command:

```
ln -s /var/lib/docker/volumes/nginx-data/_data /nginx
```

Now start the Nginx container with persistent data storage.
```
sudo docker run -d --name nginx-server -p 80:80 -v nginx-data:/usr/share/nginx/html nginx
```
Where,

d = run the container in a detached mode

name = name of the container to be created

p = port to be mapped with host

v = name of docker volume

![10](https://user-images.githubusercontent.com/11027110/204248095-2569405e-8674-4cca-a0af-aea12d1c3553.jpg)


Now verify the contents available in the data persistent directory with running following command:
```
sudo ls /var/lib/docker/volumes/nginx-data/_data
```
The following output will be displayed in your terminal:

![12](https://user-images.githubusercontent.com/11027110/204249812-1041f4d2-8bd7-4499-b675-b9f5c3e5ec8f.jpg)


Let's make some changes on the content of index.html file located at /var/lib/docker/volumes/nginx-data/_data
```
sudo vi /var/lib/docker/volumes/nginx-data/_data/index.html
```

Change some HTML code on index.html file and save it. Navigate the URL in your browser and you will find your Nginx contents changed as shown below:
![11](https://user-images.githubusercontent.com/11027110/204250532-dafccc61-8975-4740-8d1b-e5cb3227039e.jpg)


### Conclusion
In this article, we have learned how to install docker, pull docker image from the docker hub repository and run an application inside the docker container. Also, we have learned how to create a persistent data storage and map it with a docker container.









