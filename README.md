# **How to connect to a remote Linux computer** <br />


Working with large datasets requires a greater computational power than an average laptop. You can subscribe to the vendors providing with the high performance computing (HPC) services or set up your own HPC facility. In any case, you will need to connect your laptop to your HPC machine using a ‘ssh client’ for transferring data back and forth. 


## **What is a ‘ssh client’?**


First, what is ‘ssh’? ‘ssh’ elaborated as ‘Secure Shell’ is a network communication protocol used for connecting two computers and exchanging data between them. And the softwares that allow for ssh connection is called ‘ssh clients’. All major operating systems such as Linux, Mac or Windows have built-in ssh clients. Furthermore, MobaXterm and Putty are two widely used external ssh clients for Windows computers. 


You can quickly check if your laptop or desktop has a ssh client:

- open a terminal
- run the following command
```
ssh
```


If you see something like Fig 1, then you have a ssh client in your computer.
<br />
<br />
<br />
<p align="center">
  <img 
    src="https://github.com/asadprodhan/How-to-connect-to-a-remote-Linux-computer-/blob/main/ssh_flags.PNG"
  >
<p align = "center">
Figure 1. ssh client 
</p>
<br />


## **How to establish ssh connection between your laptop and your HPC machine?**


In your local computer (laptop/desktop), you run the following command line to connect to your remote computer (HPC machine) (Fig 2):


```
ssh userName@IP_address_of_your_HPC_machine
```



> You will need to find the IP address of your HPC machine. Generally, the HPC service providers will provide you with it. However, if it is your own HPC facility (Linux machine), then you will need to find this IP address on your own. 
<br />


**This tutorial is all about how to find the IP address of your Linux machine and establish a ssh connection. See the descriptions below.**

<br />
<br />
<p align="center">
  <img 
        src="https://github.com/asadprodhan/How-to-connect-to-a-remote-Linux-computer-/blob/main/RemoteConnection_v2.png"
  >
<p align = "center">
Figure 2. Connecting to the remote computer using ssh
</p>
<br />
<br />


### **Find the IP address of your Linux machine**



**I.	First, find the IP address of your network**


- open a terminal in your Linux machine

- run one of the following commands  


```
ifconfig
```


***Or,***



```
ip address
```


>It will be something like ‘inet 192.168.1.29’ listed under 'eno1'. **The first three numbers constitute the IP address of your network.**


> Note that 'eno1' can be named as tho, eth1, eth2, enp4s0 or enpXXX1f6 etc depending on the driver that runs the ethernet network interface device in your Linux machine.


> The ethernet or wireless network interfaces are required for connecting your Linux machine to ethernet or wireless based internet, respectively



**II.	Find the IP address of your Linux machine**


>To do so, you need to scan the network. ‘nmap’ (Network Mapping) is an open-source network scanner that discovers the devices connected to a given network.


- install ‘nmap’ by running the following command in your terminal

```
sudo apt-get install nmap
```


- then, scan your home network using its IP address as follows:


```
sudo nmap -sn 192.168.1.0/24
```


This will show the IP addresses of the devices that are connected to the network ID 192.168.1. 


>Note that the first three numbers are the network ID. ‘0/24’ indicates that the host IDs can range from 0 to 256 (this is a conversion from binary to decimal numbers. In brief, the whole IP address can be up to 32 bits, 8 for each number. '0/24' in the place of the host ID indicates that 24 bits have already been used in the network ID, and thus the host ID can have up to 8 bits, which is 0 to 256 in decimal number).


- Find your device in the list and collect its IP address


**Establish a ssh connection**



**Now, you have the IP address of your Linux machine- say, 10.65.37.96. Let’s ‘ssh’ from your local computer (laptop/desktop) to your remote computer (Linux machine) as follows**


- open a terminal in your local computer


- run the following command


```
ssh userName@10.65.37.96
```


***Done! ssh connection is now established allowing you to use your remote computer/server from your local computer.***

<br />
<br />

**Troubleshooting**


***ssh connection over two different networks, i.e. local and remote computers are on different networks***


In this case, if the ssh connection cannot be established and there is a ‘connection time out’ message; then it is worth trying the following troubleshooting:


- rebooting the internet router


- checking the router setting if it is blocking the ssh connection



**How to allow ssh connection on my internet router?**


- open a browser


- enter 192.168.1.X (replace ‘X’ by the router serial number; most cases it’s 1)


- then navigate to the 


> security settings > access control > WAN (if the remote computer on WiFi) or LAN (if the remote computer is on ethernet) > turn on ‘allow’ against ssh 


- then, 


> application settings > port forwarding > applications > ssh server > internet client > select your device from the list of devices > press ‘add’


- then


> **go to the router home tab > collect the IP address of your newly 'added' device and use this IP address for ssh connection**



```
ssh userName@your_device_IP_address_collected_from_the_router
```


More devices can be added in the same way for remote ssh connection.

