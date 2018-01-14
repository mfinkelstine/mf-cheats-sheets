# LXC Cookbook 
All LXC commands have to be run as root or use sudo command

## The LXC Basics

### LXC #1: Installation & Configuration Procedure

##### 1.1 install lxc on centos & ubuntu
- Install lxc on centos
```
root at lxc-sys in ~$ : yum install -y lxc lxc-devel lxc-doc lxc-extra lxc-libs lxc-templates
yum install libcap-devel libcgroup busybox wget bridge-utils
```
- Installing lxc on Ubuntu OS
```
apt-get install lxc 
```

##### 1.2 LXC Check Configuration
- To check [LXC] configuration use this command
```
lxc-checkconfig
```

##### 1.3 LXC Configure Networking

create the bridge network for lxc to have network

