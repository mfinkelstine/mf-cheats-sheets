# Linux Containers CheatSheat

## Table of Contents
1. [What is Containers](#Whatis-containers)
2. [Containers vs Dockers](#containervsdockers)
3. [LXC list Commands](#lxclistcommands)
4. [test](#aaa)

## What is Containers

LXC (Linux Containers) is an operating-system-level virtualization method for running multiple isolated Linux systems (containers) on a control host using a single Linux kernel.

The Linux kernel provides the cgroups functionality that allows limitation and prioritization of resources (CPU, memory, block I/O, network, etc.) without the need for starting any virtual machines, and also namespace isolation functionality that allows complete isolation of an applications' view of the operating environment, including process trees, networking, user IDs and mounted file systems.[3]

LXC combines the kernel's cgroups and support for isolated namespaces to provide an isolated environment for applications. Docker can also use LXC as one of its execution drivers, enabling image management and providing deployment services.

- Overview

  LXC provides operating system-level virtualization through a virtual environment that has its own process and network space, instead of creating a full-fledged virtual machine.
  LXC relies on the Linux kernel cgroups functionality that was released in version 2.6.24. It also relies on other kinds of namespace isolation functionality, which were developed and integrated into the mainline Linux kernel.

- Security

  Originally, LXC containers were not as secure as other OS-level virtualization methods such as OpenVZ: in Linux kernels before 3.8, the root user of the guest system could run arbitrary code on the host system with root privileges, much like chroot jails.
  Starting with the LXC 1.0 release, it is possible to run containers as regular users on the host using "unprivileged containers".
  Unprivileged containers are more limited in that they cannot access hardware directly. Nevertheless, even privileged containers should provide adequate isolation in the LXC 1.0 security model, if properly configured.

## Containters vs Dockers

## LXC list Commands

```bash
root at lxcos in ~$
lxc-attach           lxc-clone            lxc-destroy          lxc-info             lxc-start            lxc-unfreeze
lxc-autostart        lxc-config           lxc-device           lxc-ls               lxc-start-ephemeral  lxc-unshare
lxc-cgroup           lxc-console          lxc-execute          lxc-monitor          lxc-stop             lxc-usernsexec
lxc-checkconfig      lxc-create           lxc-freeze           lxc-snapshot         lxc-top              lxc-wait
```

- some useful command to manage LXC:
  - List Containters and summmery information
  ```bash
  # lxc-ls --fancy
  ```
  command output

   ```bash
   $ lxc-ls --fancy
   NAME  STATE  IPV4  IPV6  AUTOSTART  
   ----------------------------------
  ```

  - Check LXC Configuration

    check the current kernel for lxc support

    ```bash
    # lxc-checkconfig
    ```

    command output

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
usage : CONFIG=/path/to/config /usr/bin/lxc-checkconfig
  ```

- Creating Container

  lxc-create  creates a container object where is stored the configuration information and where can be stored user information.
  The identifier name is used to specify the container to be used with the different lxc commands.

  The object is a directory created in /var/lib/lxc and identified by its name.

  command with flags:

  > lxc-create {-n name} [-f config_file] {-t template} [-B backingstore] [-- template-options]

  command line

  ```bash
  lxc-create -t download -n u1
  or
  lxc-create -n <container-name> -t <template>
  ```

  example

  ```bash
  lxc-create -t download -n u1 -- --dist ubuntu --release xenial --arch amd64
  or
  lxc-create -t download -n u1 -- -d ubuntu -r xenial -a amd64
  ```

- list containters

  ```bash
  lxc-ls
  ```
