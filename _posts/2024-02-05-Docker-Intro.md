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




---
### References:
- [Intro to docker - Datacamp](https://app.datacamp.com/learn/courses/introduction-to-docker)https://app.datacamp.com/learn/courses/introduction-to-docker)
- [Docker Tutorial](https://www.youtube.com/watch?v=3c-iBn73dDE) - Video
