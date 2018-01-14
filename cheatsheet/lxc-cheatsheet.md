# LXC Cookbook 
All LXC commands have to be run as root or use sudo command

## The LXC Basics

### LXC #1: Installation & Configuration Procedure

##### 1.1 Installing LXC on centos & ubuntu
- Install lxc on centos

 ```bash
root at lxc-sys in ~$ : yum install -y lxc lxc-devel lxc-doc lxc-extra lxc-libs lxc-templates
yum install libcap-devel libcgroup busybox wget bridge-utils
```

- Installing LXC on Ubuntu OS

 ```bash
 apt-get install lxc 
 ```
