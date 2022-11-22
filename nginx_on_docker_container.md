Docker is an Open source platform that helps to build, run and ship applications. It provides the ability to package and run an application in a loosely isolated environment called a container which makes software delivery process so easy and quick.
In this article, we are going to learn how to install Docker in Ubuntu 22.04 and run Nginx container. We are going to use cloud provider Linode for this.

Installing Docker in Ubuntu 22.04 is a straightforward and simple process. We need to update the Docker repository in Ubuntu, get the GPG key, and install docker packages and dependencies.

### Prerequisites
Freshly installed Ubuntu 22.04
Sudo privileged accounts to install packages.
Install Docker in Ubuntu
You can install the latest version of Docker using the official docker repository in Ubuntu 22.04. For this, you need to add the GPG key for the official Docker repository to your system and add the repository configuration to the APT source.

###### Download Docker GPG Key
Run the following command to add GPG key.
```
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
###### Add Docker GPG Key to System Repository
Add and configure the official docker repository in your system.
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```

