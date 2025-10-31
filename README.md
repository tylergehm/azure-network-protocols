<p align="center">
<img width="897" height="566" alt="image" src="https://github.com/user-attachments/assets/2e0a472c-bf3f-4ce4-a460-cd545d84cb3f" />

</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this project, we use Wireshark to examine ICMP, SSH, DHCP, DNS, and RDP traffic to and from Azure Virtual Machines, while also configuring Network Security Groups to manage and secure network communication.</p>
</p>

- <b> ICMP (Internet Control Message Protocol):</b> ICMP is a network protocol used for diagnostics and error reporting, such as pinging to check if a device is reachable.

- <b> SSH (Secure Shell):</b> SSH provides secure, encrypted remote access to devices, allowing users to manage systems over a network.

- <b>DHCP (Dynamic Host Configuration Protocol):</b> DHCP automatically assigns IP addresses and network settings to devices, simplifying network connectivity.

- <b>DNS (Domain Name System):</b> DNS converts human-readable domain names into IP addresses, enabling devices to locate websites or services on the internet.

- <b>RDP (Remote Desktop Protocol):</b> RDP is a proprietary protocol developed by Microsoft that allows a user to connect to and control another computer remotely over a network connection, providing a graphical interface.
</p>
 
Wireshark is a free tool that captures and analyzes network traffic, like observing the data packets traveling between computers on a network. It helps IT support staff troubleshoot issues, such as slow connections or errors, by showing detailed network activity. Think of it like a security camera recording and reviewing all the activity in a busy office to spot problems.
</p>
- + <i>Wireshark can be downloaded at https://www.wireshark.org/download.html</i> + -
</p>

