# Couchbase Development Workshop

This repository contains the material for a combined developer workshop. The following SDK-s are covered:

* C/C++
* Java


# Requirements

Each training computer should have at least the following HW configuration

* 4 CPU cores >=2GHz
* 8 GB RAM
* 50 GB free disk space

The following connectivity is expected:

* Internet access
* Access to Dropbox (alternatively the training material and environment can be provided on a network share in the LAN)

The following software needs to be installed on the attendee's computer:

* VirtualBox >= 4.3

The attendee should have all required permissions to create Virtual Machines and Virtual Machine networks on his box.


# Virtual Machine Setup

> We used usually 4-5 VM-s during this training. However, we usually had issues with the VM-s network connectivity during this workshop. So this time we will set up exactly 1 VM which will include all required components.

If you use the provided VM image, then you can skip the following steps:

* Create 64 Bit Linux VM in VirtualBox and call it 'Couchbase-Dev'
* Assign 3072 MB RAM to it
* Assign a 25GB disk to it
* Add the media 'CentOS-7-x86_64-DVD-1611.iso' (The DVD CentOS7 media from https://www.centos.org/download/)
* Start the VM, choose 'Install' and follow the installation instructions
* Set the root password to 'couchbase'
* Choose the 25GB disk with automatic partitioning
* Choose to create a user 'couchbase' and password 'couchbase' during the installation
* Wait for the installation to complete

## Configure the VM network

### NAT

The NAT interface should be there by default. The NAT IP is usually something like '10.0.2.15'. 

In order to enable access from the outside world via NAT, port forwarding can be used. So to simplify further configuration steps it makes sense to allow the access from the outside world to the VM via NAT and port forwarding. Under the network settings of the VM's NAT network define the following port forwardings:

| Name          | Host port        | Gest port |
| ------------- |------------------|---------- |
| SSH           |9122              | 22        |
| CB            |9191              | 8091      |
| VNC           |9159              | 5901      |







