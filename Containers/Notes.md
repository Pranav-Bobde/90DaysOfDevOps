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
