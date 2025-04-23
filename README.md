
# Secure Network Devices
</br>

### <ins>Objective</ins>

This project aimed to provide hands-on experience securing network devices using Cisco Packet Tracer as a simulation tool. It focused on configuring authentication for routers and switches, implementing DHCP for efficient IP management, and enforcing security measures to protect switch ports from unauthorized access and potential threats. This hands-on project was designed to enhance practical knowledge and strengthen understanding of network security.
</br></br>
### <ins>Skills Learned</ins>

- Configuring authentication on network devices (routers and switches)
- Implementing DHCP for efficient IP management.
- Securing switch ports to mitigate security threats.
- Utilizing Cisco Packet Tracer for network simulation and troubleshooting.
- Advanced understanding of network security concepts, best practices, and practical applications.
</br></br>
### <ins>Tools Used</ins>

- Cisco Packet Tracer (Network simulation software).
- Router and Switch configurations (CLI-based security settings)
- Networking protocols (Authentication, DHCP, and security best practices). 
</br></br>

### <ins>Walkthrough</ins>

This project will consist of 5 tasks, which are as follows:
1. Create a network topology using Cisco Packet Tracer
2. Apply authentication on the switches
3. Apply authentication on the router
4. Enable PCs from different VLANs to communicate with each other
5. Configure DHCP on the router and secure the ports of the switch from unauthorized access
</div>
</br>



#### <ins>Task 1: Create a network topology using Cisco Packet Tracer</ins>
We will use Cisco Packet Tracer to design and create a network topology that consists of 2 switches connected with 2 PCs each, as in Figure 1. 

Figure 1
![Figure 1](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/figure%201.png)
</br></br></br>

#### <ins>Task 2: Apply authentication on the switches</ins>
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

![Figure 3](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%203%20Verification%20of%20password%20at%20Switch0.png)

This time round, when invoking the command 'en' to enter privileged EXEC mode, we are being prompted for a password before we can proceed. The required password is configured as "apple" in our earlier steps. This prompt signifies that basic authentication access for switch0 has been successfully implemented.

After entering the correct password "apple", we will invoke the <show run> command to review the current configuration on Switch0.

|Command	|Purpose|
|---------|--------|
|show run	|displays the switch's current active settings and is used to review the applied configuration.|
|control+Q	|returns immediately to the command prompt.|

The statement "enable password apple" was listed amongst the configuration details, confirming that the word "apple" was being stored as a plaintext password for accessing privileged EXEC mode.

Key observations:
The implemented password protection served as a simple way of providing terminal access control in a network. However, the password was being stored as plaintext and would be vulnerable to unauthorized access. For stronger security, an <enable secret> command  should be used instead—it encrypts the password and overrides the plaintext enable password.

We will now seek to rectify this to an encrypted password through the following steps:

Figure 4: Encrypting password of Switch0

![Figure 4](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/figure%204%20Encrypting%20password%20of%20Switch0.png)

|Command	|Purpose|
|---------|--------|
|no enable password |removes the existing plaintext password stored in a configuration file.|
|enable secret |defines a secret password and encrypts it.|

The <no enable password> command will disable the existing, less secure plaintext password for accessing the privileged EXEC mode. The <enable secret> command is a more secure, encrypted password for privileged EXEC mode. It will supersede the <enable password> if both are configured. Using encryption provides much better protection against unauthorized access.

Figure 5: Encrypted password of Switch0

![Figure 5](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%205%20Encrypted%20password%20of%20Switch0.png)

The above figure shows the resulting configuration:
- The plaintext enable password was removed, thereby improving security.
- The password apple was being encrypted into "$1$mERr$KA3NlZC09aPz89f9oGpKe1"
- The switch uses the encrypted enable secret password for privileged EXEC mode access.

Security Perspective:
By replacing the <enable password> with the encrypted <enable secret>, switch0 is more secure against attacks that rely on password cracking or interception. This is a key best practice for securing access to a network or network devices.

Next, we will implement the same on Switch1 using the same encrypted "apple" password.

Configuring Switch1:

