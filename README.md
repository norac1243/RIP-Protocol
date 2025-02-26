# Routing Information Protocol (RIP)

#### **What is RIP?**  
Routing Information Protocol (RIP) is one of the oldest **distance-vector** routing protocols used in networks. It enables routers to exchange routing information to determine the best path for data packets. RIP uses **hop count** as a metric to measure the distance between source and destination, with a maximum hop limit of **15** (anything beyond 15 is considered unreachable).  

#### **Why Was RIP Created?**  
In the early days of networking, there was a need for a simple, standardized way for routers to communicate and share routing information. RIP was designed in the **1980s** to provide:  
- **Automated Routing** – Routers could dynamically update their tables instead of manual configuration.  
- **Simplicity** – Easy to implement with minimal processing power.  
- **Compatibility** – Worked across different vendors' network devices.  

#### **How Does RIP Work?**  
- Each router **broadcasts its routing table** to its neighbors every **30 seconds**.  
- Routers update their tables based on received information, choosing the shortest path (fewer hops).  
- If a route is unreachable for **180 seconds**, it is removed (RIP uses a timeout mechanism).  
- Uses **split horizon** and **hold-down timers** to reduce routing loops and ensure stability.  

#### **Versions of RIP**  
- **RIP v1** – Classful, does not support subnet masks (obsolete).  
- **RIP v2** – Classless, supports CIDR (still in use).  
- **RIPng** – An extension of RIP for IPv6 networks.  

#### **Applications of RIP**  
- **Small networks** – Due to its hop limit, RIP is best suited for small to medium-sized networks.  
- **Legacy systems** – Older hardware that cannot support more advanced protocols like OSPF or BGP.  
- **Educational purposes** – Used for learning about routing basics in networking courses.  

#### **Limitations of RIP**  
- **Slow convergence** – Takes time to recover from network changes.  
- **Scalability issues** – Not suitable for large networks due to the 15-hop limit.  
- **Inefficient routing** – Does not consider factors like bandwidth or latency, only hop count.  

#### **Why is RIP Still Relevant?**  
Despite its limitations, RIP is still used in certain environments where simplicity and compatibility matter more than efficiency. However, modern networks often prefer more advanced protocols like OSPF or EIGRP for better performance.  


