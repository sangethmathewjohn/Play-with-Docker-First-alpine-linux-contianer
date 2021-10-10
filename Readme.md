### Docker Images
        
        docker image pull alpine
 The pull command fetches the alpine image from the Docker registry and saves it in our system. In this case the registry is Docker Hub.
 
 You can use the docker image command to see a list of all images on your system.
        docker image ls

### Docker Container Run

        docker container run alpine ls -l
While the output of the ls command may not be all that exciting, behind the scenes quite a few things just took place.
When you call run, the Docker client finds the image (alpine in this case), creates the container and then runs a command in that container. 
When you run docker container run alpine, you provided a command (ls -l), so Docker executed this command inside the container for which you saw the directory listing. After the ls command finished, the container shut down.

When you executed the command docker container run hello-world, it also did a docker image pull behind the scenes to download the hello-world image.

        docker container run -it alpine /bin/sh
You are now inside the container running a Linux shell and you can try out a few commands like ls -l, uname -a and others.
Note that Alpine is a small Linux OS so several commands might be missing. Exit out of the shell and container by typing the exit command

In the steps above we ran several commands via container instances with the help of docker container run. The docker container ls -a command showed us that there were several containers listed. Why are there so many containers listed if they are all from the alpine image?

This is a critical security concept in the world of Docker containers! Even though each docker container run command used the same alpine image, each execution was a separate, isolated container. Each container has a separate filesystem and runs in a different namespace; by default a container has no way of interacting with other containers, even those from the same image. Let’s try another exercise to learn more about isolation.

### ACCESS CONTAINER
        
        docker container start <container ID>
Container ID is obtained from the command

        docker contianer ls -a
Instead of using the full container ID you can use just the first few characters, as long as they are enough to uniquely ID a container. 
So we could simply use “3030” to identify the container instance in the example above, since no other containers in this list start with these characters

Notice this time that our container instance is still running. We used the ash shell this time so the rather than simply exiting the way /bin/sh did earlier, ash waits for a command. We can send a command in to the container to run by using the exec command, as follows:
        
        docker container exec <container ID> ls
To access the shell
        
        docker container exec -it <container ID> /bin/sh

### Terminology

In the last section, you saw a lot of Docker-specific jargon which might be confusing to some. So before you go further, let’s clarify some terminology that is used frequently in the Docker ecosystem.

   Images - The file system and configuration of our application which are used to create containers. To find out more about a Docker image, run docker image inspect alpine. In the demo above, you used the docker image pull command to download the alpine image. When you executed the command docker container run hello-world, it also did a docker image pull behind the scenes to download the hello-world image.
   Containers - Running instances of Docker images — containers run the actual applications. A container includes an application and all of its dependencies. It shares the kernel with other containers, and runs as an isolated process in user space on the host OS. You created a container using docker run which you did using the alpine image that you downloaded. A list of running containers can be seen using the docker container ls command.
   Docker daemon - The background service running on the host that manages building, running and distributing Docker containers.
   Docker client - The command line tool that allows the user to interact with the Docker daemon.
   Docker Hub - Store is, among other things, a registry of Docker images. You can think of the registry as a directory of all available Docker images. You’ll be using this later in this tutorial.