Note: This demonstration uses Virtual Machines created in a previous project:  [Creating Virtual Machines in Azure Portal](https://github.com/tylergehm/vm)

<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop Connection
- Command-Line Tools
- Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 11 Home (Host Machine)
- Windows 11 Pro (21H2)
- Ubuntu Pro 24.04

<h2>Project Steps</h2>

- Step 1 - Install Wireshark onto Windows 11 Virtual Machine
- Step 2 - Observe ICMP Traffic
- Step 3 - Configure a Firewall (Network Security Group)
- Step 4 - Observe SSH Traffic
- Step 5 - Observe DHCP Traffic
- Step 6 - Observe DNS Traffic
- Step 7 - Observe RDP Traffic
- Step 8 - Project Clean Up

<h2>Step 1 - Install Wireshark onto Windows 11 Virtual Machine </h2>

Note: This demonstration uses a Virtual Machine created in a previous project:  [Creating Virtual Machines in Azure Portal](https://github.com/tylergehm/vm)
</p>

<img width="1674" height="283" alt="image" src="https://github.com/user-attachments/assets/7bf845e4-158b-4672-a735-93c7c1cf5e15" />
This project will begin by selecting "Virtual Machines" on the Azure Portal home page.

<img width="1187" height="434" alt="image" src="https://github.com/user-attachments/assets/fc5cf89c-e5b3-4e03-b343-ba6e2c8cb735" />
Once inside the Virtual Machines page of Azure Portal, the Public IP Address to the Windows 11 Virtual Machine can be obtained. This is the VM that will be used for this demonstration. 
</p>

<img width="452" height="270" alt="image" src="https://github.com/user-attachments/assets/b7ddee2b-cbdf-405b-a399-cc509f1a2f68" /> </p>
Once the IP Address for the Windows 11 VM has been obtained, hold the Windows Key + press "R" to open up the run command. In the box next to "Open", type the letters "mstsc" and press Enter. Mstsc stands for Microsoft Terminal Services Client. The Microsoft Terminal Services Client (MSTSC) is the client application built into Windows that uses the Remote Desktop Protocol (RDP) to establish a secure, graphical connection to a remote computer or server.

<img width="532" height="302" alt="image" src="https://github.com/user-attachments/assets/17c5d870-4be1-4233-abac-53b2d301e0b6" />

The Windows 11 Virtual Machine will be accessed using the VM's Public IP Address in Remote Desktop Connection

<img width="557" height="527" alt="image" src="https://github.com/user-attachments/assets/560d59c6-3836-42d4-a145-c3bf5ee35176" />

Credentials will be required to log into the Windows 11 VM, which were established when creating the VM.

<img width="511" height="487" alt="image" src="https://github.com/user-attachments/assets/75dc4a55-7d6b-418a-81f4-81078766c72c" />

After logging in, Windows Security will prompt a warning message that the security certificate cannot be verified. Click "Yes" to continue to Windows 11 VM.

<img width="1917" height="980" alt="image" src="https://github.com/user-attachments/assets/06f4f884-8658-4994-8bbc-df888e53975c" />

Once inside the Windows 11 VM, Wireshark will be downloaded from the official website at https://www.wireshark.org/download.html. 

The Windows x64 Installer will be selected for download.

<img width="1735" height="1463" alt="image" src="https://github.com/user-attachments/assets/7a0a208c-2ea3-4979-b858-5a88bd8df825" />

Open up the Wireshark installation wizard and click "Next" through each step until Wireshark is installed.

<img width="939" height="729" alt="image" src="https://github.com/user-attachments/assets/46fbca66-8647-4060-af4c-7f581de73078" />

In Wireshark, the Ethernet options you select for packet capture are referred to as "Interfaces" or "Network Interfaces" on the homepage (also called the Capture Interfaces dialog). These are the network adapters or Ethernet devices (e.g., eth0, eth1, or specific network card names) available on your system that Wireshark can use to capture packets. You choose one or more interfaces to start capturing network traffic.

Hover your mouse over the Interfaces to see which one has the Private IP Address of the Windows 11 VM. In this case, it is 172.16.0.4. 

Double click the Interface to begin the packet capture.

<img width="1192" height="519" alt="image" src="https://github.com/user-attachments/assets/73e806ba-fcef-4a59-8f47-c4bad4ba90fd" />

The Private IP Address can be found in the directory page for the Windows 11 VM in the Azure Virtual Machine Portal.

<img width="932" height="722" alt="image" src="https://github.com/user-attachments/assets/f8a6792a-ab91-444e-9fd7-6bdb170d5f18" />

Once the packet capture has begun, an endless flow of packet traffic will begun to appear in Wireshark.

<h2>Step 2 - Observe ICMP Traffic </h2>

ICMP (Internet Control Message Protocol) traffic consists of control and error-reporting messages used by network devices to communicate status, errors, or diagnostic information, such as ping requests and replies or destination unreachable notifications. It operates at the network layer and is essential for troubleshooting and network management.

<img width="930" height="721" alt="image" src="https://github.com/user-attachments/assets/34c81e51-e4a4-471b-ad2f-a46ed8f483cc" />

This step of the project will begin by using the search bar inside Wireshark, which is utilized to filter traffic for specific ports or protols. In this case, the filter will be used for filtering out ICMP traffic.

<img width="1861" height="733" alt="image" src="https://github.com/user-attachments/assets/012103cf-3d96-428d-b130-5a15deddc229" />

The Linux VM's Private IP Address can be found in the Virtual Machines page of the Azure Portal. This IP Address will be utilized for testing ICMP traffic, as it will be pinged by the Windows 11 VM.

<img width="967" height="895" alt="image" src="https://github.com/user-attachments/assets/59307fd4-6085-4e3c-a401-af02218850a0" />

Inside the Windows 11 VM, Powershell will be opened up for the ping test.

<img width="1475" height="750" alt="image" src="https://github.com/user-attachments/assets/5abb462f-ad78-4f5f-8b7d-9d2325301d8e" />

Once Powershell is opened, "ping 172.16.1.4" into the command prompt.

<img width="1919" height="689" alt="image" src="https://github.com/user-attachments/assets/93bb7a71-c3ab-4970-80fa-e845d9b9cc2b" />

Ping was successful. The Wireshark packet capture shows the ICMP traffic for the ping requests and replies between the two VMs.

There are a total of 8 packets; 4 packets of request from the Windows 11 VM and 4 packets of reply from the Linux VM.

The ping command typically sends four packets by default to provide a small but sufficient sample to measure network connectivity, latency, and packet loss. This number balances quick testing with reliable results, as multiple packets help detect inconsistencies like dropped packets or variable response times.

<h2>Step 3 - Configure a Firewall (Network Security Group) </h2>

In this step of the project, the Linux VM will have a Firewall configured in it's Network Security Group (NSG). This Firewall will be set up to block any incoming ICMP traffic, which will block any ping attempts from the Windows 11 VM.

In Microsoft Azure, a Network Security Group (NSG) is called so to reflect its role as a cloud-native, flexible, and programmable set of rules that control inbound and outbound network traffic for Azure resources, functioning similarly to a traditional firewall. The term "group" emphasizes that it’s a collection of security rules applied to virtual networks or specific resources like virtual machines, distinguishing it from a physical firewall appliance by focusing on its logical, policy-based nature in a cloud environment. This naming aligns with Azure’s terminology for managing security at scale across virtual networks.

<img width="1872" height="784" alt="image" src="https://github.com/user-attachments/assets/7607e730-9bec-4986-9c79-e00ec491f41d" />

The Linux NSG can be access in the Azure Portal. Opening up the Linux VM directory page, click the drop down arrow next to "Networking", then click "Network settings". 

Once inside the Network settings, click on "Linux-VM-nsg" to access the Network Security Group for the Linux VM.

<img width="1898" height="855" alt="image" src="https://github.com/user-attachments/assets/91ea937e-3d49-4abd-b405-5c797e3a0c87" />

View of inside the Linux VM Network Security Group.

<img width="1898" height="886" alt="image" src="https://github.com/user-attachments/assets/96bcbb50-fbda-4bba-969d-05f11470c09a" />

To add the ICMP Firewall, click the "Settings" drop down box ---> click "Inbound Security Rules" ---> then click "Add"

In the "Add inbound security rule" section, the first form to fill out is the Destination port ranges. In this section, an asterisk "*" will be placed, which represents any port. The port number is irrelevant in this case because ICMP does not use a port number.

The protocol "ICMPv4" will be selected because we are testing the ping with an IPv4 Private IP Address.

The action to be selected is "deny", which will block any incoming ICMP packets.

The rule requires a name, so "DenyPing" is the name of the rule being put into place for this project.

Once this is filled out, click "Add" to create the new security rule.

<img width="1559" height="416" alt="image" src="https://github.com/user-attachments/assets/c6386274-d7d4-437c-bb73-86adc73c000a" />

The ICMP Firewall has been successfully added into the Network Security Group for the Linux VM.

<img width="1916" height="471" alt="image" src="https://github.com/user-attachments/assets/a7424481-e415-46ed-8a3e-c31fa486f5df" />

Returning to the Windows 11 VM, the Linux VM will be pinged using Powershell. 

The ping request timed out because the Linux VM security rule is now in place. 

It can be observed in Wireshark that ping requets were sent but there is no reply because the incoming traffic is blocked on the Linux VM.

<h2>Step 4 - Observe SSH Traffic </h2>
SSH (Secure Shell) traffic refers to network data transmitted over the SSH protocol, which provides a secure, encrypted channel for remote access, file transfers, and command execution between devices. It typically uses TCP port 22 and is commonly used for managing servers or secure file transfers via tools like SCP or SFTP. The encryption ensures that data, such as login credentials and commands, remains confidential and protected from interception.

<img width="872" height="193" alt="image" src="https://github.com/user-attachments/assets/b638f3d8-b65d-4081-9e67-87951d30b6bc" />

This step in the project will begin by changing the Wireshark filter from "icmp" to "ssh" to filter for SSH traffic.

<img width="1475" height="225" alt="image" src="https://github.com/user-attachments/assets/aa52ac6b-cbdf-4167-a4a7-e7f0f01bf547" />

Using Powershell in the Windows 11 VM, the Linux VM will be connected into using SSH. 

The command typed will be "ssh Linux-VM@172.16.1.4" --- Linux-VM is the username for the Linux VM and 172.16.1.4 is the Private IP Address for the Linux VM.

<img width="1470" height="329" alt="image" src="https://github.com/user-attachments/assets/10baf665-23fb-48d3-b62a-02f6d6549828" />

Once the command was entered, Powershell verifies that the connection to the Linux VM is to be made. Type "Yes"

Next, the password for the Linux VM user will be requested before the connection can be made.

<img width="1903" height="784" alt="image" src="https://github.com/user-attachments/assets/03322ba0-77cf-4b0f-92f8-aab411858f0b" />

The connection was successfully made and Wireshark captured all the SSH network traffic that occured during the process.

The connection successfully logged into the Linux VM via SSH, as indicated by the prompt Linux-VM@Linux-VM:~$. This shows a shell session (likely Bash) on the Linux VM.

<h2>Step 5 - Observe DHCP Traffic </h2>

<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/abc6b151-bc04-4eca-ae1a-14c143d011b3" /></p>


DHCP (Dynamic Host Configuration Protocol) traffic consists of network messages exchanged between a DHCP client and server to automatically assign and manage IP addresses and network configuration details, such as subnet masks and gateways. It typically involves a four-step process (Discover, Offer, Request, Acknowledge) to lease an IP address to a device. This traffic is essential for devices to join a network without manual configuration. DHCP uses UDP ports 67 and 68.

<img width="954" height="169" alt="image" src="https://github.com/user-attachments/assets/666db282-512d-4e45-bafd-e56729bd5b89" />

This step will begin by changing the Wireshark filter from SSH to UDP ports 67 and 68.

The filter used will be "udp.port == 67 || udp.port == 68" 

The Wireshark filter udp.port == 67 || udp.port == 68 is written this way to specify that it should capture UDP packets where either the source or destination port is 67 (DHCP server) or 68 (DHCP client). The || operator means "logical OR" in Wireshark's filter syntax, allowing the filter to match packets that satisfy either condition. This syntax ensures both client-to-server and server-to-client DHCP traffic is captured.

<img width="1423" height="471" alt="image" src="https://github.com/user-attachments/assets/2623d27a-2535-4ccb-8bbf-c86dbef6ab18" />

To observe DHCP traffic, the IP address on the Windows 11 VM must be released and renewed to trigger the DHCP process, which involves the client (VM) sending a request to the DHCP server and receiving a new IP address. Releasing the current IP address (e.g., using ipconfig /release) forces the VM to initiate a new DHCP handshake (Discover, Offer, Request, Acknowledge), generating observable network traffic on UDP ports 67 and 68. Without this, the VM may retain its existing IP lease, producing no DHCP traffic to capture.

In order to do this, a script must be created and then deployed within Powershell. 

The script will be created in Notepad with the commands "ipconfig /release" to release the current Private IP address and "ipconfig /renew" to give the Windows 11 VM a new Private IP address.

<img width="938" height="591" alt="image" src="https://github.com/user-attachments/assets/4718c839-25b7-42e4-be95-f6cbf2cca546" />

The script will be saved the "C:\" drive as "DHCP.bat". 

A .bat file is a batch file used in Windows to execute a series of commands automatically in the Command Prompt or PowerShell. It contains plain-text commands, such as those to run programs or configure network settings, and is executed by double-clicking or calling it from a terminal. In this project, the DHCP.bat file will automate the release and renewal of an IP address to trigger DHCP traffic.

<img width="1465" height="597" alt="image" src="https://github.com/user-attachments/assets/4b07b08c-6de8-49d2-b82c-873bcf69e02f" />

The DHCP.bat was verified by using the "cd C:\" command to change the directory to the C:\ folder.

Then the command "dir" was entered to show the directory for the C:\. The DHCP.bat file is present in the folder's directory.

<img width="260" height="67" alt="image" src="https://github.com/user-attachments/assets/981b8112-3ffb-499e-a887-2b3647562936" />

The command ".\dhcp.bat" was entered into Powershell to run the DHCP script; causing the IP address to be released and then renewed.

<img width="1913" height="1016" alt="image" src="https://github.com/user-attachments/assets/454bb8c1-2c62-42d7-9b93-167c786a0ce8" />

The DHCP script was successfully deployed and the DHCP traffic is observable in Wireshark. 

We can see that the DHCP four way handshake has successfuly occurred.

The DHCP four-way handshake is the process by which a client obtains an IP address from a DHCP server, involving four messages: Discover, Offer, Request, and Acknowledge (DORA). The client broadcasts a Discover message to locate a DHCP server, which responds with an Offer containing an available IP address and configuration details. The client then sends a Request to formally ask for the offered IP, and the server finalizes the process with an Acknowledge message, confirming the lease of the IP address.

<h2>Step 6 - Observe DNS Traffic </h2>
This step of the project revolves around observing DNS traffic. 

DNS traffic refers to the network data exchanged between a client device and a Domain Name System (DNS) server to resolve domain names (e.g., www.example.com) into IP addresses. When a user attempts to access a website, the client sends a DNS query, and the server responds with the corresponding IP address, enabling the connection. This traffic is essential for navigating the internet and typically occurs over UDP port 53.

<img width="1025" height="131" alt="image" src="https://github.com/user-attachments/assets/0355c2b6-9c8f-4381-b6f1-cfbf90d17aa9" />

The first step of this process is to change the Wireshark filter to "dns"

<img width="558" height="43" alt="image" src="https://github.com/user-attachments/assets/6b505cf6-1bc9-4302-a02e-fb7feee5ce18" />

In Powershell, the command "nslookup linkedin.com" is typed in. Once this command is executed, PowerShell initiates a DNS query to resolve the domain name linkedin.com into an IP address.

<img width="1906" height="706" alt="image" src="https://github.com/user-attachments/assets/5cdeda68-9d72-48df-9af4-490109f067ed" />

The command was successfully executed and Wireshark captured the DNS traffic for this process.

<h2>Step 7 - Observe RDP Traffic </h2>

RDP traffic refers to the network data exchanged between a client device and a server to establish and maintain a Remote Desktop Protocol (RDP) session. When a user connects to a remote computer , the client sends a request to the server, and the server responds by displaying its desktop interface, enabling the user to interact with the remote machine as if they were sitting in front of it. This traffic is essential for remote administration, technical support, and virtual desktop infrastructure, and typically occurs over TCP port 3389. </p>

<img width="690" height="119" alt="image" src="https://github.com/user-attachments/assets/8c0ace2e-cae9-464a-ad00-09e3b0d3ae03" />
</p>
We will begin to observe RDP traffic by changing the Wireshark packet filter to "tcp.port == 3389" then press Enter.
</p>
<img width="1919" height="1022" alt="image" src="https://github.com/user-attachments/assets/1b77e129-d326-4119-a172-d883c18ade8e" /> </p>
The RDP traffic constantly appears to be "spamming" data in Wireshark because its primary job is to keep the remote screen perfectly updated . Even when you're not actively moving the mouse or typing, the server is continuously sending small, frequent packets representing minor changes like a blinking cursor, a clock tick, or background animations. Additionally, RDP uses control and keep-alive messages to constantly monitor and adapt to the network's quality, and the underlying TCP protocol generates a continuous stream of Acknowledgement (ACK) packets for every piece of data received, all of which contribute to the high packet count you see in the capture.
</p>
<h2>Step 8 - Project Clean Up</h2>

Virtual Machines cost money to run, so it is important to delete them and all their data after use. </p>

<img width="1300" height="389" alt="image" src="https://github.com/user-attachments/assets/308937e9-41d8-4930-9360-ffe3adf27495" />
</p>
The first thing that will be done is to type "Resource Groups" in the Azure Portal search bar. </p>
An Azure resource group is a logical container that holds related resources for an Azure solution, such as virtual machines, databases, and storage accounts. It allows you to manage the lifecycle (like deployment, updates, and deletion) of these resources together as a single unit.</p>

<img width="1887" height="579" alt="image" src="https://github.com/user-attachments/assets/33bb0ff6-5f5f-48ac-b619-ea1e108a6c5b" /> </p>
Once inside the resource groups portal, locate the resource group that virtual machines were created in. </p>


<img width="1191" height="720" alt="image" src="https://github.com/user-attachments/assets/8e73408f-7ae7-4980-bf7c-0845eb9a1b0f" /> </p>

Once the resource group has been opened up, locate the button that says "Delete resource group" and click on it. </p>

<img width="722" height="812" alt="image" src="https://github.com/user-attachments/assets/74da59c1-9738-4495-8ba7-6ab740482e19" /> </p>

Inside the "Delete resource group" page, click on the "Copy" icon next to the resource group name. Then paste the the resource group name into the section that says "Enter resource group name to confirm deletion". Once this is done, then click on "Delete", and the resource groups with the virtual machines and all of their data will be deleted.

<h2>Conclusion</h2>
This project effectively demonstrated the use of Wireshark to capture and analyze critical network protocols—ICMP, SSH, DHCP, DNS, and RDP—within Microsoft Azure Virtual Machines, while showcasing the power of Network Security Groups to control and secure traffic flow. By observing live packet exchanges, configuring firewall rules to block ICMP pings, and triggering protocol-specific traffic through commands like ping, SSH login, IP renewal, and DNS lookups, we gained practical insight into how these protocols operate in a cloud environment and how NSGs function as virtual firewalls to enforce security policies. The continuous RDP traffic highlighted the protocol’s role in maintaining real-time remote desktop sessions, reinforcing the importance of monitoring and managing network activity for troubleshooting, security, and performance optimization in Azure deployments.




