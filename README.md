# Link_Failure_in_Mininet_LINC
This repo provides some script, tutorials on creating topology, simulating optical and packet link failures

#Files
Here is the description of each file.

### ComplexPktTopo_PktLink_and_Taps.py
This file creates a packet network which is then connected to tap interfaces. This is usefull, because 
linc-oe switches can then be connected to the tap interfaces and create a mixed packet and optical topo. 
Have a look at OptPkt_Network_Link_Failure.md tutorial to see the instructions on creating optical and packet network. 

### Link_Failure_PktNet.py
Creates a simple topo with 3 switches.  

### OptPkt_Network_Link_Failure.md	
Seting up LINC-OE simple optical topology controlled by iControl and a packet simple topology controlled 
by Ryu. Then failing some of the optical and packet links and observing the behaviuor.

### Pkt_Network_Link_Failure.md
This file contains instruciton on setting up a simple packet topology controlled by Ryu. 
Then failing some of the optical and packet links and observing the behaviuor.


