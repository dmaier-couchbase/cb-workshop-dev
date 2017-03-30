   * [Couchbase Development Workshop](#couchbase-development-workshop)
      * [Requirements](#requirements)
      * [Virtual Machine Setup](#virtual-machine-setup)
         * [Configure the VM network](#configure-the-vm-network)
            * [NAT](#nat)
            * [Host only](#host-only)
            * [Network settings](#network-settings)
         * [Docker](#docker)
         * [Couchbase](#couchbase)
         * [Graphical User Interface](#graphical-user-interface)
         * [Java IDE](#java-ide)
         * [C/C++ IDE](#cc-ide)


         
# Couchbase Development Workshop

This repository contains the material for a combined developer workshop. The following SDK-s are covered:

* C/C++
* Java


## Requirements

Each training computer should have at least the following HW configuration

* 4 CPU cores >=2GHz
* 8 GB RAM
* 50 GB free disk space

The following connectivity is expected:

* Internet access
* Access to Dropbox (alternatively the training material and environment can be provided on a network share in the LAN)

The following software needs to be installed on the attendee's computer:

* VirtualBox >= 4.3
* Putty and WinSCP (Windows only)
* A VNC Viewer (https://github.com/TigerVNC/tigervnc/releases)

The attendee should have all required permissions to create Virtual Machines and Virtual Machine networks on his box.


## Virtual Machine Setup

> Instead of setting up 4-5 VM-s, we will set up exactly 1 VM which will include all required components.
> If you use the provided VM image, then you can skip the following steps BUT at least check if the network is configured correctly! More details about the network configuration can be found in the section 'Configure the VM network'.

Perform the following steps in order to create the Virtual Machine:

* Create 64 Bit Linux VM in VirtualBox and call it 'Couchbase-Dev'
* Assign 3072 MB RAM to it
* Assign a 25GB disk to it
* Change the CPU configuration to use at least 2 cores of your host machine
* Add the media 'CentOS-7-x86_64-DVD-1611.iso' (The DVD CentOS7 media from https://www.centos.org/download/)
* Start the VM, choose 'Install' and follow the installation instructions
* Set the root password to 'couchbase'
* Choose the 25GB disk with automatic partitioning
* Choose to create a user 'couchbase' and password 'couchbase' during the installation
* Wait for the installation to complete

### Configure the VM network

The following commands need to be executed as user 'root'

#### NAT

If you just want to access the outside world from within the VM then a NAT interface is enough. The NAT interface should be there by default. The NAT IP is automatically assigned and is usually something like '10.0.2.15'. 

In order to enable access from the outside world via NAT, port forwarding can be used. So to simplify further configuration steps it makes sense to allow the access from the outside world to the VM via NAT and port forwarding. Under the network settings of the VM's NAT network define the following port forwardings:

| Name          | Host port        | Gest port |
| ------------- |------------------|---------- |
| SSH           |9122              | 22        |
| CB            |9191              | 8091      |
| VNC           |9159              | 5901      |

Boot the VM and disable the firewall:
```
systemctl disable firewalld
systemctl stop firewalld
```

#### Host only

Host-only networking creates a network that is completely contained within the host computer. It allows us to connect to our VM without using Port forwarding.

* Power off the VM
* Under the VM settings add 'Adapter 2' and enable it
* Select 'Host-only Adapter' as the type
* If there is no global host-only network then you need to create it via the general Virtualbox preferences
* Power on the maching

#### Network settings

Your VM should now have two network cards. You can double check and change the settings by using the following tool:

```
nmtui
```

* Make sure that all network devices are enabled at startup and that they are available to all users
* Check the name server settings
* Change the host name to 'couchbase-dev.localdomain'
* Show your IP addresses:
```
ip addr show
```

> In my case the NAT interface had the IP address 10.0.2.15 and the host only network was 192.168.56.101

* Make sure that you have access to the internet. The following ping should return a response:
```
ping 8.8.8.8
ping google.com
```

### Docker

> Instead of dealing with multiple VM-s, we will use Docker containers within the VM in order to do the clustering exercises

The following steps can be performed to run a Couchbase instance via Docker:

* Install Docker as 'root' user:
```
yum install docker
systemctl start docker
systemctl enable docker
```

* Start 3 Couchbase instances
```
docker run -d --name couchbase-1 -p 8091-8094:8091-8094 -p 11210-11211:11210-11211 couchbase
docker run -d --name couchbase-2 couchbase
docker run -d --name couchbase-3 couchbase
```

This downloads and runs the latest Couchbase container. The first container will be accessible from the outside world.

* Retrieve the container's internal IP addresses and note them down:
```
inspect couchbase-$i | grep IPAddress
```

Access the Couchbase UI via the Host-Only IP
```
http://192.168.56.101:8091/
```

Remember, the first node exposes port 8091 and so it's possible to access it via the docker host's name on this port.

You should see Couchbase's setup dialog.

* Testwise create a 3 node cluster via the UI on the first node 

Use the internal IP-s of the docker containers as host names of your cluster nodes!

* Stop the containers
```
docker stop couchbase-1
docker stop couchbase-2
docker stop couchbase-3
```

* Delete the containers
```
docker rm couchbase-1
docker rm couchbase-2
docker rm couchbase-3
```

* Create the containers again
```
docker run -d --name couchbase-1 -p 8091-8094:8091-8094 -p 11210-11211:11210-11211 couchbase
docker run -d --name couchbase-2 couchbase
docker run -d --name couchbase-3 couchbase
```

* Double check that the containers are running
```
docker ps
```

* Check if you can access the Couchbase CLI
```
docker exec -it couchbase-1 /bin/bash
```

* Test if all nodes are reachable
```
curl http://172.17.0.2:8091/pools/
curl http://172.17.0.3:8091/pools/
curl http://172.17.0.4:8091/pools/
```
> Whereby the IP-s above need to be replaced with the internal container IP-s of your Couchbase containers

The result should look like this:
```
{"isAdminCreds":true,"isROAdminCreds":false,"isEnterprise":true,"pools":[],"settings":[],"uuid":[],"implementationVersion":"4.6.1-3652-enterprise","componentsVersion":{"lhttpc":"1.3.0","os_mon":"2.2.14","public_key":"0.21","asn1":"2.0.4","kernel":"2.16.4","ale":"4.6.1-3652-enterprise","inets":"5.9.8","ns_server":"4.6.1-3652-enterprise","crypto":"3.2","ssl":"5.3.3","sasl":"2.3.4","stdlib":"1.19.4"}}
```
* Stop all containers again

```
docker stop couchbase-1
docker stop couchbase-2
docker stop couchbase-3
docker ps
```

### Couchbase

One exercise will be to install Couchbase Server w/o using the Docker image, which means that we need to Download and verify the rpm file.

* Download the RHEL7/CentOS7 installation package
```
yum install wget
cd --
mkdir Downloads
cd Downloads
wget https://packages.couchbase.com/releases/4.6.1/couchbase-server-enterprise-4.6.1-centos7.x86_64.rpm
```

* Install Couchbase Server
```
rpm -ivh couchbase-server-enterprise-4.6.1-centos7.x86_64.rpm
```

* Check the service status
```
systemctl status couchbase-server | grep Active
```

* Verify that you can access the Admin UI
```
http://192.168.56.101:8091
```

* Stop Couchbase
```
systemctl stop couchbase-server
```

* Uninstall Couchbase again
```
rpm -e couchbase-server
```

* Remove the old installation directory
```
rm -Rf /opt/couchbase/
```

> Leave the installation package under /root/Downloads/ !

### Graphical User Interface

We want to do some Development exercises on the VM, so we need a way to access a graphical user interface.

* Install 'Epel'
```
yum install epel-release
```

* Install X
```
yum groupinstall "X Window system"
```

* Install XFCE Desktop Environment
```
yum groupinstall xfce
```

* Install a VNC server
```
 yum install tigervnc-server
```

* Set VNC password for user root to 'couchbase'
```
vncpasswd
```

* Modify the VNC startup file
```
vi /root/.vnc/xstartup
```

* Add the Desktop Environment to the VNC startup
```
#!/bin/sh

unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
#exec /etc/X11/xinit/xinitrc
exec /usr/bin/startxfce4
```

* Start the VNC server
```
vncserver :1 -geometry 1280x1024
```

> The VNC Server can be stopped by using the command 'vncserver -kill :1'

* Use a VNC client to connect to the UI (The password is 'couchbase')

### Java IDE

* Install Maven
```
yum install maven
```

* Download the JDK installation package from Oracle's web site (jdk-8u121-linux-x64.tar.gz from http://www.oracle.com/technetwork/java/javase/downloads/) and place it under '/root/Downloads'

* Install the JDK
```
cd /root/Downloads
tar -xvf jdk-8u121-linux-x64.tar.gz
mv jdk1.8.0_121 /opt/jdk
echo ' ' >>  /root/.bash_profile
echo 'export PATH=/opt/jdk/bin:$PATH' >> /root/.bash_profile
echo 'export JAVA_HOME=/opt/jdk' >> /root/.bash_profile
source /root/.bash_profile
```
    
* Double check the version
```
java -version
```

This should return:
```
Java HotSpot(TM) 64-Bit Server VM (build 25.121-b13, mixed mode)
```

* Download Netbeans from https://netbeans.org/downloads/ to '/root/Downloads'

> I used the full distribution

* Change the script 'netbeans-8.2-linux.sh' to be executable
```
chmod +x netbeans-8.2-linux.sh 
```

* Log-in to the graphical user interface and install Netbeans under /opt/netbeans
```
./netbeans-8.2-linux.sh 
```

This might take a while.

> I installed Glassfish to /opt/glassfish

* Ensure that Netbeans uses the right JDK by investigating the file /opt/netbeans/netbeans.conf

```
netbeans_jdkhome="/opt/jdk"
```

If not then set the right SDK!


* Start Netbeans

```
/opt/netbeans/bin/netbeans-8.2-linux.sh 
```

Or use the the Desktop libk 'Netbeans 8.2'

* Create an empty Maven Java project and build it

### C/C++ IDE

* Install the development tools
```
yum groupinstall 'Development Tools'
```

* Install Qt5
```
yum install qt5-* --skip-broken
```

> This worked in CentOS 6 w/o the flag --skip-broken. Let's hope the best.

* Install the Qt-Creator
```
yum install qt-creator
```

* Log-in to the graphical user interface and run Qt-Creator
```
TODO
```
