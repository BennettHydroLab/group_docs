# Computing resources

This page provides links to common computing platforms that the group uses. For information about how to configure your environment see [this page](computing_environments.md).

## Group server (`ocotillo`)

The group maintains a separate computing server that has the following resources:

- 2x AMD Epyc 7763 64 Core CPU
- 1 TB system memory (RAM)
- 8x NVIDIA RTX A6000 Ada GPU
- 50 TB storage

It can be accessed from `ocotillo.has.arizona.edu` while on the UA network or VPN. You will need to have an account manually set up to access `ocotillo`. If you haven't had this happen already, talk to Andrew to set up a meeting to gain access.

!!! note

    Usage of this system is unmanaged, and it is expected that you are concious of your resource usage. If you are going to be running large jobs on this system that take significant resources (i.e. >500 GB memory, > 32 cores, or >2 GPUs), please coordinate your runs via our slack channel.

### Accessing `ocotillo` from outside of UA
To access outside of the UA network we suggest setting an entry in your ssh config as:
```
Host ocotillo
    User <your_username>
    HostName ocotillo.has.arizona.edu
    ProxyJump filexfer.hpc.arizona.edu
    LocalForward <port1> localhost:<port1>
    LocalForward <port2> localhost:<port2>
    ControlMaster auto
    ControlPersist yes
```

This will do a "proxy jump" through the file transfer server from the UA HPC center. You will need a UA HPC account for this to work. You can set as many port forwards as you would like, depending on how many simultaneous web apps you tend to monitor. If you set up passwordless login via ssh-keys make sure to set up passwordless login for both `filexfer.hpc.arizona.edu` and `ocotillo.has.arizona.edu` separately.

## UA High Performance Computing (HPC)

The University of Arizona runs the High Performance Computing systems that all students, staff, and faculty are able to use. For more detailed information about available resources see the [UA HPC Documentation website here](https://hpcdocs.hpc.arizona.edu/).

When signing up for an account use Andrew's email as your sponsor.

### Tips for streamlining UA HPC access

The default setup on the UA HPC system is a bit unconventional and can make standard workflows awkward to run. This is due to there being the "bastion" node which is separate from the "login" node, meaning when you first ssh to `hpc.arizona.edu` you cannot get right on with work, but have to choose a default system to jump to. This can be worked around by jumping directly to the `junonia` server. We use a similar method to accessing `ocotillo` by jumping through the file transfer server. You can still switch systems using their respective named commands (e.g. `puma` or `ocelote`). This can be accomplished by setting up your ssh config:

```
Host junonia
    User <your_username>
    HostName junonia.hpc.arizona.edu
    ProxyJump filexfer.hpc.arizona.edu
    LocalForward <port1> localhost:<port1>
    LocalForward <port2> localhost:<port2>
    ControlMaster auto
    ControlPersist yes
```

### Some helpful aliases to set up

### Accessing jupyter servers running in interactive sessions from VSCode

## CyVerse

## Free resources

### Google Colab

### GitHub Spaces

### Binder

## Cloud computing (paid)

### Runpod

### Google, Amazon, Microsoft