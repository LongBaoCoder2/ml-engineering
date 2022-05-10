# Model Training

# Table of contents
- [Table of contents](#table-of-contents)

# Container
## What are Containers
- Container: A way to package the ML program and running the package as a set of **resource-isolated** processes.
- Containers take a different approach compared to VM: by leveraging the low-level mechanics of the host operating system, containers provide most of the isolation of virtual machines at a fraction of the computing power.
- Reading: [Docker Curriculum](https://docker-curriculum.com/)
<img width="440" alt="Screenshot 2022-05-10 at 19 10 28" src="https://user-images.githubusercontent.com/64508435/167615650-10dfda0f-79ac-4d9d-82bf-c4ca8b1418e6.png">

## Why Containers 
- This decoupling allows container-based applications to be deployed easily and consistently, regardless of whether the target environment is a
  - private data center,
  - the public cloud,
  - or even a developer’s personal laptop.
- Containers (& Docker) have seen widespread adoption. Companies like Google, Facebook, Netflix and Salesforce leverage containers to make large engineering teams more productive

## Operating System
- Kernel (required): Basic Part to start a host machine
  - Kernel modules (nfs, ip_tables)
  - Device drivers
  - System tools (shell, compiler)
  - Libraries (socket, ssl, crypto)
  - Utilities (file manager)

- Other dependencies (optional)
<img width="246" alt="Screenshot 2022-05-10 at 19 12 58" src="https://user-images.githubusercontent.com/64508435/167616058-b214f811-6539-40b6-ac3e-c491802b12c7.png">

## Old Fashion of Deployment
- Multiple apps per host
- Shared dependencies

## New Way: Deploy Containers
- Only share the kernel
<img width="267" alt="Screenshot 2022-05-10 at 19 15 41" src="https://user-images.githubusercontent.com/64508435/167616476-121d559d-5426-423d-94de-e1f4e6710929.png">

## From Physical Machine to Container
- Only dependency is system kernel when building the container
<img width="688" alt="Screenshot 2022-05-10 at 19 16 27" src="https://user-images.githubusercontent.com/64508435/167616600-6b500625-3c23-4512-a345-237b45a086e7.png">

# Docker
- Docker is a Linux-based, open-source containerization **platform** that developers use to build, run, and package applications for deployment using containers
  -  provide utilies to build & run the containers
<img width="550" alt="Screenshot 2022-05-10 at 19 18 19" src="https://user-images.githubusercontent.com/64508435/167616877-dae2248e-e7d2-4fb4-b557-1ee947203d2a.png">
## Docker 101
- `Image` a read-only template with instructions for creating a Docker container. (like a recipe)
- `Dockerfile` is a simple text file that contains a list of commands that the Docker client calls while creating an image
  - Start from a base image, say can start from Python3.8 base image `FROM python:3.8`
  - `CMD ["python", "./app.py"]`: if we run this containers, the `app.py` will be run.
  -  <img width="536" alt="Screenshot 2022-05-10 at 19 27 43" src="https://user-images.githubusercontent.com/64508435/167618319-97d9adbe-ecb7-48dc-915b-33391e0360c8.png">

- `Container` A container is a runnable instance of an image (a cake made by the recipe)
  - You can create, start, stop, move, or delete a container using the Docker API or CLI. 
  - You can connect a container to one or more networks, attach storage to it, or even create a new image based on its current state.
- `Docker Daemon`: The background service running on the host that manages building, running and distributing Docker containers. The daemon is the process that runs in the operating system which clients talk to.
  - build the container image from the docker file. 
- `Docker Client` - The command line tool that allows the user to interact with the daemon. More generally, there can be other forms of clients too - such
as Kitematic which provide a GUI to the users.
- `Docker Registries` (repositories) - A registry of Docker images. You can think of the registry as a directory of all available Docker images. If required, one can host their own Docker registries and can use them for pulling images.
  - Google Cloud, Azure provides their own repositories (container registries)

## Commonly use Docker Commands
- docker pull: down images from remote repo to the local repo
- docker push: push the images from local repo to remote repo
<img width="890" alt="Screenshot 2022-05-10 at 19 25 19" src="https://user-images.githubusercontent.com/64508435/167617941-43f34df4-1149-4bbd-b8e6-504b45923a71.png">

[(Back to top)](#table-of-contents)
