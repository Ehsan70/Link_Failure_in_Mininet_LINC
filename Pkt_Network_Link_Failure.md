<b>Goal</b>: Setting up a simple packet topology controlled by Ryu. Then failing some of the optical and packet links and observing the behaviuor.   
<b>Requirements:</b>
A basic knowlege of Ryu, OpenFlow and linux CLI is required. 

<b>Environment: </b> I have used the VM from sdn hub, I recommond you do the same. Link for installation is provided below: http://sdnhub.org/tutorials/sdn-tutorial-vm/

<b>Road Map: </b>This document has two sections for setup: 

 1. Setting up the network   
 2. Doing tests and experiments</br>

<b>Notations: </b>
 - `iControl>` Means the iControll command line


# 1. Setting up the network and the controller #
 a. Run Ryu 
 If you are using SDN hub Vm, go to `/home/ubuntu/ryu` and run Ryu: 
 ```shell
 > sudo ./bin/ryu-manager --verbose ryu/app/simple_switch_13.py
 ```
 b. Start up the Mininet network 
 ```shell
 > sudo -E python Link_Failure_PktNet.py
 ```
# 2. Doing some tests and observing the behavior 
When the controller and the topo are up and running, I do the follwoing in the Mininet CLI: 

1. pingall
2. bring a link down
3. pingall
4. bring the link up again
5. pingall

The captured packets can be found in [mn_ryu_linkfailure_of3.pcapng](https://github.com/Ehsan70/Link_Failure_in_Mininet_LINC/blob/master/WiresharkTests/mn_ryu_linkfailure_of3.pcapng). 
Here is the topo: 
![Alt text](resources/PktNet_3SWs_3Hosts.jpg?raw=true  "Packet Network for link failure testing")

Note that when a link goes down, odp_port_status messages are sent to the controller from switch. Here is the structure of this message: 

![Alt text](resources/OFPT_PORT_STATUS_v13.jpg?raw=true  "Structure of the ofp_port_status in open flow version 1.3")

