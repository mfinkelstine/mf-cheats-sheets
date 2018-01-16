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
##### 1.2 LXC Check Configuration
- To check [LXC] configuration use this command
 
 ```bash
  lxc-checkconfig
 ```

- lxc-checkconfig output :

 ```bash
$ lxc-checkconfig 
Kernel configuration not found at /proc/config.gz; searching...
Kernel configuration found at /boot/config-3.10.0-693.11.1.el7.x86_64
--- Namespaces ---
Namespaces: enabled
Utsname namespace: enabled
Ipc namespace: enabled
Pid namespace: enabled
User namespace: enabled
newuidmap is not installed
newgidmap is not installed
Network namespace: enabled
Multiple /dev/pts instances: enabled
 
--- Control groups ---
Cgroup: enabled
Cgroup clone_children flag: enabled
Cgroup device: enabled
Cgroup sched: enabled
Cgroup cpu account: enabled
Cgroup memory controller: enabled
Cgroup cpuset: enabled

--- Misc ---
Veth pair device: enabled
Macvlan: enabled
Vlan: enabled
Bridges: enabled
Advanced netfilter: enabled
CONFIG_NF_NAT_IPV4: enabled
CONFIG_NF_NAT_IPV6: enabled
CONFIG_IP_NF_TARGET_MASQUERADE: enabled
CONFIG_IP6_NF_TARGET_MASQUERADE: enabled
CONFIG_NETFILTER_XT_TARGET_CHECKSUM: enabled

--- Checkpoint/Restore ---
checkpoint restore: enabled
CONFIG_FHANDLE: enabled
CONFIG_EVENTFD: enabled
CONFIG_EPOLL: enabled
CONFIG_UNIX_DIAG: enabled
CONFIG_INET_DIAG: enabled
CONFIG_PACKET_DIAG: enabled
CONFIG_NETLINK_DIAG: enabled
File capabilities: enabled

Note : Before booting a new kernel, you can check its configuration
usage : CONFIG=/path/to/config /bin/lxc-checkconfig

```

##### 1.3 LXC Configure Networking
