---
title: 'Docker Intro'
date: 2024-02-05
tags:
  - Docker
---

### Intro to Docker

Containers run (reproducible) and behave (portable) identically.
They work in isolation from other containers and from the host device.

Containers are also more safe. If one is compromised, the others are still okay.

### Docker - managing system for containers

- Deamon - The docker server
- API - how the user interacts with the Deamon and how the applications interact with the Deamon

Containers interact with the computer through processes. The process only has access to a single folder, without looking at the entire file system.
Every container and process is kept isolated from anything else. 

3. Containers VS Virtual Machine

```
docker run hello-world
docker run -it ubuntu #for interactive containers
docker run -d postgres

docker ps #will print the running containers
```

4. We can specify the name of containers
- When creating new containers, you can specify their names.
```
docker run --name <containername> <image-name>
```
- The name of the container will be then dysplaied in the last col of docker ps output
<img width="1000" alt="Screenshot 2024-02-09 at 17 03 38" src="https://github.com/simoneatt11/simoneatt11.github.io/assets/61795621/1d17e08a-f99b-455a-8ce5-1cada7e5c92a">

- Look for a specific container using filter (-f)
```
docker ps -f "name=<container_name>" 
```

- Remove container using rm
```
docker container rm <container_name>
```

5. pulling images from docker hub
```
docker pull <image_name>
```
Which images are available on our machine?

```
docker images
```
<img width="861" alt="Screenshot 2024-02-09 at 17 24 59" src="https://github.com/simoneatt11/simoneatt11.github.io/assets/61795621/713e0142-44a7-4655-8fce-7351afd7ca46">

Remove an image using "image rm" - you can only delete them once every container inside is deleted 
```
docker image rm <image_name>
docker container prune # removes all the stopped containers
docker image prune -a # removes all the stopped containers

```

6. How to distribute images

You can upload (push) an image to a docker registry using 

```
docker image push <image name>
```
Include the private registry name in the docker image name before, if you want to push it in a specific registry.
Usually there are security limitations to a docker registry. You can login using the docker login command

You can also send the docker image to people. Save it as a file and share it. The persone receiving it will open it using the load command
```
docker save -o image.tar <image name>
docker load -i image.tar
```

7. How to create oue own images

DOCKERIMAGES are the recipy to create DOCKERCONTAINERS. To make these images we need to create a list of instructions, that we call DOCKERFILE

A DOCKERFILE always starts FROM another DOCKERIMAGE. (indeed using the command FROM + image name)

```
docker build -t first_image .
```
Personalize your immage with RUN commands. (treat it as a txt file, using nano or echo and append commands)

8.  Copying files into images
```
COPY <path-to-file-name> <path-to-file-in-destination-image>
```
without specification, everything in that file path will be copied.
To download and unzip files use RUN curl and RUN unzip. then remove the zip folder running RUN rm
```
RUN curl <file_url> -o <destination>
RUN unzip <file-path>/<filename>.zip -d <unzipped-directory>
RUN rm <file-path>/<filename>.zip
```
you can pipe the 3 commands using "\\" at the end of each line 

9.  The starting command for a docker

CMD command accept only the shell command to execute when it starts 

10.  Layers and coaching


11.  

12. 



---

To do: look for a summary table for all docker commands

---

### References:
- [Intro to docker - Datacamp](https://app.datacamp.com/learn/courses/introduction-to-docker)https://app.datacamp.com/learn/courses/introduction-to-docker)
- [Docker Tutorial](https://www.youtube.com/watch?v=3c-iBn73dDE) - Video
