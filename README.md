# RIP-Protocol
RIP protocol for MCN SEM 6 RC19-20 </br>

# Table of Contents

# Network Topology Diagram 
![topology DIAGRAM](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/Network%20topology%20diagram.jpg)
# BEST PRACTICES:
## Set the Preferences to show port labels. </br>
This does help while assigning ip addresses to each port.</br>
To navigate to preferences, either,</br>
1. click on Options and then Preferences</br>
2. Ctrl+R</br>
Choose "Always Show Port Labels"</br>
![preferences](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/2%20preferences.JPG)</br>
## Label each port by its IP ADDRESS

# STEP1: Build the topology as seen in the above diagram.
Note the Network Devices being used are</br>
- Generic (Router-PT)</br>
- Generic (PC-PT)</br>
![topology](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/1st%20network%20topo.JPG)</br>
# STEP2: Statically Assign the IP address and Subnet Mask for the PCs
Accoridng to the diagram,</br>
PC0 takes IP address: 10.0.0.2, Subnet Mask: 255.0.0.0 (represented by /8)</br>
PC1 takes IP address: 20.0.0.2, Subnet Mask: 255.0.0.0 (represented by /8)</br>
To assign this, click on the PC icon > Desktop tab > IP Configuration.</br>
Assign as below:</br>
![PC0](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/3%20IP%20Configuration%20PC0.JPG)</br>
![PC1](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/3%20IP%20Configuration%20PC1.JPG)</br>
After assigning any IP address to any port or device, its best to label the port using the label icon present top
see [best practices](#best-practices). 

# STEP3: Statically Assign the IP address of Fast Ethernet 0/0 port for both PC0 and PC1
Fast Ethernet 0/0 or Fa0/0 is the port in your router that connects to a PC.</br> 
Hence we can set it up for both Router0 and Router1 connected to PC0 and PC1 respectively.</br></br>
Click on Router0 and then on CLI. 
Type in below::</br>
![Router0 fa0/0](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/3%20Router%200%20ip%20set%20fa00.JPG)</br>
Explanation::</br>
1. First type in no / n to exit configuration dialog</br>
2. Then press Enter key (=Return)</br>
3. Type in "en" (short) or "enable" (full) </br>
4. Enter global configuration mode by typing in  "conf t" (short) or "configure terminal" (full) </br>
5. To set IP address of fa0/0 or FastEthernet0/0 we navigate to it by typing,</br>
 "int fa0/0" (short) or "int FastEthernet0/0 " (full) </br>
6. Enter the IP address, that is, 10.0.0.0.1 with subnet mask, 255.0.0.0 (which is represented by /8)</br>
By either typing,</br>
"ip add 10.0.0.1 255.0.0.0"(short)</br>
"ip address 10.0.0.1 255.0.0.0"(full)</br>
7. Boot the port, that is change the state from down to up using command,</br>
"no shut" (short)</br>
"no shutdown" (full)</br>
8. Type in "exit" to get out off fa0/0</br>
</br></br>
That's it!</br>
Do the same for router2 set for fa0/0, IP address as 20.0.0.0.1 with subnet mask, 255.0.0.0 </br>
![Router 2 fa0/0](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/3%20Router2%20ip%20set%20fa00.JPG)</br>

# SERIAL PORTS:
Note that each Router can connect to another Router, (int the case of Router-PT) via serial ports.</br>
These serial ports are </br>
1. Serial 2/0 </br>
2. Serial 3/0</br>
By labelling the ports, you will now see the ports highlighted as Se2/0 (for Serial 2/0) and Se3/0 (for Serial 3/0). See [best practices](#best-practices)</br></br>
These serial ports can either be DCE or DTE.</br>
1. For DCE, It requires clock rate and bandwidth to be set.</br>
2. DTE, It doesnt require clock rate and bandwidth to be set.</br></br>
To find out which of your ports are DCE and which is DTE, you can either:</br>
1. On setting you [preferences](#best-practices) to label each port. DCE ports are labelled by a clock.</br>
2. Use a command, "show controller serial 2/0" (replace 2/0 by 3/0 for serial 3/0)</br>
note: this command does not work in global configuration mode. So if you are in global configuration mode, get out of it by either using "exit" or Ctrl+C</br>

# STEP4: Assign IP addresses for each of the Router 0
</br>
For Router0, accrding to the [diagram](##network-topology-diagram) 
</br>
I. its serial port, on the line connecting router0 and router2, has IP address: 192.168.1.254/30</br>
To set IP address:</br>
1. First check what kind of port this is. For me its a DCE serial 2/0. For you, instead of this it can be DCE serial 3/0, DTE serial 2/0 or DTE serial 3/0 . So properly note that before proceeding.</br>
![SHOW](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/router%20show%20step%2044444.JPG)</br>
2. Since mine is a DCE serial 2/0, I do the following commands. Some commands are marked "Only for DCE". These commands need not be implemented for DTE.</br>
Type in::</br>
![4.1](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/step%204%20substep%20code.JPG)</br>
Explanation::</br>
[1] Enter global configuration mode by typing in  "conf t" (short) or "configure terminal" (full) </br>
[2] To set IP address of se2/0 (in my case) we navigate to it by typing,</br>
 "int serial 2/0" </br>
if its se3/0 in your case, command:  "int serial 3/0" </br>
[3] Enter the IP address, that is 192.168.1.254 with subnet mask, 255.255.255.252 (which is represented by /30)
By typing,</br>
"ip add 192.168.1.254 255.255.255.252"</br>
[4] [only for DCE] now you gotta set clock rate and bandwidth. We mostly use standard measurements bandwidth as 64 and clock rate as 64000 unless externally specified.</br>
The commands are:</br>
"clock rate 64000"</br>
"bandwidth 64"</br>
[5] Boot the port, that is change the state from down to up using command,</br>
"no shut" (short)</br>
"no shutdown" (full)</br>
[6] Type in "exit" to get out of serial2/0 (in my case)</br>

2. its serial port, on the line connecting router0 and router1, has IP address: 192.168.1.249/30</br>
In my case this port is DCE serial 3/0.</br>
Type in commands:</br>
![4.2](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/step%204%20substep%20code%202.JPG)</br>

# STEP5: Assign IP addresses for each of the Router 1
For Router1, accrding to the [diagram](##network-topology-diagram),</br>
1. its serial port, on the line connecting router0 and router1, has IP address: 192.168.1.250/30</br>
For me its a DTE serial 2/0 port, so I typed in commands</br>
![5.1](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/step%205%20substep%20code%201.JPG)</br>

2. its serial port, on the line connecting router1 and router2, has IP address: 192.168.1.246/30</br>
For me its a DTE serial 3/0 port, so I typed in commands</br>
![5.2](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/step%205%20substep%20code%202.JPG)</br>

# STEP6: Assign IP addresses for each of the Router 2</br>
For Router2, accrding to the [diagram](##network-topology-diagram),</br>
1. its serial port, on the line connecting router0 and router2, has IP address: 192.168.1.253/30</br>
   For me its a DTE serial 2/0 port, so I typed in commands</br>
   ![6.1](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/step%206%20substep%20code%201.JPG)</br>
2. its serial port, on the line connecting router1 and router2, has IP address: 192.168.1.245/30</br>
   For me its a DCE serial 3/0 port, so I typed in commands</br>
   ![6.2](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/step%206%20substep%20code%202.JPG)</br>

# STEP7:Configure RIP Protocol</br>
1. For this one should get into global configuration mode first, that's by "conf t"</br>
2. Then "router rip"</br>
3. Then add the respective networks for each router </br>
Router 0:</br>
![rip r0](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/step%208%20router0.JPG)</br>
Router1:</br>
![rip r1](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/step%208%20router1.JPG)</br>
Router2:</br>
![rip r2](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/step%208%20router2.JPG)</br>

