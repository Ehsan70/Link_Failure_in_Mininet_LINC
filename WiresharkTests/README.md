
#File Description

Following procidure is applied to all of the tests: 
 1. pingall
 2. bring a link down
 3. pingall
 4. bring the link up again
 5. pingall


#### mn_pox_linkfailure_of1.pcapng
- This file contains packets exchanged between pox controller and simple packet network. 
- Note that packet network is created by "sudo -E python Link_Failure_PktNet.py 
- Pox does not support 1.3. 
- Note that Pox is openflow 1.0 capable while  the switches are 1.3 so they agree on 1.0. 
- Above scenarios is applied. 

#### mn_ryu_linkfailure_of3.pcapng
- This file contains packets exchanged between ryu controller and simple packet network. 
- Note that packet network is created by "sudo -E python Link_Failure_PktNet.py  
- Note that Ryu is openflow 1.3 capable and the switches are 1.3 so they agree on 1.3. 
- Above scenarios is applied. 

#### mn_ryu_linc_PktOpt_linkfailure.pcapng
- This file contains 
 - packets exchanged between ryu controller and packet network. 
 - packets exchanged between icontrol controller and optical network. 
- Note that packet network is created by "sudo -E python Link_Failure_PktNet.py  
- Note that Ryu is openflow 1.3 capable and the switches are 1.3 so they agree on 1.3. 
- Above scenarios is applied. 
- Follow instructions at [OptPkt_Network_Link_Failure.md](https://github.com/Ehsan70/Link_Failure_in_Mininet_LINC/blob/master/OptPkt_Network_Link_Failure.md)


