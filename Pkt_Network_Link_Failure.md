<b>Goal</b>: Setting up a simple packet topology controlled by Ryu. Then failing some of the optical and packet links and observing the behaviuor.   
<b>Requirements:</b>
A basic knowlege of Ryu, OpenFlow and linux CLI is required. 
Doing https://github.com/Ehsan70/Mininet_LINC_script/blob/master/LINCoe_and_iControl.md tutorial is a must. 

<b>Environment: </b> I have used the VM from sdn hub, I recommond you do the same. Link for installation is provided below: http://sdnhub.org/tutorials/sdn-tutorial-vm/

<b>Road Map: </b>This document has two sections for setup: 

 1. Setting up the network   
 2. Doing tests and experiments</br>

<b>Notations: </b>
 - `iControl>` Means the iControll command line


# 1. setting up the network and the controller#
 a. Run Ryu 
 If you are using SDN hub Vm, go to `/home/ubuntu/ryu` and run Ryu: 
 ```shell
 > sudo ./bin/ryu-manager --verbose ryu/app/simple_switch_13.py
 ```
 b. Start up the Mininet network 
 ```shell
 > sudo -E python SimpleOptTopoScratch.py
 ```