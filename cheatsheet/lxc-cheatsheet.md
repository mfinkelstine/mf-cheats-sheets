# LXC working on my centos
# All LXC commands have to be run as root (or sudo)

# 1. Installation Procedure

## 1.1 install lxc on Centos OS
```
yum install lxc*
```
## 1.2 installing lxc on Ubuntu OS
```
apt-get install lxc
```
## 1.3 LXC Check Configuration
To check [LXC] configuration use this command
```
lxc-checkconfig
```


# 2. LXC Basic Commands

## 2.1 LXC Service start/stop
Starting and Stopping an LXC container
```
lxc start [CONTAINER_NAME]
lxc stop [CONTAINER_NAME]
```

## 2.2 LXC list Containers
To Disply a list of container details for start and stopped containters.
The **name** field is what's usually used in order commands to reference the specific container.
```
lxc list
```
## 2.3 LXC Create Container from Image

There are further details below on managing images and remote image repository, which you’ll need when creating a new container.
This example will create a new container and start it using the Ubuntu 1604 template. 
Change [CONTAINER] to be the name of the new container.
```
lxc launch ubuntu:16.04 [CONTAINER]
```

## 2.4 LXC Delete Container
To Remove Container cannot be undone
```
lxc delete [CONTAINER]
```
# 3. LXC Images
Linux Container are created from templates or images that are stored locally or downloaded from remove repository servers.

## 3.1 LXC List Images Repository
List available images
Images that have been downloaded, imported or cached are stored locally in the image repository. 
The output will list the image name, size and various other details.

```
lxc image list

```

Remote images that reside on an image repository or remote LXC server can also be listed. 
This is great for seeing what images are available when creating new containers. 
Change [REMOTE_NAME] to be the name of the image repository from the image list command. 

>Note: add the : symbol at the end.

```
lxc image list [REMOTE_NAME]:
```


## 3.2 LXC Get image details
Further details can be obtained from an image file than what’s displayed with image list. 
The below command will detail all information known about the image. 
Replace [IMAGE_NAME] with a valid image name displayed in the image list command, such as ubuntu-xenial.

```
lxc image info [IMAGE_NAME]

```
## 3.3 LXC Add a new Image Repository
Add a new Image Repository
There are various public image repositories that can be added to your LXC installation. 
LinuxContainers.org is a common one and hosts several distribution types. 
Replace [NAME] with the text name you’d like to give to the repository (it’s just an alias) and [HOST] with the address of the repository.

```
lxc remote add [NAME] [HOST]
```
For example

```
lxc remote add lxc-org images.linuxcontainers.org

```

## 3.4 LXC Delete a local image
Delete a local image
Replace [IMAGE_NAME] with the the alias or fingerprint of the image.

```
lxc image delete [IMAGE_NAME]
```
## 3.5 LXC Create new Image from Running Container
You can create a new image from an existing container with a simple command 
however it’s important to ensure that the created template will contain everything that the running container contained – such as SSH keys, data, etc. 
It’s therefore important to ensure you clean up anything which may be sensitve before running this command.

```
lxc publish [CONTAINER] --alias [ALIAS]

```
You’ll need to change [CONTAINER] to your Linux container name and [ALIAS] to the name you’d like to use for your new image.



# 3 Systen Configuration

## 3.1 enable nat on iptables
```
echo 1 > /proc/sys/net/ipv4/ip_forward
```
## 3.2 Auto Start Container
Set the container to start automatically when the LXC service starts – usually at host boot time. Use 1 to enable and 0 to disable.
```
lxc config set [CONTAINER_NAME] boot.autostart 1
```
## 3.3 Container Add Delay to boot start
You can also use boot.autostart.delay to set a delay in seconds after starting this container, before starting the next.
```
lxc config set [CONTAINER_NAME] boot.autostart.delay 30
```
## 3.4 Container Auto start order
Start up can be ordered using lxc.autostart.order to prioritise which containers are started first. Higher numbers are started first.
```
lxc config set [CONTAINER_NAME_1] boot.autostart.order 10
lxc config set [CONTAINER_NAME_2] boot.autostart.order 8
```


# 4. DO IT for every project you want a container for

# 4.1
lxc-create -t download -n my_project

# 4.2 if you want to share project's source (or maybe logs folder) with the host, sourceedit /var/lib/lxc/my_project/config and add the following
lxc.mount.entry = /home/user/Workspace/my_project my_project none default,bind 0 0

# 4.3 if you want to make available throught the host, execute the following (adapt the IP and PORT) and persist it!
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport {PORT} -j DNAT --to {IP}:{PORT}

# 5. DO IT every time you want

# 5.1 start your container
lxc-start -n my_project

# 5.2 if you need a shell, attach to the container
lxc-attach -n my_project

# 5.3 stop the container once you're done
lxc-stop -n my_project
