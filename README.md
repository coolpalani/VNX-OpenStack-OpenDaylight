# VNX-OpenStack-OpenDaylight

This project is an extension of [VNX OpenStack Ocata tutorial](https://github.com/davidfdezc/vnx-lab-openstack-ocata/tree/master/openstack_lab-ocata_4n_classic_ovs) where open source SDN platform OpenDaylight is integrated to work as backend of OpenStack's Networking service Neutron.

## Requirements

 - VNX installed [(VNX Installation Guide)](http://web.dit.upm.es/vnxwiki/index.php/Vnx-install-ubuntu3)
 - Operating System: Ubuntu 14.04 / Ubuntu 16.04 (Recommended)

## Installation

Build all filesystems required by the nodes to be deployed:

```shell
sudo sh filesystems/build-filesystems
``` 

## Description

This VNX scenario is composed of the following nodes:

 - one controller
 - one network node
 - one SDN controller (OpenDaylight)
 - two compute nodes

For this deployment we are using the following software versions:

 - OS (for all nodes): Ubuntu 16.04 LTS
 - OpenStack: Ocata
 - OpenDaylight: Boron SR3

## Usage 

First of all, create the scenario using the following command:

```shell
sudo vnx -f openstack_lab-ocata-boron.xml -v --create
```

After a couple of minutes (startup process of the nodes takes some time when creating the virtual scenario) run the following command to configure OpenStack in our scenario:

```shell
sudo vnx -f openstack_lab-ocata-boron.xml -v -x step1-6
```

Load all necessary images on Glance for the VMs that we will boot later:

```shell
sudo vnx -f openstack_lab-ocata-boron.xml -v -x load-img
```

Start OpenDaylight controller:

```shell
sudo vnx -f openstack_lab-ocata-boron.xml -v -x start-odl
```

Configure all nodes to work with OpenDaylight as a backend of Neutron:

```shell
sudo vnx -f openstack_lab-ocata-boron.xml -v -x start-boron
```

Deploy an example scenario with two subnets with two VMs per subnet, connected to each other with a virtual router. This router will also be attached to an external network so the VMs can connect to the Internet. Currently, only vm1 is able to reach external networks as it has a floating IP associated. To create such scenario run the following command:

```shell
sudo vnx -f openstack_lab-ocata-boron.xml -v -x create-odl-scenario
```

Finally, to destroy this VNX scenario run:

```shell
sudo vnx -f openstack_lab-ocata-boron.xml -v --destroy
```

## References

 -  [VNX Website](http://web.dit.upm.es/vnxwiki/index.php/Main_Page)
 -  [OpenDaylight Website](https://www.opendaylight.org)
 -  [Netvirt + OpenStack guide](http://docs.opendaylight.org/en/stable-boron/submodules/netvirt/docs/openstack-guide/openstack-with-netvirt.html)
 -  [networking-odl ML2 driver](https://docs.openstack.org/networking-odl/latest/index.html)
