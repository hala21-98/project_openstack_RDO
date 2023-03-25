# private_cloud_openstack_RDO
How to build a private cloud using openstack

<img width="800" alt="image" src="https://user-images.githubusercontent.com/76592289/227682132-a1e8ee43-20bb-4b2f-a433-b1998eeac707.jpg">

                                  
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
1. During the installation of the CentOS OS. Move to Install CentOS Stream 8-stream and click tab on your keyboard.
Thin Type a space to separate than the last kernel option, type net.ifnames=0 biosdevname=0


<img width="800" alt="image" src="https://user-images.githubusercontent.com/76592289/227681824-fa0327f3-9797-48c0-a0db-16c866cc175a.png">

This will enable old Linux NIC card naming (eth0, eth1, …etc).

2. Now you see the installation screen, Click on Network & Host.

<img width="420" alt="image" src="https://user-images.githubusercontent.com/76592289/227682265-ecd6c7f2-dceb-472f-86d5-a97ab0df31a4.png">

2.1 First step we need to set the Host Name,

<img width="420" alt="image" src="https://user-images.githubusercontent.com/76592289/227682323-4a5bf1cf-37ed-4b4d-bb94-a0da8cdf42bb.png">

2.2 Now, the network card got an IP from the DHCP. configure the IP manually by clicking configure. Give the card the same fetched configuration from DHCP.
     >> Disable IPV6 and configure IPV4
     
<img width="420" alt="image" src="https://user-images.githubusercontent.com/76592289/227682445-502819db-cf30-4523-acd2-1677dc878f40.png">

2.3 Select the Installation Destination and choose your HDD, just click to Done button if u just have one HDD.

2.4 Click the Time and Date button and select Cairo as your local time zone, Make sure that NTP on the top right is enabled, click on the gear icon and wait for a moment to make sure it is syncing with centos public NTP servers.

2.5 For Software Selection, please, select Server with GUI

2.6 create root password,

2.7 create user and make him Admin,

3. Once all are set. Begin the OS installation.

4. When the installation is over Reboot and Accept the Licenses,

## 4. Prerequisites Deployment:

As a prerequisite, you have to install the needed repos and Adding to that, you must disable some services and enable the legacy network service.
The below section illustrates the actions we have to follow:
Firstly, we need to check the hostname, and check if we can reach the internet or not, and switch to be root.

1. Switch to root,

<img width="420" alt="image" src="https://user-images.githubusercontent.com/76592289/227682865-001f0fa0-b3d2-47dd-8087-c3ef86d5ee12.png">

2. Add the hostname to /etc/hosts and make an alias for it,

<img width="420" alt="image" src="https://user-images.githubusercontent.com/76592289/227683541-db6ba19a-08d2-479f-a336-9c74aac57a8a.png">

3. Disable and stop firewalld

<img width="420" alt="image" src="https://user-images.githubusercontent.com/76592289/227684180-7832b68b-adbe-41d5-aacd-9047ce67835c.png">

4. Disable SeLinux

sed -i 's/SELINUX=.*/SELINUX=disabled/' /etc/selinux/config

<img width="420" alt="image" src="https://user-images.githubusercontent.com/76592289/227685054-b0e9b7b0-d5fb-498f-abfa-ec8c652b009f.png">

5. Disable and stop Networkmanager

<img width="420" alt="image" src="https://user-images.githubusercontent.com/76592289/227685745-8d31dd68-a85b-472d-b121-f260cd7d371b.png">

6. Download network-scripts

<img width="420" alt="image" src="https://user-images.githubusercontent.com/76592289/227685998-32074c90-72b0-436e-9da2-58d009619acb.png">

7. Enable and Start network-scripts

<img width="420" alt="image" src="https://user-images.githubusercontent.com/76592289/227688020-8630af38-0e9e-4ab5-a5d1-de3b00c1d4bc.png">

8. Enable power tools and install yoga,

<img width="420" alt="image" src="https://user-images.githubusercontent.com/76592289/227688059-0b458126-e537-42c5-ad58-6ad078467088.png">

9. Update the system,
```
dnf -y update
```
10. Install Packstack

<img width="420" alt="image" src="https://user-images.githubusercontent.com/76592289/227688823-3f62669d-f64b-42fc-943b-ccd2b3dfcf95.png">