# Table of Contents
1. [Network](#network-topology-diagram)</br>
2. [Best Practices](#best-practices)</br>
3. [Understanding Of Serial Ports](#serial-ports)</br>
4. Steps in RIP</br>
<ul>
<li>4.1<a href = "#step1-build-the-topology-as-seen-in-the-above-diagram">Build Network Topology</a> </li>
<li>4.2 <a href="#step2-statically-assign-the-ip-address-and-subnet-mask-for-the-pcs">Assign IP address for the PCs</a></li>
<li>4.3 <a href="step3-statically-assign-the-ip-address-of-fast-ethernet-00-port-for-both-pc0-and-pc1">Assign fa0/0 address for the Routers</a></li>
<li>4.4 <a href="#step4-statically-assign-the-default-gateway">Assign Default Gateway for the PCs</a></li>
<li>4.5 <a href="#step5-assign-ip-addresses-for-each-of-the-router-0">Assign IP address for serial ports of Router0</a></li>
<li>4.6 <a href="#step6-assign-ip-addresses-for-each-of-the-router-1">Assign IP address for serial ports of Router1</a></li>
<li>4.7 <a href="#step7-assign-ip-addresses-for-each-of-the-router-2">Assign IP address for serial ports of Router2</a></li>
<li>4.8 <a href="#step8-configure-rip-protocol">Configure RIP</a></li>
<li>4.9 <a href="#step9-simulation-of-rip">Simulate Working of RIP</a></li>
</ul>
5. <a href = "https://github.com/norac1243/RIP-Protocol/blob/main/README.md#when-simulation-fails-what-can-we-do-to-fix-it">How to fix Simulation Fails?</a>


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
<ul>
 <li>PC0 takes IP address: 10.0.0.2, Subnet Mask: 255.0.0.0 (represented by /8)</li>
 <li>PC1 takes IP address: 20.0.0.2, Subnet Mask: 255.0.0.0 (represented by /8)</li>
</ul>
</br></br>
To assign this, click on the PC icon > Desktop tab > IP Configuration.</br></br>
Assign as below:</br>
<b>FOR PC0:</b></br>
![PC0](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/3%20IP%20Configuration%20PC0.JPG)</br></br>
<b>FOR PC1:</b></br>
![PC1](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/3%20IP%20Configuration%20PC1.JPG)</br></br>
After assigning any IP address to any port or device, its best to label the port using the label icon present top
see [best practices](#best-practices). </br>

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

# STEP4: Statically Assign the Default Gateway
The default gateway in the PC is the IP address of the fa0/0 port of the router it's connected to. 
Therefore, for PC0 default gateway is 10.0.0.1 and for PC1 it's 20.0.0.1
Set Default gateway by clicking on:
PC0>Desktop > IP Configuration > Default Gateway
Do the same for PC1. 


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

# STEP5: Assign IP addresses for each of the Router 0
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

# STEP6: Assign IP addresses for each of the Router 1
For Router1, accrding to the [diagram](##network-topology-diagram),</br>
1. its serial port, on the line connecting router0 and router1, has IP address: 192.168.1.250/30</br>
For me its a DTE serial 2/0 port, so I typed in commands</br>
![5.1](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/step%205%20substep%20code%201.JPG)</br>

2. its serial port, on the line connecting router1 and router2, has IP address: 192.168.1.246/30</br>
For me its a DTE serial 3/0 port, so I typed in commands</br>
![5.2](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/step%205%20substep%20code%202.JPG)</br>

# STEP7: Assign IP addresses for each of the Router 2</br>
For Router2, accrding to the [diagram](##network-topology-diagram),</br>
1. its serial port, on the line connecting router0 and router2, has IP address: 192.168.1.253/30</br>
   For me its a DTE serial 2/0 port, so I typed in commands</br>
   ![6.1](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/step%206%20substep%20code%201.JPG)</br>
2. its serial port, on the line connecting router1 and router2, has IP address: 192.168.1.245/30</br>
   For me its a DCE serial 3/0 port, so I typed in commands</br>
   ![6.2](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/step%206%20substep%20code%202.JPG)</br>

# STEP8: Configure RIP Protocol</br>
1. For this one should get into global configuration mode first, that's by "conf t"</br>
2. Then "router rip"</br>
3. Then add the respective networks for each router </br>
Router 0:</br>
![rip r0](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/step%208%20router0.JPG)</br>
Router1:</br>
![rip r1](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/step%208%20router1.JPG)</br>
Router2:</br>
![rip r2](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/step%208%20router2.JPG)</br>


The question arises in how we determine the networks for each of these routers.
For this we will be doing and operations.

## For Router 0, we have 3 ports in use (fa0/0, se 2/0, se 3/0):
1. We have fa0/0: 10.0.0.1 having subnet address of 255.0.0.0
we find the first network address by performing on an AND operation on the binary forms of 10.0.0.1 and 255.0.0.0, which gives ya 10.0.0.0
2. Then we have se2/0: in my case its connected to  192.168.1.254/30
we find the network address by performing AND operation on binary forms of
- 192.168.1.254 and
- 255.255.255.252 (the subnet mask here is represented by 30, which in ip address form is 11111111.11111111.
11111111.11111100, which has a total of thirty 1s. convert this ip address to decimal and you will get 255.255.255.252)
- on performing and operation you get, 192.168.1.252
3. Then we have se3/0: in my case its connected to  192.168.1.249/30
we find the network address by performing AND operation on binary forms of
- 192.168.1.249 and
- 255.255.255.252 
- on performing and operation you get, 192.168.1.248


## For Router 1, we have 2 ports in use (se 2/0, se 3/0):
1. Then we have se2/0: in my case its connected to  192.168.1.250/30
we find the network address by performing AND operation on binary forms of
- 192.168.1.250 and
- 255.255.255.252
- on performing and operation you get, 192.168.1.248
2. Then we have se3/0: in my case its connected to  192.168.1.246/30
we find the network address by performing AND operation on binary forms of
- 192.168.1.246 and
- 255.255.255.252 
- on performing and operation you get, 192.168.1.240

## For Router 2, we have 3 ports in use (fa0/0, se 2/0, se 3/0):
1. We have fa0/0: 20.0.0.1 having subnet address of 255.0.0.0
we find the first network address by performing on an AND operation on the binary forms of 20.0.0.1 and 255.0.0.0, which gives ya 20.0.0.0
2. Then we have se2/0: in my case its connected to  192.168.1.253/30
we find the network address by performing AND operation on binary forms of
- 192.168.1.253 and
- 255.255.255.252 
- on performing and operation you get, 192.168.1.252
3. Then we have se3/0: in my case its connected to  192.168.1.245/30
we find the network address by performing AND operation on binary forms of
- 192.168.1.245 and
- 255.255.255.252 
- on performing and operation you get, 192.168.1.240

# STEP9: Simulation of RIP

Basically, RIP protocol uses the path / route that has the least number of hops to get from the source to the destination. To get from PC0 to PC1, we have two routes:</br>
Route1: PC0 <=> Router0 <=> Router2 <=> PC1</br>
Route2: PC0 <=> Router0 <=> Router1 <=> Router2 <=> PC1</br>
Route1 has lesser number of hops compared to Route2.</br>
Hence when we simulate the packet transmission from PC0 to PC1, it should take Route1.</br>
On removing Route1, RIP protocol chooses route2 to transmit packets from PC0 to PC1 since no other route exists</br>

To simulate,enter Simulation Mode in the Bottom Right Corner (blue arrow).</br>
Click the Envelope Icon and then click on PC0 and PC1 (red arrow)
</br>In the Simulation Panel, Edit Filters, Click ICMP under IPv4
</br> Then in play controls click capture forward to see the packet traverse route1. </br>
at the end of it you should get an event list encircled in pink below and the successful status message highlighted by yellow arrow. 
</br>
![sim route1](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/simulation-pic1.JPG)


</br>
Now get rid of the connection line between router0 and router2. 
</br>
Click the Envelope Icon and then click on PC0 and PC1
</br>
There is only one route in this case, that is route2, so the packets have no choice but to choose that route. </br>
![sim route2](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/simulation-pic2.JPG)

# When Simulation fails, what can we do to fix it?
Normally packet simulation doesn't work the first time. So try doing it two times more.That is the same step of clicking the Envelope Icon and then click on PC0 and PC1. </br></br></br>
If that doesn't work,check if you've entered the proper IP address for each device.</br>
click on a device and then click Config and check each port address. Also check the gateways of the PCs. </br>
On confirming correct port address, simulate once more. </br></br></br>
if that fails again, test the working of the individual connection lines. </br>
That is, Click the Envelope Icon and then click:</br>
1. PC0 and Router0</br>
2. PC1 and Router1</br>
3. Router0 and Router1</br>
4. Router0 and Router2</br>
and so on and so forth. </br></br></br>
if any of these connections fail, that means that there is an error in the 8th step,[Configure RIP](#step8configure-rip-protocol). If you have by mistake added a wrong network,make sure you are config mode and then after typing router rip you can type in this command to remove the wrong network is:</br>
"no network 20.0.0.0"</br>
where 20.0.0.0 can be understood as any wrong network. </br>
</br>
Test again. it should work.
# 
<i>Your support is appreciated! If this project helps you, consider starring ⭐ it. Proper credit is requested for any reuse.</i>

