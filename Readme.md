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