11. Generate answer file,
```
packstack --gen-answer-file=/root/answers.txt --os-neutron-l2-agent=openvswitch 
--os-neutron-ml2-mechanism-drivers=openvswitch --os-neutron-ml2-tenant-network-types=vxlan --os-neutron-ml2-type-drivers=vxlan,flat 
--provision-demo=n --os-neutron-ovs-bridge-mappings=extnet:br-ex --os-neutron-ovs-bridge-interfaces=br-ex:eth0 
--keystone-admin-passwd=redhat --os-heat-install=n
```
<img width="420" alt="image" src="https://user-images.githubusercontent.com/76592289/227688975-6e84bfe8-ec82-44e7-8bbd-8c2ca8b380c0.png">

12. Start the installation,

<img width="420" alt="image" src="https://user-images.githubusercontent.com/76592289/227689149-34e37516-f03c-433c-8130-6dfff788afc2.png">

Wait for the installation to finish, you can access the openstack dashboard browse to 192.168.140.131

<img width="420" alt="image" src="https://user-images.githubusercontent.com/76592289/227689545-0e1d9fe6-d7ef-4aa2-b88f-ea303e79f718.jpg">

## 5. Validation:

open the dashboard in your browser, and enter the User Name and the password to Sign In.

<img width="420" alt="image" src="https://user-images.githubusercontent.com/76592289/227689810-d28657c5-bf6b-4605-812e-34bd5735394d.PNG">

<img width="420" alt="image" src="https://user-images.githubusercontent.com/76592289/227689951-9dead25a-d272-4d8b-92f7-50bd73e70d1d.PNG">

1. Install image file and Create image using glance component:

```
curl -L http://download.cirros-cloud.net/0.3.4/cirros-0.3.4-x86_64-disk.img | glance image-create --name='cirros image' --visibility=public --container-format=bare --disk-format=qcow2
```
>> CirrOS is a minimal Linux distribution that was designed for use as a test image on clouds such as OpenStack Compute.

<img width="420" alt="image" src="https://user-images.githubusercontent.com/76592289/227719344-2b403d30-5e61-4ccd-af05-96ddc88cb12f.png">

1.1 validate the image from the GUI

>> project->compute->images

<img width="520" alt="image" src="https://user-images.githubusercontent.com/76592289/227719563-b3518cc1-c485-4c91-a4ff-4a99cc2d7f61.png">

2. create the Instance 

```
openstack server create --image 'cirros image' --flavor m1.tiny --network Internal server2
```

<img width="520" alt="image" src="https://user-images.githubusercontent.com/76592289/227735989-d6d9445f-5ea6-4790-8fae-dd217c112517.png">

2.1 validate the instance from the GUI

<img width="520" alt="image" src="https://user-images.githubusercontent.com/76592289/227736139-b3f6a1c1-d370-4e19-9adb-9ac9bbe97a75.png">

2.2 Create FloatingIP, to reach our instance from the Internet

<img width="520" alt="image" src="https://user-images.githubusercontent.com/76592289/227721716-b9d7e946-2c7a-496a-aaed-3bbe7710cd5f.png">

2.3 Assign the FloatingIP to the Instance_Port

>> We know the IP for this Instance from GUI

<img width="520" alt="image" src="https://user-images.githubusercontent.com/76592289/227722152-a774b449-d960-42f5-974d-22090790ac20.png">

<img width="520" alt="image" src="https://user-images.githubusercontent.com/76592289/227722547-c7cf6386-c287-4938-b8eb-65ad2d1a5b14.png">

Then let’s assigen the FloatingIP for the Instance Port

<img width="520" alt="image" src="https://user-images.githubusercontent.com/76592289/227735760-12f5cfe6-1d97-46f9-90a7-64ea337aae59.png">

Validate the Instance from the GUI:

<img width="520" alt="image" src="https://user-images.githubusercontent.com/76592289/227735811-77bffe55-bfa3-4285-b227-f1d6335e141f.png">

3. Add two rules in the default security group to enable ssh port and ICMP

>> Project→ Network→ Security Groups → Manage Rule

<img width="520" alt="image" src="https://user-images.githubusercontent.com/76592289/227723242-88d9da4e-198c-41d5-9817-77fb16284463.png">

<img width="520" alt="image" src="https://user-images.githubusercontent.com/76592289/227723332-143096ba-60cc-424c-bb7a-34a0e4d67945.png">

validate two rules added

<img width="520" alt="image" src="https://user-images.githubusercontent.com/76592289/227723506-781e77e7-4917-430a-83cf-1eda801c648d.png">














