Figure 6: Setting up encrypted password for Switch1

![Figure 6](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/figure%206%20Setting%20up%20encrypted%20password%20for%20Switch1.png)


Figure 7: Encrypted password of Switch1

![Figure 7](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/figure%207%20Encrypted%20password%20of%20Switch1.png)


#### <ins>Task 3: Apply authentication on the router</ins>

In this task, we will install a router model 2911 between Switch0 and Switch1. A router is a key network device on any network topology, and we will implement password authentication as an access control measure.

Figure 8: Network topology with Router0
![F8](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%208%20Network%20topology%20with%20Router0.png)

Figure 9: Setting up a password for Router0

![f9](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%209%20Setting%20up%20a%20password%20for%20Router0.png)


|Command	|Purpose|
|---------|-------|
|en |moves the session from user EXEC mode (Router>) to privileged EXEC mode (Router#) in order to execute higher-level commands, including configuration commands.|
|conf t |enters global configuration mode.|
|line console 0 |configures the console line, which is used for local management access to the router via the console port.|
|login |enables login authentication for the console line.|
|password cisco  |sets the password for the console line to "cisco".|
|exit |exits the console line configuration mode.
|exit |exits global configuration mode.|


The command <line console 0> refers to the console port, allowing configuration of its login settings.

The error message "% Login disabled on line 0, until 'password' is set" indicates that a password must be configured before login can be enabled. 

We had set "cisco" as the password required for accessing the console line during future login attempts.

The above console line configuration successfully enabled login authentication for the router console line. The plaintext password "cisco" was configured, allowing access to Router0's CLI via the console.


Figure 10: Encrypting password of Router0 </br>
![f10](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%2010%20Encrypting%20password%20of%20Router0.png)


|Command	|Purpose|
|---------|-------|
|en | moves the session from user EXEC mode (Router>) to privileged EXEC mode (Router#) to execute higher-level commands, including configuration commands.|
|conf t |enters global configuration mode.|
|enable secret cisxo |sets the enable secret password to "cisxo".|
|exit |exits global configuration mode, returning to privileged EXEC mode (Router#).|
|exit |logs out the user from the router CLI and makes the console available for the next session.|

The command <enable secret cisxo> stores the password "cisxo" in an encrypted format, making it far more secure against unauthorized access to privileged EXEC mode.


Next, we will change the passwords to "orange" for both console access and privileged EXEC mode as a practice. The configuration changes are detailed in Figure 11.

Figure 11: Changing password and encrypting it on Router0 </br>
![f11](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%2011%20Changing%20password%20and%20encrypting%20it%20on%20Router0.png)
 </br> </br> </br>



#### <ins>Task 4: Enable PCs from different VLANs to communicate with each other</ins>

Static IP Configuration - assigning of a unique IP address to a network device.

We will be assigning static IP addresses to the respective PCs on the network as per the table below:

|PC  |IPv4 Address	|Subnet Mask	|VLAN	|Default Gateway|
|----|--------------|-------------|-----|---------------|
|PC0|	10.10.10.1|	255.255.255.0|	10|	10.10.10.254|
|PC1|	10.10.10.2|	255.255.255.0|	10|	10.10.10.254|
|PC2|	10.10.20.1|	255.255.255.0|	20|	10.10.20.254|
|PC3|	10.10.20.2|	255.255.255.0|	20|	10.10.20.254|


Figure 12: Accessing IP configuration via the Desktop interface on PC0
![f12](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%2012%20Accessing%20IP%20configuration%20via%20the%20Desktop%20interface%20on%20PC0.png)


Figure 13:  Initial IP configuration of PC0
![f13](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%2013%20Initial%20IP%20configuration%20of%20PC0.png)


Figure 14: Static assigned IP configuration of PC0 on VLAN 10
![f14](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%2014%20Static%20assigned%20IP%20configuration%20of%20PC0%20on%20VLAN%2010.png)


Figure 15: Static assigned IP configuration of PC2 on VLAN 20
![f15](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%2015%20Static%20assigned%20IP%20configuration%20of%20PC2%20on%20VLAN%2020.png)


We will repeat the same steps to configure both the IPv4 addresses and Default Gateway for PC1, PC2, and PC3.

With the current IP address configuration, only PCs in the same VLAN are able to communicate with each other. 
For PCs to be able to communicate with PCs on another VLAN, a router would be needed.

We shall now test the connectivity between PCs on the same VLAN.

Figure 16: Test connectivity result of PC0 on VLAN 10 and VLAN 20 </br>
![f16](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%2016%20Test%20connectivity%20result%20of%20PC0%20on%20VLAN%2010%20and%20VLAN%2020.png)


As evidenced by the successful ping, PC0 (10.10.10.1) is able to establish a connection with PC1 (10.10.10.2) on VLAN 10. 
However,  PC0 (10.10.10.1) is unable to do so with PC2 (10.10.20.1) on VLAN 20 due to network segmentation.

We shall now attempt to fix this by establishing connectivity between the 2 VLANs.

First, we will need to configure Switch0.

Figure 17: Configuring Switch0 </br>
![f17](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%2017%20Configuring%20Switch0.png)



|Command	|Purpose|
|---------|-------|
|en |moves the session from user EXEC mode (Switch>) to privileged EXEC mode (Switch#) to execute higher-level commands, including configuration commands.|
|conf t |enters global configuration mode, allowing system-wide changes to the switch’s settings.|
|int fa0/1 |enters the interface configuration mode for FastEthernet0/1 (fa0/1) which connects to PC0.|
|switchport mode access |sets FastEthernet0/1 (fa0/1) to access mode. Access mode is used for connecting end devices and it ensures that port fa0/1 can only carry traffic for a single VLAN.|
|switchport access vlan 10 |assigns FastEthernet0/1 (fa0/1)  to VLAN 10.|
|int fa0/2 |enters the interface configuration mode for FastEthernet0/2 (fa0/2) which connects to PC1.|
|switchport mode access |sets FastEthernet0/2 (fa0/2) to access mode.| 
|switchport access vlan 10 |assigns FastEthernet0/2 (fa0/2)  to VLAN 10.|
|int fa0/3 |enters the interface configuration mode for FastEthernet0/3 (fa0/3).|
|Switchport mode trunk |configures FastEthernet0/3 as a trunk port. Unlike access mode, trunk mode allows multiple VLANs to pass through. A trunk port is typically used for inter-switch communication or connecting to a router for VLAN routing. Hence, FastEthernet0/3 (fa0/3) can transport traffic for VLAN 10 and other VLANs.|


Key Takeaways
VLAN Segmentation:
- Ports FastEthernet0/1 and FastEthernet0/2 only carry VLAN 10 traffic
- The trunk port (FastEthernet0/3) allows multiple VLANs to communicate across switches.

Access vs. Trunk Mode:
- Access ports are meant for end devices like PCs, servers, and printers.
- Trunk ports are used for network devices such as switch-to-switch connections.

Network Security & Efficiency
- VLANs reduce broadcast domains, improving network efficiency.
- Trunking ensures VLAN communication while maintaining segmentation.

Next, we shall configure Router0 to establish connectivity between Switch0 and Router0.

Figure 18: Configuring Router0 </br>
![f18](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%2018%20Configuring%20Router0.png)


|Command|Purpose|
|-------|-------|
|en |moves the session from user EXEC mode (Router>) to privileged EXEC mode (Router#) to execute higher-level commands, including configuration commands.|
|conf t |enters global configuration mode, allowing system-wide changes to the switch’s settings.|
|int gig0/0 |enters the interface configuration mode for GigabitEthernet0/0 (gig0/0) which connects to Switch0.|
|no shut |activates the GigabitEthernet0/0 (gig0/0) interface out of an administratively shut-down (disabled) state when the router is first configured.|
|int gig0/0.10 |creates and moves to sub interface GigabitEthernet0/0.10 (the ".10" represents VLAN 10 traffic). Sub-interfaces are logical divisions of a physical interface. They allow a single physical interface to handle traffic from multiple VLANs|
|encapsulation dot1q 10|configures 802.1Q encapsulation for VLAN 10 on the sub interface GigabitEthernet0/0.10. 802.1Q is the protocol used to tag Ethernet frames with VLAN information. This command specifies that this sub-interface handles traffic for VLAN 10. When the router receives frames tagged with VLAN 10, they are routed using this sub-interface.|
|ip address 10.10.10.254 255.255.255.0 |assigns an IP address and subnet mask to the sub-interface. 10.10.10.254 is the default gateway for VLAN 10. Devices in VLAN 10 will use this address to route traffic beyond their local network. 255.255.255.0 (subnet mask) indicates that VLAN 10 uses the /24 network, which supports up to 254 hosts.|
|switchport access vlan 10 |assigns FastEthernet0/2 (fa0/2)  to VLAN 10.|
|int fa0/3 |enters the interface configuration mode for FastEthernet0/3 (fa0/3).|
|Switchport mode trunk |configures FastEthernet0/3 as a trunk port. Unlike access mode, trunk mode allows multiple VLANs to pass through. A trunk port is typically used for inter-switch communication or connecting to a router for VLAN routing. Hence, FastEthernet0/3 (fa0/3) can transport traffic for VLAN 10 and other VLANs.|

The commands for establishing connectivity between Switch1 and Router0 are as follows:

Figure 19: Configuration Switch1 </br>
![f19](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%2019%20Configuration%20Switch1.png)</br>

Figure 20: Configuration of Router0 to establish connectivity with Switch1</br>
![f20](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%2020%20Configuration%20of%20Router0%20to%20establish%20connectivity%20with%20Switch1.png)</br>

Connectivity test performed on PCs within the same network segment VLAN 10:

Figure 21: Connectivity test from PC1 to PC0 within same VLAN 10</br>
![f21](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%2021%20Connectivity%20test%20from%20PC1%20to%20PC0%20within%20same%20VLAN%2010.png)</br>

Connectivity test performed on PCs within the same network segment VLAN 20:

Figure 22: Connectivity test from PC3 to PC2 within same VLAN 20</br>
![f22](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%2022%20Connectivity%20test%20from%20PC3%20to%20PC2%20within%20same%20VLAN%2020.png)</br>

Connectivity test from PC0 on VLAN 10 to PC2 (10.10.20.1) and PC3 (10.10.20.2)  on VLAN 20:

Figure 23: Connectivity test from PC0 to PC2 and PC3</br>
![f23](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%2023%20Connectivity%20test%20from%20PC0%20to%20PC2%20and%20PC3.png)</br>

Connectivity test from PC2 on VLAN 20 to PC0 (10.10.10.1) and PC1 (10.10.10.2)  on VLAN 10:

Figure 24: Connectivity test from PC2 to PC0 and PC1</br>
![f24](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%2024%20Connectivity%20test%20from%20PC2%20to%20PC0%20and%20PC1.png)</br>

These connectivity tests concluded that:
1. PCs on the same VLAN can communicate with each other.
2. PCs on VLAN 10 can communicate with PCs on VLAN 20.
 </br> </br> </br>


#### <ins>Task 5: Configure DHCP on the router and secure the ports of the switch from unauthorized access</ins>

The following commands configure Dynamic Host Configuration Protocol (DHCP) on router0, allowing it to assign IP addresses dynamically to network devices. Let’s break down each step.

Figure 25: Configuring DHCP protocol on Router0</br>
![f25](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%2025%20Configuring%20DHCP%20protocol%20on%20Router0.png)</br>

|Command|Purpose|
|-------|-------|
|en |moves the session from user EXEC mode (Router>) to privileged EXEC mode (Router#) to execute higher-level commands, including configuration commands.|
|conf t|enters global configuration mode, allowing system-wide changes to the switch’s settings.|
|ip dhcp pool 1|creates a DHCP pool named "1" for dynamic IP allocation. This pool name is arbitrary and could be any name or number. DHCP pools define how IP addresses are distributed across network devices.|
|network 10.10.10.0 255.255.255.0|defines the range that the DHCP pool will assign. 10.10.10.0 is the network ID of the subnet. 255.255.255.0 is the subnet mask, indicating that the IP range is 10.10.10.1 to 10.10.10.254 (excluding 10.10.10.0, the network address). Devices requesting DHCP will receive IP addresses dynamically within this range.|
|exit|exits the DHCP configuration mode, returning to global configuration mode|

Once DHCP was configured, Router0 would dynamically assigns an IP addresses from the 10.10.10.0/24 subnet when a device requests an IP address.

Changing IP configuration from static allocation to DHCP allocation on PC0:


Figure 26: Current IP configuration for PC0</br>
![f26](https://github.com/chiahsing-loh/Secure-Network-Devices/blob/main/images/Figure%2026%20Current%20IP%20configuration%20for%20PC0.png)</br>

Figure 27: IP configuration for PC0 using DHCP</br>

Similarly, DHCP configuration was made to PC1 as depicted in Figure 28.

Figure 28: IP configuration for PC1 using DHCP</br>


Suppose an attacker attempts to get information from this network and aims to destroy it subsequently. For this attempt, the attacker uses laptop0 to connect to port fa0/2 on Switch0 as depicted in Figure 29.


Figure 29: Network topology showing unauthorized access by an attacker via Laptop0</br>


Using Laptop0, the attacker managed to get a dynamically assigned IP address using DHCP configuration.

Figure 30: Attacker's Laptop0 IP configuration using DHCP</br>

The attacker uses the "ping" command to test his unauthorized access and establishes a successful connection with PC0, as shown in Figure 31.

Figure 31: Connectivity achieved by attacker's Laptop0</br>


To prevent unauthorized access, we must secure the switches' ports through the following steps.

In our network topology, we only want 1 PC to have access to Switch0 via port fa0/2.

Here are the commands to configure port security on port fa0/2 to prevent unauthorized access and enhance network security.

Figure 32: Configuring port fa0/2 on Switch0</br>

|Command|Purpose|
|-------|-------|
|en |moves the session from user EXEC mode (Switch>) to privileged EXEC mode (Switch#) to execute higher-level commands, including configuration commands.|
|conf t|enters global configuration mode, allowing system-wide changes to the switch’s settings.|
|int fa0/2|enters the interface configuration mode for FastEthernet0/2 (fa0/2) which connects to PC1.|
|switchport port-security|port security on FastEthernet0/2. Port security allows control over which devices can connect to the port, preventing unauthorized access.|
|switchport port-security maximum 1|limits the number of devices that can connect to this port to 1. If a second device is plugged into FastEthernet0/2, the switch considers it unauthorized.|
|switchport port-security violation shutdown|defines the action to take when a violation occurs. If an unauthorized device is detected, the switch will automatically shut down the port, preventing unauthorized access.|
|switchport port-security mac-address sticky|defines the switch to dynamically learns the MAC address of the first device connected to FastEthernet0/2. This MAC address is then automatically stored in the switch’s configuration. If another device attempts to connect, a security violation occurs.|
|switchport access vlan 10|assigns FastEthernet0/2 (fa0/2)  to VLAN 10.|
|int fa0/3|enters the interface configuration mode for FastEthernet0/3 (fa0/3).|
|Switchport mode trunk|configures FastEthernet0/3 as a trunk port. Unlike access mode, trunk mode allows multiple VLANs to pass through. A trunk port is typically used for inter-switch communication or connecting to a router for VLAN routing. Hence, FastEthernet0/3 (fa0/3) can transport traffic for VLAN 10 and other VLANs.|

Similar security hardening was also made on port fa0/1 on Switch0:

Figure 33: Configuring port fa0/1 on Switch0</br>

The above steps enhanced Switch0's port security by limiting access to specific devices, preventing MAC address spoofing attacks, and automatically shutting down unauthorized access.


A subsequent attempt to reconnect Laptop1 to port fa0/2 on Switch0 is denied. Hence, the access control made on Switch0 port fa0/2 has been strengthened against unauthorized access.

Figure 34: Failed connectivity of attacker's Laptop1</br>
