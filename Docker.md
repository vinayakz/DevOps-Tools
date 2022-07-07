# Docker overview
Docker is a centralized platform for packaging, deploying, and running applications. Before Docker, many users face the problem that a particular code is running in the developer's system but not in the user's system. So, the main reason to develop docker is to help developers to develop applications easily, ship them into containers, and can be deployed anywhere.

# What is Docker?
Docker is an open-source centralized platform designed to create, deploy, and run applications. Docker uses container on the host's operating system to run applications. It allows applications to use the same Linux kernel as a system on the host computer, rather than creating a whole virtual operating system. Containers ensure that our application works in any environment like development, test, or production.

- Container is a standardized unit of software that packages up
  - Code
  - Dependencies
  - System tools, libraries
  - Configuration settings

- It is lightweight, standalone, executable package that includes everything
  need to run application
- Available for Linux and Windows based system
- Software runs consistently irrespective of underlying host OS  

## Docker architecture

![image](https://user-images.githubusercontent.com/33689324/177492442-175123e6-2510-483c-a332-d08fe2140f5a.png)


## VM vs Container
![image](https://user-images.githubusercontent.com/33689324/177493766-964853e4-c94b-47a6-89c6-5db0bc4ef50d.png)


Let me start by sharing how I got introduced to Docker. Take one example projects, suppose this requirement to set up, an end to end stack including various different technologies, like a web server using node js, and database such as MongoDB, a messaging system like Redis, and an orchestration tool like Ansible. We had a lot of issues developing this application with all these different components. First, the thing to be taken care of was their compatibility with the underlying operating system, we had to ensure that all these different services were compatible with the version of the operating system we were planning to use.

There have been times when certain versions of these services were not compatible with the OS. And we’ve had to go back and look for another OS that was compatible with all these different services. Secondly, we had to check the compatibility between the services and the libraries and dependencies on the OS. We’ve had issues where one service requires one version of a dependent library, whereas another service requires another version. 

The architecture of our application changed over time, we’ve had to upgrade to newer versions of these components or change the database, etc. And every time something changed, we had to go through the same process of checking compatibility between these various companies and the underlying infrastructure.

![image](https://user-images.githubusercontent.com/33689324/177495775-b247c22d-005b-4b37-8c45-0d1aab843ca7.png)

With Docker, I was able to run each component in a separate container with its own libraries and its own dependencies, all on the same VM and the OS, but within separate environments or containers. We just had to build the Docker configuration once and all our developers could now get started with a simple Docker run command, irrespective of what the underlying operating system they run. All they needed to do was to make sure they had Docker installed on their systems. 

![image](https://user-images.githubusercontent.com/33689324/177501464-02681dae-2100-4108-a333-c8e0e666735f.png)

# Installation of Docker on AWS EC2 instance
1. Login to your EC2 instance (From Git Bash) and run the following command

```sh 
sudo curl https://get.docker.com | sh
          OR
sudo yum install docker 
```
2. Start Docker

```sh 
sudo systemctl start docker
```
3. Enable Docker

```sh 
sudo systemctl enable docker
```
4. Logout and login again into the instance.
5. Verify that Docker CE is installed correctly by running the hello-world image.

```sh 
docker run hello-world
```
6. This command downloads a test image and runs it in a container. When the container runs, it prints an informational message and exits.
7. Docker CE is installed and running. 

- Setup is complete. We are ready to start learning Docker !!!!

# Example Of Docker image 

1. To pull an image from docker hub 
   https://hub.docker.com/_/jenkins?tab=description
   
2. Pulling an image -
    ```sh 
    docker pull jenkins:2.60.3
    ```
3. creating a container - docker run -p 8080:8080 or  -p 50000:50000 -v /your/home:/var/jenkins_home jenkins
4. If you want to  delete this container and images
  ```sh 
  docker ps -a  | grep jenkins 
```
5. Deleting the container  
  ```sh
  docker rm <ContainerID or Name>
  ```
6. Deleting the image  
  ```sh
  docker images  | grep jenkins 
  docker rmi <ImageID or Image Name and Tag>
  ```
  
