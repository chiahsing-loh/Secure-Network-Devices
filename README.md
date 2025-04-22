
# Secure Network Devices
</br>

### Objective

This project aimed to provide hands-on experience securing network devices using Cisco Packet Tracer as a simulation tool. It focused on configuring authentication for routers and switches, implementing DHCP for efficient IP management, and enforcing security measures to protect switch ports from unauthorized access and potential threats. This hands-on project was designed to enhance practical knowledge and strengthen understanding of network security.
</br></br>
### Skills Learned

- Configuring authentication on network devices (routers and switches)
- Implementing DHCP for efficient IP management.
- Securing switch ports to mitigate security threats.
- Utilizing Cisco Packet Tracer for network simulation and troubleshooting.
- Advanced understanding of network security concepts, best practices, and practical applications.
</br></br>
### Tools Used

- Cisco Packet Tracer (Network simulation software).
- Router and Switch configurations (CLI-based security settings)
- Networking protocols (Authentication, DHCP, and security best practices). 
</br></br>

### Walkthrough

This project will consist of 5 tasks, which are as follows:
1. Create a network topology using Cisco Packet Tracer
2. Apply authentication on the switches
3. Apply authentication on the router
4. Enable PCs from different VLANs to communicate with each other
5. Configure DHCP on the router and secure the ports of the switch from attackers
</div>
</br>



#### Task 1: Create a network topology using Cisco Packet Tracer
We will use Cisco Packet Tracer to design and create a network topology that consists of 2 switches connected with 2 PCs each, as in Figure 1. 

Figure 1
![Figure 1](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/figure%201.png)
</br></br></br>

#### Task 2: Apply authentication on the switches
Authentication is the process of providing access control for systems by checking to see if a user's credentials match the credentials in the database of authorized users.

To implement network security on this topology, we should enable passwords for the network devices to prevent unauthorized users from accessing this network.

We will use the following commands to assign the password 'apple' to switch0 in privileged EXEC mode:

Figure 2: Setting a password for Switch0

![Figure 2](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%202%20Setting%20a%20password%20for%20Switch0.png)

|Command	|Purpose|
|---------|--------|
|en 	|enables privileged EXEC mode to execute higher-level commands and access device configurations.|
|conf t	|enters global configuration mode to configure the switch's settings and make administrative changes.|
|enable password	|defines a new password or changes an existing password for access to privileged EXEC mode.|
|exit	|exits current mode (global configuration or privileged EXEC)|
</br>

The following commands are used to verify and view the password set for switch0:

Figure 3: Verification of password at Switch0

\
\
\
\
![Figure 2](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/LFS101-Course-Badge-1-300x300.jpg?raw=true)\
Figure 2: Linux Badge sample




