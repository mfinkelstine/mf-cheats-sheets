# Linux Containers CheatSheat

## Table of Contents
1. [What is Containers](#What is containers)
2. [Containers vs Dockers](#container sv dockers)
3. [LXC Command list](#lxc command list)
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

## LXC Commad list

```bash
root at lxcos in ~$ 
lxc-attach           lxc-clone            lxc-destroy          lxc-info             lxc-start            lxc-unfreeze
lxc-autostart        lxc-config           lxc-device           lxc-ls               lxc-start-ephemeral  lxc-unshare
lxc-cgroup           lxc-console          lxc-execute          lxc-monitor          lxc-stop             lxc-usernsexec
lxc-checkconfig      lxc-create           lxc-freeze           lxc-snapshot         lxc-top              lxc-wait


```
