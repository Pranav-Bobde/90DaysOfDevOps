# Day 1 - 28 July, 2022

### Operating System
- made up of kernel + application/user layer

<img src="https://user-images.githubusercontent.com/66965591/181861250-082e75aa-a3f2-492e-b0ef-bbc1e4ff413b.png" width="400" height="400" /> <img src="https://user-images.githubusercontent.com/66965591/181861261-9241c85b-62c0-4f67-a2d4-849a89205421.png" width="400" height="400" />

- So the linux kernel is common in all - Just the GUI, icon packs, themes, apps, etc differs.
- Same for Android & Mac & IOS

Kernel

- Linux → linux
- MacOS → darwin
- POSIX (Portable Operating System Interface) - Standard Def to be maintained by the UNIX based OSs

# Day 2 - 29 July, 2022

### Virtualisation
Physical Machine, VM, Containers
- PM: Require all the hardware resources to run (single instance)
- VM: Multiple instances from same hardware resources
- Containers: Why create whole VMs if you can just run the apps you need. (Provide all the environment for running your app)

### Hypervisors
- Type 1: 
  - a.k.a Bare Metal Hypervisors    
  - Worked on the bare metal directly
  - More efficient & performant
  - Maily used in Data Centers
  - Ex. VMWare ESXi, Microsoft Hyper-V, etc
- Type 2:
  - a.k.a Hosted Hypervisor
  - Work on top of the OS (Host OS)
  - Less efficient
  - Mainly used by consumers
  - Ex. Oracle Virtual Box, VMWare Workstation, QEMU, etc

# Day 3 - 30 July, 2022

### Linux

File System

/home - home directory of all non-root users (Available: User)

/root - home directory of all root user

/bin - executable binary files of most essential user commands 

/sbin - executable binary files of system commands (Access: Superuser)

/lib - essential shared libraries that the binaries from /bin & /sbin use

/usr - supposed to be for user (due to storage limitations in the past, split in root bin folders and user binary folders was done)

- usually the commands are run from here only
- usually it has more binaries than the root level binaries (/bin, /sbin)

/usr/local - user applications are installed here

/opt - 3rd party apps which install in one directory (don’t split into bins, libs, etc)

/boot - files required for booting

/etc - configurations for system-wide applications

/dev - connected devices 

/var - log, cache files

/tmp - temporary resources required for some processes

/media - External devices (also referenced in /dev)

/mnt - for manual mounting

Commands
- Info about OS
    - uname -a
    - cat /etc/os-release
- Info about CPU
    - lscpu
- Info about Mem
    - lsmem

# Day 4 - 31 July, 2022

### Package Manager
1. apt or apt-get
2. Software Center
3. snap 

### Snap vs Apt
Snap
- It provides self contained packages (i.e.larger size)
    - Package includes all its dependencies
- Supports universal linux packages (.snap)
- Provides auto-updates
- snapcraft
  - command & framework used to build & publish snaps

Apt
- Dependecies are shared (i.e. smaller size)
- Linux distro specific packages (.deb)
- Manual Updates

Cons (snap):
- If multiple apps have same dependencies, it will be downloaded multiple times
    - Thus, you shuould go with apt whenever possible

### PPA
- Personal Package Archive
- Provided by the communities
- Anybody can create & share their repo to distribute their software


### Types Of Package Managers
Can be broadly classified in 2 types based on the 2 major distros
- **Debian Based**
  - apt
  - apt-get

- **Red Hat Based** 
  - yum
