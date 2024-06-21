# RIP-Protocol
RIP protocol for MCN SEM 6 RC19-20 

# Table of Contents

# Network Topology Diagram 
![topology](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/1st%20network%20topo.JPG)
# BEST PRACTICES:
## Set the Preferences to show port labels. 
This does help while assigning ip addresses to each port.
To navigate to preferences, either,
1. click on Options and then Preferences
2. Ctrl+R
Choose "Always Show Port Labels"
![preferences](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/2%20preferences.JPG)
##

# STEP1: Build the topology as seen in the above diagram.
Note the Network Devices being used are
- Generic (Router-PT)
- Generic (PC-PT)

# STEP2: Statically Assign the IP address and Subnet Mask for the PCs
Accoridng to the diagram,
PC0 takes IP address: 10.0.0.2, Subnet Mask: 255.0.0.0 (represented by /8)
PC1 takes IP address: 20.0.0.2, Subnet Mask: 255.0.0.0 (represented by /8)
To assign this, click on the PC icon > Desktop tab > IP Configuration.
Assign as below:
![PC0](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/3%20IP%20Configuration%20PC0.JPG)
![PC1](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/3%20IP%20Configuration%20PC1.JPG)
After assigning any IP address to any port or device, its best to label the port using the label icon present top
see [best practices](#best-practices). 

# STEP3: Statically Assign the IP address of Fast Ethernet 0/0 port for both PC0 and PC1
Fast Ethernet 0/0 or Fa0/0 is the port in your router that connects to a PC. 
Hence we can set it up for both Router0 and Router1 connected to PC0 and PC1 respectively.
Click on Router0 and then on CLI. 
Type in below::
![Router0 fa0/0](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/3%20Router%200%20ip%20set%20fa00.JPG)
Explanation::
1. First type in no / n to exit configuration dialog
2. Then press Enter key (=Return)
3. Type in "en" (short) or "enable" (full) 
4. Enter global configuration mode by typing in  "conf t" (short) or "configure terminal" (full) 
5. To set IP address of fa0/0 or FastEthernet0/0 we navigate to it by typing,
 "int fa0/0" (short) or "int FastEthernet0/0 " (full) 
6. Enter the IP address, that is, 10.0.0.0.1 with subnet mask, 255.0.0.0 (which is represented by /8)
By either typing,
"ip add 10.0.0.1 255.0.0.0"(short)
"ip address 10.0.0.1 255.0.0.0"(full)
7. Boot the port, that is change the state from down to up using command,
"no shut" (short)
"no shutdown" (full)
8. Type in "exit" to get out off fa0/0

That's it!
Do the same for router2 set for fa0/0, IP address as 20.0.0.0.1 with subnet mask, 255.0.0.0 
![Router 2 fa0/0](https://github.com/norac1243/RIP-Protocol/blob/main/PICTURES%20-%20RIP/3%20Router2%20ip%20set%20fa00.JPG)

# SERIAL PORTS:
Note that each Router can connect to another Router, (int the case of Router-PT) via serial ports.
These serial ports are 
1. Serial 2/0 
2. Serial 3/0
By labelling the ports, you will now see the ports highlighted as Se2/0 (for Serial 2/0) and Se3/0 (for Serial 3/0).
These serial ports can either be DCE or DTE.
1. For DCE, It requires clock rate and bandwidth to be set.
2. DTE, It doesnt require clock rate and bandwidth to be set.
To find out which of your ports are DCE and which is DTE, you can either:
1. Label your ports as shown here. DCE ports are labelled by a clock.
2. Use a command, "show controller serial 2/0" (replace 2/0 by 3/0 for serial 3/0)
note: this command does not work in global configuration mode. So if you are in global configuration mode, get out of it by either using "exit" or Ctrl+C

# STEP4: Assign IP addresses for each of the Router 0

For Router0, accrding to the diagram___________, 
1. its serial port, on the line connecting router0 and router2, has IP address: 192.168.1.254/30
To set IP address:
1. First check what kind of port this is. For me its a DCE serial 2/0. For you, instead of this it can be DCE serial 3/0, DTE serial 2/0 or DTE serial 3/0 . So properly note that before proceeding.
___________
2. Since mine is a DCE serial 2/0, I do the following commands. Some commands are marked "Only for DCE". These commands need not be implemented for DTE.
__________________
[1] Enter global configuration mode by typing in  "conf t" (short) or "configure terminal" (full) 
[2] To set IP address of se2/0 (in my case) we navigate to it by typing,
 "int serial 2/0" 
if its se3/0 in your case, command:  "int serial 3/0" 
[3] Enter the IP address, that is 192.168.1.254 with subnet mask, 255.255.255.252 (which is represented by /30)
By typing,
"ip add 192.168.1.254 255.255.255.252"
[4] [only for DCE] now you gotta set clock rate and bandwidth. We mostly use standard measurements bandwidth as 64 and clock rate as 64000 unless externally specified.
The commands are:
"clock rate 64000"
"bandwidth 64"
[5] Boot the port, that is change the state from down to up using command,
"no shut" (short)
"no shutdown" (full)
[6] Type in "exit" to get out of serial2/0 (in my case)

2. its serial port, on the line connecting router0 and router1, has IP address: 192.168.1.249/30
In my case this port is DCE serial 3/0.
Type in commands: ________________


# STEP5: Assign IP addresses for each of the Router 1
For Router1, accrding to the diagram___________, 
1. its serial port, on the line connecting router0 and router1, has IP address: 192.168.1.250/30
For me its a DTE serial 2/0 port, so I typed in commands
__________

2. its serial port, on the line connecting router1 and router2, has IP address: 192.168.1.246/30
For me its a DTE serial 3/0 port, so I typed in commands
__________

# STEP6: Assign IP addresses for each of the Router 2
1. its serial port, on the line connecting router0 and router2, has IP address: 192.168.1.253/30
2. its serial port, on the line connecting router1 and router2, has IP address: 192.168.1.245/30






