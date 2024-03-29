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
  
# Day 8 - 5 August, 2022
### Pipeline / Redirecting
- history | less
    - less displays content in pages
- history | grep sudo
    - filter content with sudo in them
- history | grep “sudo chmod”
    - filter content with “sudo chmod" in them
- history | grep sudo > redirect.txt
    - stores all the content from the prev commmands in the file
- history | grep sudo >> redirect.txt
    - appends the content

# Day 9 - 6 August, 2022

### Bash Scripting
Shell → Interpreter (convert the cli commands into to instructions for kernel)

 Various Implementaions (shells)

- Bourne Shell (sh)
    - /bin/sh
- Bash (Bourne Again Shell)
    - /bin/bash
    - more improved version of sh
- zsh
    - /bin/zsh
    - extended bourne shell with many improvements

### Scripts
- .sh files
- shebang - First line of the shell script
    - #!/bin/bash
        - specify the shell based upon which the scripting is done
        - i.e. we are using bash syntax

# Day 10 - 7 August, 2022
```bash #!/bin/bash
echo "script start"

file_name=config.yaml
if [ -d "config" ]
then
	echo "reading config dir"
else
	echo "config dir not found"
fi

user_group=xx
if [ $user_group == "user" ]
then
	echo "configure the server"
elif [ $user_group == "admin" ]
then
	echo "administer the server"
else
	echo "Not permitted to configure server"
fi

echo "using file $file_name to configure server"
```
# Day 11 - 8 August, 2022
Revised 

# Day 12 - 9 August, 2022

### Parameters

- $1, $2…

### Store command results in a var

- config_files=$(ls “$config_dir”)

### Reading input from user

```bash
read -p "Enter pwd: " user_pwd
echo "Pwd: $user_pwd"
```

- all params & their count
    
    ```bash
    echo "all params: $*"
    echo "no. of params: $#"
    ```
    

### Note: $n1 + $n2 → considered as string concat.
### For Arithmatic expressions ⇒ (($n1 + $n2))

### Loops

1. while
    
    ```bash
    while true
    	do
    		read -p "enter a number" num
    		if [ "$num" == "quit" ]
    		then
    			break
    		fi
    	echo "num: $num"
    	done
    ```
    
2. for
    
    ```bash
    for param in $*
    	do
    		echo $param
    	done
    ```

# Day 13 - 10 August, 2022

### Functions

```bash
#!/bin/bash

# no params
function do_something{
	echo "doing something"
}

do_something

##################

# with params
function do_this() {
	echo "doing $1"
}

do_this "a thing"

#creating file with given file name as parameter and adding execute permission based on second parameter
function create_file() {
	file_name=$1
	touch $file_name
	echo "file $file_name created"
	if[ "$is_shell_script" = $2 ]
	then
		chmod u+x $file_name
		echo "added execute permission"
	fi
}

create_file test.sh true

function sum(){
	total=$(($1+$2))
	return $total
}
sum 2 10
result=$? #returns the result of the previous command
```

### Environment Variables

#NOTE: env vars set in a CLI session are only avaiable in that session.

- Add an environment variable
    - export DB_USER=dbuser
- Remove an environment variable
    - unset DB_USER
- /etc/environment
    - has a PATH variable
    - which is system-wide available
    - list of directories to executable files or binaries
- you can add your custom program to the PATH’s list
    - for your user
        - by going to your .bashrc file
        - then add the line
        
        ```bash
        PATH=$PATH:/home/user/my_custom_program
        ```
        
        - now you can call your custom script from anywhere

# Day 14 - 11 August, 2022
Switch → connects devices in a LAN

Router → connects with outside the LAN (or outside our network)

Firewalls → system that prevents unauthorised access from entering a private network

DNS → mapping of IPA to Names

### Root Domains

