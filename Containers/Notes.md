# 17 June, 2022 - Day 13
Hypervisor - Originally Invented in the 1960s

- A software that runs on a computer host that virtualises it.

Explanation:

Let’s say you have a compute host,

- Compute Host
    - It has 3 Main Components:
        - CPU
        - RAM
        - NETWORK
        - STORAGE (OPTIONAL) - cuz hypervisor doesn’t necessarily virtualise the storage.
- So, how do you take it’s power and spread among multiple users
- That’s where Hypervisor comes in
- So, Hypervisor is the software layer that sits on top of the Compute host that virtualises all of the functions of the host.
- It’s what ensures that only the data that needs to be seen by that VSI is seen by the VSI
- It divides you res into subparts to enable you to schedule multiple servers
- That’s called
- VSI - Virtual Server Instance
    - it has vCPUs, vRAMs, vNICs
- Types
  - Type 1:
    - VMware ESXi - VMware
    - Hyper-V - Microsoft
    - KVM - Red Hat
    - Citrix XenServer - Zen Open Source Project
  - Type 2:
    - VMware Workstation - Linux, Windows
    - VMware Workstation Player - Linux
    - VirtualBox - Linux, Windows, Mac

# 18 June, 2022 - Day 14

## VM vs Containers

 **" VM is isolation of machines, while Containers is isolation of processes ”**

1. The level at which virtualization happens - virtualization happens at hardware level vs. OS level
2. The type of isolation achieved - isolation of machines vs. isolation of processes
3. How resources are accessed - via hypervisor vs. via kernel features such as namespace and cgroups
4. Flexibility of hardware vs. portability

Some Basic Important Components Of Container (Docker As Ref)
1. Registry
    1. A **repository or collection of repositories—used to store and access container images.**
2. Images
    1. It’s just a Binary Representation (just as vmdk is a disk image, ova is vm image)
    2. What’s interesting in the case of Container Image is that there’s also a notion of parent-child relationship & Image Layering.
    3. It’s very much like the notion of snapshots
    4. Big Advantage: It allows you to concentrate on specific things in specific places & know where they are.
        1. Let’s you discover some vulnerability in the user library in cenos or busybox, & so you need to replace it. 
        2. But before doing that you need to understand all the apps that will be impacted by that.
        3. So, with this PCRS you can easily see that all the child nodes of the busybox will be impacted by it. Thus, you can just rebuild & reployt this & all the children of it & can have a high degree of certainty that the thing that i patched here is now inherited by everything else.
    ![image](https://user-images.githubusercontent.com/66965591/174392143-219a2ac0-49db-4a79-b8ea-098bd4d4327f.png)    
    
3. Docker File
    1. Where you write all the config for the image which will be able to create a container instance
    2. You can take the analogy of classes & objects in the case of images & container instances
4. Docker Host 
    1. Daemon 
        1. Exposes all the APIs to the client
    2. Cache
        1. Caches the tree hierarchy of the images
5. Client
    1. Manages the lifecycle of the containers.
    2. Also, able to configure the infrastructure inside the Docker Host
        1. Network, Storage Storage Configurations
        2. Storage
            1. Volumes - Persistent Area Of Storage
            2. So a container will have or may have a Volume if it wants to persist any data beyond the lifecycle of the container.
            3. #NOTE: The process and the container state are tied to the Lifecycle of the container.
            4. So, you basically got 2 options.
                1. Either you create a volume & mount it on the container or
                2. You’ll push it out on a network socket to somewhere
    3. Perform operations like push, pull, run, commit, etc using the exposed API by the daemon.

# 19 June, 2022 - Day 15

Docker-Compose

- instead of writing those huge commands for each instance, you can do it all in just one
- You need to create a docker-compose.yml file
    - It contains all the different configs for all your containers
    - !Note: while building it only checks if the image with the naming convention already exits or not. If it does → it skips the build. 
    So, if you ever change the Dockerfile you will need to tell docker-compose to rebuild the image
- **!Note:** it’s docker-compose not docker compose
- Commands
    - docker-compose up -d
        - run in detach mode
    - docker-compose up -d —build
        - to force build the image
    - docker-compose down -v
        - to clear the associated volumes it creates with the instances

### Setup Dev & Prod Environments

- There are 2 ways to do so
    1. Create separate Dockerfiles for each
    2. Use the same Dockerfile

To do it in the same file

- You will need 3 docker-compose files
    - one as base
        - contains configs which are common to both
    - one for dev
        - configs specific to dev environment
    - one for prod
        - configs specific to prod environment
- To run in dev env
    - docker-compose -f <base-docker-compose-file> -f <prod-docker-compose-file>up -v —build
- To run in prod env
    - docker-compose -f <base-docker-compose-file> -f <dev-docker-compose-file> up -v —build
    - docker-compose -f docker-compose.yml -f docker-compose.prod.yml up -v —build

### **!Note:** We’ll need to add an if statement in the Dockerfile like this

- So that it does not install the dev dependancies in the prod environment
    ![image](https://user-images.githubusercontent.com/66965591/174500198-595ff19c-5e6b-45ca-ae04-9ecf31e37b07.png)

# 20 June, 2022 - Day 16

Running another service (container) - mongo

Volumes
- To persist data we’ll be needing volume
- But if we create an anonymous volume as usual we may end up deleting it (-v tag) while shutting down the containers as they are anonymous
- So we need to name our anonymous volume
- So, to name an anonymous volume we just need to prepend the name to the path

```yaml
mongo:
    image: mongo
    environment:
      - MONGO_INITDB_ROOT_USERNAME=pranav
      - MONGO_INITDB_ROOT_PASSWORD=pass
    volumes:
      - mongo-db:/data/db      #<vol-name>:path (named-anonymous-volume)
#Declaring Names
volumes:
  mongo-db:
```

- But you see our name (mongo-db) can potentially be used by any other service too
- Therefore, we’ll need to **declare** the names

### **!TIP**: To quickly connect to the mongo client run
→ docker exec -it <container-name> mongo -u <username> -p <password>

### Logs
- docker logs <container-name>
    - to see the logs once
- docker logs <container-name> - f
    - to stay in the logging console

### Network
- docker inspect <instance-name>
- docker network ls
- docker network instpect <instance-name>

### IP Address
- Docker-Compose creates a custom network just for your app
- When we have a **Custom network** we have **DNS**
- Thus, You can connect to another container just by using the **service name**

# 21 June, 2022 - Day 17

## Setting up Global Environment Variables File
- Just a good practise to have all your env variables in a single place

**!IMP**: There might me cases where the order of instantiation matters.
Add depends_on prop to the service which needs a service to be available before starting itself

```yaml
version: "3"
services:
  node-app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - PORT=3000
    depends_on:
      - mongo   #node-app depends on mongo (requires it to be available first)

  mongo:
    image: mongo
    volumes:
      - mongo-db:/data/db

volumes:
  mongo-db:
```

**!NOTE**: It can happen that the container has initialised but the application is yet to start. In such cases you need to addd checks in your app’s code.
In our case we have mongoose which by default tries to connect for 30s.

# 22 June, 2022 - Day 18

Setup authentication, caching, redis, sessions via express-session...

Link To Work: [Day18](https://github.com/Pranav-Bobde/docker-node-app/commit/8950b17f967e087abe573793904d58e2e42f5b47)

# 23 June, 2022 - Day 19
Not able to login. Thowing error. Not even getting any logs, or something.
Trying to to resolve the issue.
