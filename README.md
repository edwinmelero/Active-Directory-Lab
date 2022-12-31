# Active-Directory-Lab
This is a lab exercise to produce an Active Directory similar to a mini corporate environment. 

This diagram below shows an overview to visualize how the network is setup.
![Active Directory Lab](https://user-images.githubusercontent.com/105263523/210102488-779ac67d-e1b1-41b0-bac3-da7cf548cc90.png)


I used Oracle VM VirtualBox to setup the Domain Controller where it will house the Active Directory. The Domain Controller has two network adapters which will connect to the outside internet and the other will connect to the private network which the Client will be connecting to. I installed Server 2019 ISO on the virtual machine and assigned IP addressing for the internal network. I named the server DC, short for Domain Controller, installed Active Directory and created a domain (mydomain.com). Then I configured the routing and NAT (RAS/NAT) so the clients on the private network can access the internet through the Domain Controller. I then setup the DHCP on the DC so that when the Windows 10 Virtual Machine gets created it can automatically assign an IP address. After the network has been setup I then ran a PowerShell script that automatically created 1,000+ users in Active Directory. Lastly I created a new virtual machine, installed Windows 10 and renamed it Client1. I joined the client to the private network and logged in using one of the user accounts created.


The Domain Controller network adapter 1 is attached to NAT.

![AdapterNAT](https://user-images.githubusercontent.com/105263523/210120339-36638625-42eb-4119-88d5-6af05b359619.png)


Enable network adapter 2. Attach to the Internal Network.

![Adapter2internalnetwork](https://user-images.githubusercontent.com/105263523/210122140-277936c0-faff-4a12-a3fe-84b2afa8f864.png)


Renamed Network connections.

![Network Connections](https://user-images.githubusercontent.com/105263523/210125465-eafa2e63-cd75-4a5e-b2b6-92fed755b1a0.PNG)


Running on the DC, after Server 2019 ISO installation, I installed the Server Roles: Active Directory Domain Services, DHCP Server and DNS Server.

![server roles installed](https://user-images.githubusercontent.com/105263523/210124300-739a1b0f-a60f-486c-b93f-42c1a850f330.png)


Created an Organizational Unit and named it _ADMINS. Created my admin account username: a-emelero and passowrd: Password1.

![OUAdmin](https://user-images.githubusercontent.com/105263523/210124918-6842f1ca-4d88-4ab1-b3d2-beb6517cc915.png)


Configured Routing.

![Routing](https://user-images.githubusercontent.com/105263523/210126223-377cf711-2493-41df-8673-c64a88102a88.png)


DHCP Scope. IP Address Range 172.16.0.100-200 

![DHCP](https://user-images.githubusercontent.com/105263523/210128337-f33a4fb7-ec73-424a-83ac-fd341513cbc1.PNG)


Ran PowerShell as Administrator. Set Execution Policy to unrestricted to enable all scripts on server to avoid error. Change directory command line prompt to where file of users is stored. List directory to show .\names.txt file is there. This is the file that contains the names of the users we will be creating.

![Powershell commands](https://user-images.githubusercontent.com/105263523/210126425-ac4a3fce-c539-4f91-aacc-05be22bbd3b9.PNG)


Script is pulling over 1000 names in the file and creating a username and password in the directory for each. The script creates the usernames as 1st letter of first name and last name and also lowers any capitalized letter as well as give generic password. For example: Edwin Melero = username: emelero and password: Password1.

![User creation](https://user-images.githubusercontent.com/105263523/210126661-e133076d-4442-4d43-afa2-c3960f423e7d.PNG)


Here you see the list of all the usernames in the folder named _USERS.

![user list](https://user-images.githubusercontent.com/105263523/210127267-7714b6f6-c1e0-4d83-92b8-fd1e8e498e39.PNG)


This is the creation of the client VM named CLIENT1. Network attached to Internal Network.

![CLIENT1VMnetowrkadapter](https://user-images.githubusercontent.com/105263523/210127382-e13e25d9-906b-4481-844e-da939b727572.PNG)


After Windows 10 ISO installation, Logging in to CLIENT1 VM

![CLIENT1 login](https://user-images.githubusercontent.com/105263523/210127417-b2411ea9-d3b2-457b-ace8-cafdeab2a152.PNG)


PC Renaming and joining Domain

![CLIENT1 rename and joining](https://user-images.githubusercontent.com/105263523/210128250-5ab03712-c465-419e-a7dc-2b40c4c5309a.PNG)


On the cmd command line prompt IPconfig to see our IP connections and default gateway. Ping verifies there is connection. Whoami shows user logged in. 

![IPconfigping](https://user-images.githubusercontent.com/105263523/210127623-fdcb471d-4826-4489-a16f-40e51d59a428.PNG)



