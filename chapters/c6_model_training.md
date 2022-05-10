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


# Distributed Training
- If the data is too large, we can perform Distributed Training

## Model and Data Parallelism
- `Worker` (a physical server) a separate machine that contains a CPU and one or more GPUs
- `Accelerator`: a single GPU (or TPU)
- `All-reduce`: a distributed algorithm that aggregates all the trainable parameters from different workers or accelerators.
  - after integration, we sync all the workers's parameters should be the same before going to the next integration.
- `Distributed training strategies`: how to distribute training across multiple GPUs, multiple machines, or TPUs 
  - tf.distribute.Strategy is a TensorFlow API 
- `Synchronous training`: all workers/accelerators train over different slices of input data and aggregate the gradients in each step
- `Async training`: all workers/accelerators are independently trained over the input data and update variables in an asynchronous manner
<img width="1031" alt="Screenshot 2022-05-10 at 20 43 50" src="https://user-images.githubusercontent.com/64508435/167631118-ff624c98-6916-4a01-9867-e16ea370c5a8.png">

### 1 single worker with multiple GPU: Scaling to Multiple GPUs
<img width="996" alt="Screenshot 2022-05-10 at 20 47 11" src="https://user-images.githubusercontent.com/64508435/167631764-61aea8a2-2706-4d63-bde0-49c8ddc1c199.png">
- Most commonly used scenario.
- TF provides **Mirrored Strategy**

```Python
mirrored_strategy = tf.distribute.MirroredStrategy(devices=["/gpu:0", "/gpu:1"])
with mirrored_strategy.scope():
model = tf.keras.Model(inputs=inputs, outputs=x) model.compile(...)
model.fit(...)
```
- to make the copy of variables to each GPU
- input data will be split into multiple slices and send all to each GPU

<img width="748" alt="Screenshot 2022-05-10 at 20 48 45" src="https://user-images.githubusercontent.com/64508435/167632056-897a122a-d786-4093-9ef5-da7f32c5c53c.png">
<img width="561" alt="Screenshot 2022-05-10 at 20 49 01" src="https://user-images.githubusercontent.com/64508435/167632102-3e00de6f-bfd1-4225-a681-3b264232207d.png">
<img width="696" alt="Screenshot 2022-05-10 at 20 49 53" src="https://user-images.githubusercontent.com/64508435/167632249-3cef91aa-3a82-4d13-a3c8-43cd9779ab47.png">

### Multiple Workers Multiple GPU: Scaling to Multiple Nodes
<img width="696" alt="Screenshot 2022-05-10 at 20 56 14" src="https://user-images.githubusercontent.com/64508435/167633399-3288a6d5-13bb-4990-8cd3-8ec17fed289b.png">

- MultiWorkerMirrored Strategy (Similar to Mirrored Strategy)
- First, need to setup the cluster if using Cloud Platform (if not, you need to setup server by your own)
- Multi-worker All Reduce

<img width="827" alt="Screenshot 2022-05-10 at 20 57 57" src="https://user-images.githubusercontent.com/64508435/167633684-166fece7-8016-48e9-a9b7-8c17d9f50324.png">

### ParameterServer Strategy


<img width="827" alt="Screenshot 2022-05-10 at 20 59 06" src="https://user-images.githubusercontent.com/64508435/167633900-ac18b08c-5712-45b6-9aa4-4ae0cf784975.png">

[(Back to top)](#table-of-contents)
