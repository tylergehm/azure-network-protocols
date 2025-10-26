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

- <b>RDP (Remote Desktop Protocol):</b> RDP enables remote control of Windows systems, facilitating management and troubleshooting over a network.
</p>
 
Wireshark is a free tool that captures and analyzes network traffic, like observing the data packets traveling between computers on a network. It helps IT support staff troubleshoot issues, such as slow connections or errors, by showing detailed network activity. Think of it like a security camera recording and reviewing all the activity in a busy office to spot problems.
</p>
- + <i>Wireshark can be downloaded at https://www.wireshark.org/download.html</i> + -
</p>
<b><i>NOTE:</i></b> This demonstration uses Virtual Machines created in a previous project, ["Creating Windows and Linux Virtual Machines in Azure Portal"](https://github.com/tylergehm/vm)

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
- Step 8 - Clean up project in Azure Portal

<h2>Step 1 - Install Wireshark onto Windows 11 Virtual Machine </h2>

<img width="1486" height="545" alt="image" src="https://github.com/user-attachments/assets/0c97dde1-8e92-4132-bc86-4057ed27573b" />
The project will begin by obtaining the Public IP Address of the Windows 11 Virtual Machine in the Azure Portal.
</p>

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


<h2>Step 5 - Observe DHCP Traffic </h2>


<h2>Step 6 - Observe DNS Traffic </h2>


<h2>Step 7 - Observe RDP Traffic </h2>


<h2>Step 8 - Clean up project in Azure Portal </h2>
</p>
<br />