![image](https://user-images.githubusercontent.com/66965591/184267288-ff7377a1-2615-454d-a513-5ae874f22889.png)

### Top Level Domains
6 Original TLDs
- .edu
- .com
- .org
- .mil
- .net
- .gov

Others → Geographical Domains that were added later

- .ca
- .us
- .in
- .at
- .uk
- ....

### Who manages all these domain names?

⇒ Internet Corporation for Assigned Names and Numbers (**ICANN**)
- Manages the TLD development & architecture of the internet domain space
- Authorises Domain Names Registrars, to domains names maybe registered & reassigned

### DNS Working
- Every system has a DNS client preinstalled
- OS makes query req to the DNS client
- that makes req to the recursive name server
    - typically operated by your ISP
- if still not found, it’ll go to one of the 13 route servers which manage req for TLDs
    - they are available/placed all around the world
        - idk but here is the addr of .com s domain server which you can ask
    - then the recurent servers asks the .com (TLD server) if they got the IPA
        - idk here is the Authorative Name Servers of the .com domain
    - now this time the Name Server does know about the IPA and responds it back

### Commands
- ifconfig
    - IPAs of all the connected devices, gateways, subnets, etc
- netstat
    - shows the active connections on your machine and their details
- ps aux
    - details of current running processes
- nslookup
    - IPA of any domain name
    - also gives the IPA of the DNS server your system uses


# Day 15 - 12 August, 2022

SSH → Secure Shell or Secure Sockey Shell

- A network protocol that gives users, particularly system administrators, a secure way to access a computer over an unsecured network.

Commands

- Generate Key-Pair

```
#rsa -> encryption method
ssh-keygen -t rsa
```

- ssh
    
    ```
    ssh root@{REMOTE_IP_ADDRESS}
    
    // it's the same as 
    ssh -i ./ssh/id_rsa root@10.11.12.13
    // it's the default location where it checks for the private key
    // for any other location you'd need to specify it like this
    ```
    
- copy files to a remote server
    
    ```
    scp -i ./ssh/id_rsa test.sh root@10.11.12.13:/root
    //scp -i {PRIVATE_KEY_LOC} {FILE_LOC} {USERNAME}@{REMOTE_IP_ADDRESS}:{DEST_LOC}}
    ```

# Day 16 - 14 August, 2022
### Basic
- git status - Check Files Modified

### Add
- git add <file-name> 
- git add .

### Commit
- git commit -m “commit message”
- git commit -am “commit message”
- git commit —amend (adds the changes to the previous commit)
- git log

### Push
- git push origin main
- git push -u origin main
- git push —force (used when want to delete commits from the remote)

### Pull 
- git pull origin main
- git pull -u origin main
- git pull -r (doesn’t create unneccessary merge commit while pushing)

### Remote
- git remote -v
- git remote add <remote-name> <remote-url>

### Branch
- git branch
- git checkout -b <branch-name>
- git checkout <branch-name>
- git branch -d <branch-name>

# Day 17 - 15 August, 2022

### Reset
- git reset <file-name>
- git reset HEAD~1
- git reset —hard HEAD~1
- git reset <commit-hash>
	
### Revert
- git revert <commit-hash>
- when want to undo commit changes in master branch
    - creates a commit with the reverse changes of the commit-hash commit
    - then you push it to the remote master
    - #NOTE: you never git push —force in master branch

### Merge
- git merge <branch-name>
	
### Stash
- git stash
- git stash pop

### Gitignore
- git rm -r —cached .idea
	
# Day 18 - 16 August, 2022
### Building/Packaging

Application ⇒ single package aka Artifact (Deploy on the server)

Includes:

- compiling
- compress

### Artifact Repository

- storage for artifacts
- eg. Nexus, JFrog Artifactory

### File Type

- depends on the language
- Examples
    - Java ⇒ JAR (Java Archive) or WAR
        - includes all the code, dependencies
        - Execute: java -jar <jar-file>
    - Javascript ⇒ ZIP or TAR
        - includes code, but NOT dependencies

### Package Managers/Build Tools

- JAVA
    - Maven
        - XML
        - pom.xml
        - Command: mvn package
    - Gradle
        - Groovy
        - build.gradle
        - Command: ./gradlew build
- JAVASCRIPT
    - NPM/YARN
    - package.json
    - Command: npm pack

### Considering A React-Node App

- the artifact for the front and the backend can be separate or common
    - Frontend code needs to be transpiled
        - since many browsers don’t support the latest JS versions, JSX, etc
    - Code needs to be compressed
        - Separate Tools for all
            - eg. webpack, grunt, etc
	
# Day 19 - 17 August, 2022

IAAS → **Infrastructure as a service**
- instead of setting up and managing the servers and the resources we use the resources setup and managed by other providers
- eg. AWS, GCP, etc.
- AWS - Most widely used, powerful & complex.


# Day 20 - 19 August, 2022
	
### Commands
- netstat -lpnt
    - lists active internet connections(servers)

### NOTE
- #→ Root User
- $→ Standard Linux User
	
# Day 21 - 20 August, 2022
	
### Container 
- A way to package applications with all the necessary dependenciees and configs.
- Portable

Docker Image ⇒ Actual Package ⇒ when running ⇒ Container

### Docker vs Virtual Machine
- **Docker**
    - virtualises the applications layer
    - uses the host’s kernel
    - **Pros**:
        - Smaller Size
        - Runs Faster/Quickly
- **Virtual Machine**
    - virtualises application & kernel
    - when you download an image (uses its image rather than host’s)
    - **Pros**:
        - Can run an OS VM on any OS
	

### Birthday Holiday - August 21, 2022
# Day 22 - 22 August, 2022

### Image vs Container
Container: A runtime environment for IMAGE
- It has a port bound to it
- has a virtual file system

### Docker Commands
- docker pull <IMAGE_NAME>
- docker run <IMAGE_NAME> (attached mode)
    - -d (for detached mode)
    - -p<HOST_PORT>:<CONTAINER_PORT>
- docker ps
    - -a (to get running status)
- docker start <IMAGE_NAME>
- docker stop <IMAGE_NAME>


### #NOTE:
	- you can have multiple containers with the same port but you need to attach them to different HOST PORTS to use them simultaneously.
	- docker run : deals with images; creates new container;
	- docker start : deals with containers; starts already created container;
	
# Day 23 - 23 August, 2022
### Docker Commands
- docker images
    - to see all your local images
- docker exec -it <CONTAINER_ID> or <CONTAINER_NAME> /bin/bash
- docker logs <CONTAINER_ID> or <CONTAINER_NAME>

# Rest - 24 Augues, 2022
	
# Day 24 - 25 August, 2022

### Docker run vs Docker Compose

docker run

```bash
#create and run mongodb container
docker run -d \
--name mongo \
-p 27017:27017 \
-e MONGO_INITDB_ROOT_USERNAME=admin \
-e MONGO_INITDB_ROOT_PASSWORD=password \
--net mongo-network \
mongodb

#create and run mongo-express container
docker run -d \
--name mongo-express \
-p 8080:8080 \
-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
-e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
-e ME_CONFIG_MONGODB_SERVER=mongodb \
--net mongo-network \
mongo-express
```

docker-compose
```bash
version: '3'
services:
	mongo:
		image: mongo
		ports:
			- 27017:27017
		environment:
			- MONGO_INITDB_ROOT_USERNAME=admin
			- MONGO_INITDB_ROOT_PASSWORD=password
	mongo-express:
		image: mongo-express
		ports:
			- 8080:8080
		environment:
			- ME_CONFIG_MONGODB_ADMINUSERNAME=admin
			- ME_CONFIG_MONGODB_ADMINPASSWORD=password
```

### #NOTE: docker-compose creates a common network for the containers (thus no need to create & specify the network)

### docker-compose commands:
- docker-compose -f <FILE_NAME> up
- docker-compose -f <FILE_NAME> down

# Day 25 - 26 August, 2022

### Commands
- docker rm <conatiner_id>
- docker rmi <image_id>
- docker build -t <app_name> <dockerfile_location>
	
	
### Deploying App
- Replace [localhost](http://localhost) with service name
- Before
![image](https://user-images.githubusercontent.com/66965591/187005013-31a6308b-66a0-48bd-a0b7-97de806ddaa1.png)
- After
![image](https://user-images.githubusercontent.com/66965591/187005033-e7f12588-cb3a-4a04-acf7-3e61b88dd529.png)
	
(since skipped 26 in twitter will continue from 27 here too)
# Day 27 - 27 August, 2022
### Volumes
3 Types
- hostPath : pathInContainer
- name : pathInContainer
- pathInContainer

#NOTE: Docker apps for mac , creates a linux VM & stores all the docker data inside the VM’s storage

### Adding volumes in docker-compose
![image](https://user-images.githubusercontent.com/66965591/187051431-d8634680-93a6-4105-827c-374b09b2c722.png)

# Day 30 - 31 August, 2022
### Pod
- smallest unit of K8s
- Abstraction over container
- Usually 1 application per Pod
- Each Pod gets its own IP Address
- are ephemeral (can die easily - replaced with new IP)

### Service
- permanent IP Address
- lifecycle of Pod & Service are independent
