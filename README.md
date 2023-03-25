# private_cloud_openstack_RDO
How to build a private cloud using openstack

<img width="533" alt="image" src="https://user-images.githubusercontent.com/76592289/227682132-a1e8ee43-20bb-4b2f-a433-b1998eeac707.jpg">

                                  
## A Project on how to build a private cloud using Openstack RDO.
OpenStack is a free, open standard cloud computing platform. It is mostly deployed as infrastructure-as-a-service in both public and private clouds where virtual servers and other resources are made available to users and in this project we will build Our Platform which includes full network topology and instances.
You can know more about openstack through the following link - https://docs.openstack.org/yoga/

## 1. Set Up Your Environment

In this project we used CentOS Stream 8-streamn, a single VM of MINIMUM 12 GB RAM, 2 CPUs and 2 NICs
FQDN of machine openstack.lab.local, so we should edit /etc/hosts file.

## 2. Machine preparation :
- Enabling nested virtualization

<img width="533" alt="image" src="https://user-images.githubusercontent.com/76592289/227681753-7411aab1-e8da-46ab-a7e7-cbaba1d34aec.png">

## 3. Operating System Installation :
During the installation of the CentOS OS. Move to Install CentOS Stream 8-stream and click tab on your keyboard.
Thin Type a space to separate than the last kernel option, type net.ifnames=0 biosdevname=0


<img width="533" alt="image" src="https://user-images.githubusercontent.com/76592289/227681824-fa0327f3-9797-48c0-a0db-16c866cc175a.png">
