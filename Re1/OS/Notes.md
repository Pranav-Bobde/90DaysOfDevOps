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
- Dependencies are shared (i.e. smaller size)
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

# Day 5 - 1 August, 2022

### Users & Permissions

#### 3 Types Of Users/Accounts
1. Root (a.k.a superuser) Account (ONLY 1)
    1. Unrestricted Access
2. Regular Account
    1. Standard user with regular access
3. Service Account
    1. Relevant for Linux Server Distros
    2. Each service gets its own user
    3. Best practice for security
    
#### Why do we need users?
In general:
- to share resources
- to have personal workspaces in the same system

It’s more useful in the case of servers:
- as you shouldn’t use root account to make changes
- you can’t give every one the same level of permissions
- to manage & track each users changes

Permissions can be set at
- User Level
    - set permissions for each user
- Group Level
    - set permissions for a group of users
    - you can create groups in linux and add users to them
    - a user can be a part of multiple groups
    - any user added will gain the permissions of the group

#### Access Control Files
- /etc/passwd - details of all the users
- /etc/shadow - password of the user
- /etc/group - details of all the groups

When you do cat /etc/passwd, you can see format like this
```
debian:x:1000:1000:Debian,,,:/home/debian:/bin/bash

USERNAME : PASSWORD : UID : GID : GECOS : HOMEDIR : SHELL
```

- 'x' here is just a placeholder for the password. And the password is actually stored in encrypted form at /etc/shadow
- , , , - are just the placeholder for any extra info about the user

#### Commands
- sudo adduser newuser1
- ![image](https://user-images.githubusercontent.com/66965591/182856006-e3f8e714-096d-4bf8-9aa9-5121712b3e20.png)

- sudo passwd newuser1
- ![image](https://user-images.githubusercontent.com/66965591/182856050-5d9dd13c-46fe-4de7-b391-8c6f3c564c6a.png)

- su - newuser1
- ![image](https://user-images.githubusercontent.com/66965591/182856140-d62d84ff-8817-4a2d-842d-cc49daef1b6b.png)

- sudo groupadd newusersgroup
    - Note: while creating a new user os also creats a group with the user’s name
    - As you can see here
    - ![image](https://user-images.githubusercontent.com/66965591/182856205-3def7866-5421-4718-8b08-957ea560bf94.png)

    
- sudo usermod -g newusersgroup newuser1
    - Makes the given group as the primary group of the given user
    - ![image](https://user-images.githubusercontent.com/66965591/182856414-29ec7554-d91b-4d0d-9049-76968ff224fd.png)

    
- sudo delgroup newuser1
    - delete the default group newuser1
- sudo usermode -G admin, newusersgroup newuser1
    - to add multiple groups to the secondary groups of the user
    - Note: it overwrites the current list of groups of the user
- sudo usermode -aG admin, newusersgroup newuser1
    - appends the given groups to the given user’s groups
- groups
    - lists all the groups the user is a part of
- sudo useradd -G newusersgroup newuser2
    - it will create a user and add it to the given list of groups
    - but now too, it will create the newuser2 (default group) as the primary group
    - ![image](https://user-images.githubusercontent.com/66965591/182856470-733c0537-4f4a-4ca8-8e83-17d8d81a5e53.png)

    
- sudo gpasswd -d newuser2 newusersgroup
    - to delete a user from a group
    - ![image](https://user-images.githubusercontent.com/66965591/182856513-faf0cdb6-6bc0-4c63-b5b3-1a1c12e482a3.png)

### Users & Groups
#### Commands 
- adduser or useradd
- addgroup or groupadd
- delUser or userdel
- delgroup or groupdel

Former is:
- more interactive & user friendly
- Use-case: manually executing tasks

Latter is:
- provide all details as params
- low-level utilities
- Use-case: when writing scripts

# Day 6 - 2 August, 2022

### Ownership & Permissions
#### Owners:
- User
    - Who created that file
- Group
    - The primary group of the creator of the file

#### Commands
- sudo chown newuser1 text.txt
    - change the owner of the file
- sudo chown newuser1:newUsers text.txt
    - change the group owner of a file
- sudo chgrp newusersgroup text.txt
    - change the group owner of a file

To list files & folders with their permissions
```bash
ls -l
# to view hidden files too
ls -la
```

![image](https://user-images.githubusercontent.com/66965591/182857660-e46111f7-8781-4b54-b8af-532fc708140b.png)

```bash
-rw-r--r-- 1 debian debian    0 Aug  3 13:07 text.txt

<filetype><up><gp><op> owner group-owner size month day time file-name

# all are sequences of 3 letters (w, r, x)
#up => user permissions
#gp => group permissions
#op => others permissions

```

#### File Types
1. **–** : regular file
2. **d** : directory
3. **c** : character device file
4. **b** : block device file
5. **s** : local socket file
6. **p** : named pipe
7. **l** : symbolic link

For Example: drwxrw-r-x
- d → it’s a directory
- rwx → owner has read, write & execute permissions
- rw- → group has read & write permissions
- r-x → others have read & execute permissions

![image](https://user-images.githubusercontent.com/66965591/182858164-fccca18d-2585-43fc-92c8-87bc9ccd39b7.png)

#### There are 3 ways to set permissions:
- **Symbols**
    1. One permission for one type (user, group or others) at a time
    2. All 3 permissions for one type (user, group or others) at a time
- **Numerical**
    1. All permissions at once for all types (user, group or others) at a time
    2. ![image](https://i.imgur.com/SGYIu.png)

**Examples with commands:**
- sudo chmod -x
    - remove execute permission from all
    - Before:
    - ![image](https://user-images.githubusercontent.com/66965591/182857568-e0dc3c35-e497-419e-8dff-88d60e379277.png)
    - After:
    - ![image](https://user-images.githubusercontent.com/66965591/182857544-64b04c15-9223-46ff-9c71-3d43464de285.png)
- Use can specify u (for user), g (for group), o (for others) before adding or substracting permission
- For Example:
    1. **Symbols**
        - sudo chmod g-r newDir
            - remove read permission from newDir
            - Before:
            - ![image](https://user-images.githubusercontent.com/66965591/182857510-8aae9703-36db-45d8-841c-e12ee77e2886.png)
            - After:
            - ![image](https://user-images.githubusercontent.com/66965591/182857474-c44ad7b6-1ce2-444b-9e38-8346be1eafa3.png)
        - sudo chmod g=rwx newDir
            - Before: 
            - ![image](https://user-images.githubusercontent.com/66965591/182857439-7b8e6e8f-5581-4666-a428-a2a0fd8c2aea.png)
            - After:
            - ![image](https://user-images.githubusercontent.com/66965591/182857387-87139176-4f00-4921-9363-3be61fd5bd64.png)
    2. **Numeric**
        - sudo chmod 777 newDir
        - Before:
        - ![image](https://user-images.githubusercontent.com/66965591/182857338-78065776-9a32-4fb5-8a94-ce6441904ec5.png)
        - After:
        - ![image](https://user-images.githubusercontent.com/66965591/182857305-8e3559dd-efd8-4d8b-a882-78f8041bdf35.png)

# Day 7 - 4 August, 2022
  Revised previous content and prepared content (notes).
 
 
