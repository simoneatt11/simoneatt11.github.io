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

docker run --name <containername> <image-name>

6. dndocindocin

7. sdvfvsdfbsb

8. sdbsgbsgb

9. sbgs

10. bsdgbsdgb

11. sdbgsdgbsgb

12. sbgsgbsgb



---
### References:
- [Intro to docker - Datacamp](https://app.datacamp.com/learn/courses/introduction-to-docker)https://app.datacamp.com/learn/courses/introduction-to-docker)
- 
