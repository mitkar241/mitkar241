# container
---
## The difference between VMs and containers
---
The primary difference between Virtual Machines (VMs) and containers is that the former is more powerful, but the latter is faster.

## Introduction: How the Linux operating system works
---
Before we can discuss Virtual Machines and containers, we'll need to go over some preliminary knowledge about Linux.

In the very abstract, Linux keeps track of four things for programs that you run on it:

- Memory - used for storing local variables and the code of the program that is executing. Linux uses some of the memory itself (to store its own local variables, for example) and hands out most the rest to programs that are executing.
- CPU (processors) - used for running things in parallel. If you are playing music while browsing the internet, you might be using "120%" of a processor (meaning one full processor, and 20% of another)
- Disk - If you are reading or writing files, they are stored in the disk. In general, anything that stays around after you reboot the computer will be stored on the disk.
- Devices (GPU, network, etc) - used for various purposes like connecting to the internet and rendering graphics. Linux ensures that multiple programs can use the internet at the same time, or render to a monitor at the same time.

## How Virtual Machines and containers fit into things
---
In a usual Linux system, programs know about each other. One program could, for example, write to the file at /home/colin/file.txt and the other could read from it. A program could kill another simply by issuing a kill command.

This is generally fine - when you run Chrome and Spotify on your computer at the same time, you assume that one will not interfere with the other. Linux will allocate shared resources like memory and CPU fairly so that both programs can work properly, and they won't share any files in any way that breaks things.

However, there are often conflicts between shared resources in business software. If you have two programs that use the Python programming language, one might expect the file at "/usr/bin/python" to be an executable corresponding to Python v2.7, whereas another newer program might expect Python v3.6. In that case, there's no way to run both programs concurrently without changing the code of one of them.

Similarly, two webservers such as Apache and nginx might run on port 80 by default, so it'd be impossible to run both programs at once without changing their configuration files.

This is where Virtual Machines and containers are useful - they allow you to separate resources like files and ports between programs, so that programs can't "step on each others' feet"

## What happens when you put a program into a Virtual Machine or container
---
The big change for moving programs into containers or VMs is that each will have its own version of shared resources like files and network ports. The container running Chrome might create a file at ~/.chrome/cache while the container running Notepad would not see that file at all.

Similarly, one webserver could reserve port 80 concurrently with another. They'd both be reserving their ports within the scope of their VM/container, not within the entire operating system.

From our example above, the file at "/usr/bin/python" could contain Python 2.7 in one container, but contain Python 3.7 in another. They'd be different files, but each program would "see" a different executable at the same place.

With all this in mind, let's look at how containers and VMs are implemented at a very high level.

## How do containers work?

Containers work by creating "namespaces", which are a Linux feature that group shared resources together. For example, if you had five processes running together within a Docker container, they'd still be running within Linux itself (and they'd be visible in a task manager within Linux), but they would not see the processes in Linux:

Within the container, you might see 10 processes running within its "namespace"
```
root@web-6bd6bfc85b-lws8t:/# ps aux | wc -l
10
```
Within linux (outside the container), you see all 500+ processes, including the 10 above.
```
colin@colin-desktop:/$ ps aux | wc -l
577
```
Essentially, the programs are asking "what are the contents of /usr/lib/python" and instead of answering truthfully, Linux is answering with the contents of /var/lib/docker/overlayfs/1/usr/lib/python - this little deception allows programs to run in parallel, because Linux would respond with different files for every container.

## How do VMs work?
---
VMs are very similar to emulators. If you've ever seen older video games running on modern computers, they're using a VM.

If the idea for containers was to provide a "fake" version of Linux, the idea for VMs is to provide "fake" versions of the CPU, ram, disk, and devices. That is, VMs are "faking" one level deeper.

The VM equivalent of Docker is called a "hypervisor." It's the program which is in charge of creating the VMs themselves, so when a VM is running something it corresponds to an instance of a hypervisor on the "host" (Linux in the pictures above)

The hypervisor might "lie" to the VM and say "There is one SSD attached, it has 50GB of capacity", but the VM's writes to the "SSD", the write would instead go to a file in the host at /etc/disks/disk-1.qcow2.

VMs are very powerful, you can even use them to run other operating systems (such as MacOS or Windows) and different hardware configurations (like a GameCube or Apple II)

## Practical differences
---
To recap:

- In containers, it's the processes that are being "lied to", they must still have been the sort of thing that would've run in Linux.
- In VMs, there's a nested OS (Linux/mac/windows/game cube/...) that (generally) doesn't know it's not talking to real hardware. When that OS writes things to its drive for example, those writes are sent to a file in Linux instead of to a physical drive.

## Performance
---
- Various benchmarks show that the CPU in VMs is `10-20`% slower than containers.
- VMs also usually use `50-100`% more storage (containers don't need all of the files the operating system would need.)
- Finally, VMs use `~200mb` of memory each for the 'inner operating system', whereas containers have essentially no memory overhead.

Given these performance benefits, it looks like containers are always a better choice. In most cases, they are. However, there are a few cases where VMs are a better choice:

- If you are running untrusted (e.g., user supplied) code, it's difficult to be confident that they can't "escape" a container. This has gotten better in recent years, but it's long been a contentious point.
- If you are running, e.g., a Windows or MacOS guest within a Linux server, you'll need to use a VM for the mentions stated above.
- Finally, you can emulate hardware devices (like graphics cards) with a VM, but this is not a common use-case outside of very specific industry applications.
