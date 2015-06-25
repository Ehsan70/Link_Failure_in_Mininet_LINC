<b>Goal</b>: Seting up LINC-OE simple optical topology controlled by iControl and a packet simple topology controlled by Ryu. Then failing some of the optical and packet links and observing the behaviuor.   
<b>Requirements:</b>
A basic knowlege of LINC-OE, TAP interfaces, Ryu, Erlang language and linux CLI is required. 
Doing https://github.com/Ehsan70/Mininet_LINC_script/blob/master/LINCoe_and_iControl.md tutorial is a must. 

<b>Environment: </b> I have used the VM from sdn hub, I recommond you do the same. Link for installation is provided below: http://sdnhub.org/tutorials/sdn-tutorial-vm/

<b>Road Map: </b>This document has two sections for setup: 

 1. setting up the network   
 2. Doing tests </br>

Then the tutorial would run couple of experminets. After the experminet the tutorial talkes about the details of the network and what is goingt on under the hood.   

<b>Notations: </b>
 - `>` means the linuc command line <br>
 - `iControl>` Means the iControll command line


# 1. setting up the network #
## Optical Network
 a. Run iControl: 
 ```shell
 > cd loom/iControl
 > rel/icontrol/bin/icontrol console
 ```
 The iControl starts and listens on 0.0.0.0:6653 </br>
 b. Clearting the tap interfaces: 

 c. Set up the `sys.config` file: 
 `rel/files/sys.config` file for the network shown above should looks as following:
```erlang
[{linc,
  [{of_config,disabled},
   {capable_switch_ports,
    [{port,1,[{interface,"tap1"}]},
     {port,2,[{interface,"tap2"}]},
     {port,3,[{interface,"tap3"}]},
     {port,4,[{interface,"dummy"}, {type, optical}]},
     {port,5,[{interface,"dummy"}, {type, optical}]},
	 {port,6,[{interface,"dummy"}, {type, optical}]},
     {port,7,[{interface,"tap4"}]},
     {port,8,[{interface,"dummy"}, {type, optical}]},
     {port,9,[{interface,"dummy"}, {type, optical}]},
     {port,10,[{interface,"dummy"}, {type, optical}]},
     {port,11,[{interface,"tap6"}]},
     {port,12,[{interface,"tap7"}]},
     {port,13,[{interface,"dummy"}, {type, optical}]},
     {port,14,[{interface,"dummy"}, {type, optical}]},
     {port,15,[{interface,"dummy"}, {type, optical}]},
     {port,16,[{interface,"dummy"}, {type, optical}]},
     {port,17,[{interface,"dummy"}, {type, optical}]},
     {port,18,[{interface,"dummy"}, {type, optical}]},
     {port,19,[{interface,"tap5"}]}
    ]},
   {capable_switch_queues, []},
   {optical_links, [{{1,5}, {2,1}}, {{1,4},{4,1}}, {{4,4},{2,2}}, {{4,3},{3,1}}, {{2,3},{3,4}}, {{2,4},{5,1}} ]},
   {logical_switches,
    [{switch,1,
      [{backend,linc_us4_oe},
       {controllers,[{"Switch0-Controller","localhost",6653,tcp}]},
       {controllers_listener,disabled},
       {queues_status,disabled},
       {datapath_id, "00:00:00:00:00:01:00:01"},
       {ports,[{port,1,[{queues,[]}, {port_no, 1}]},
       		   {port,2,[{queues,[]}, {port_no, 2}]},
       		   {port,3,[{queues,[]}, {port_no, 3}]},
               {port,4,[{queues,[]}, {port_no, 4}]},
               {port,5,[{queues,[]}, {port_no, 5}]}
              ]}]},
     {switch,2,
      [{backend,linc_us4_oe},
       {controllers,[{"Switch0-Controller","localhost",6653,tcp}]},
       {controllers_listener,disabled},
       {queues_status,disabled},
       {datapath_id, "00:00:00:00:00:01:00:02"},
       {ports,[{port,14,[{queues,[]}, {port_no, 1}]},
       		   {port,15,[{queues,[]}, {port_no, 2}]},
       		   {port,16,[{queues,[]}, {port_no, 3}]},
               {port,17,[{queues,[]}, {port_no, 4}]}
              ]}]},
     {switch,3,
      [{backend,linc_us4_oe},
       {controllers,[{"Switch0-Controller","localhost",6653,tcp}]},
       {controllers_listener,disabled},
       {queues_status,disabled},
       {datapath_id, "00:00:00:00:00:01:00:03"},
       {ports,[{port,10,[{queues,[]}, {port_no, 1}]},
               {port,11,[{queues,[]}, {port_no, 2}]},
               {port,12,[{queues,[]}, {port_no, 3}]},
               {port,13,[{queues,[]}, {port_no, 4}]}
              ]}]},
     {switch,4,
      [{backend,linc_us4_oe},
       {controllers,[{"Switch0-Controller","localhost",6653,tcp}]},
       {controllers_listener,disabled},
       {queues_status,disabled},
       {datapath_id, "00:00:00:00:00:01:00:04"},
       {ports,[{port,6,[{queues,[]}, {port_no, 1}]},
 			   {port,7,[{queues,[]}, {port_no, 2}]},
               {port,8,[{queues,[]}, {port_no, 3}]},
               {port,9,[{queues,[]}, {port_no, 4}]}
              ]}]},
     {switch,5,
      [{backend,linc_us4_oe},
       {controllers,[{"Switch0-Controller","localhost",6653,tcp}]},
       {controllers_listener,disabled},
       {queues_status,disabled},
       {datapath_id, "00:00:00:00:00:01:00:05"},
       {ports,[{port,18,[{queues,[]}, {port_no, 1}]},
               {port,19,[{queues,[]}, {port_no, 2}]}
              ]}]}
    ]}]},
 {of_protocol, [{no_multipart, false}]},
 {enetconf,
  [{capabilities,[{base,{1,1}},{startup,{1,0}},{'writable-running',{1,0}}]},
   {callback_module,linc_ofconfig},
   {sshd_ip,any},
   {sshd_port,1830},
   {sshd_user_passwords,[{"linc","linc"}]}]},
 {epcap,
  [{verbose, false},
   {stats_interval, 10},
   {buffer_size, 73400320}]},
 {lager,
  [{handlers,
    [{lager_console_backend,debug},
     {lager_file_backend,
      [{"log/error.log",error,10485760,"$D0",5},
       {"log/debug.log",debug,10485760,"$D0",5},
       {"log/console.log",info,10485760,"$D0",5}]}]}]},
 {sasl,
  [{sasl_error_logger,{file,"log/sasl-error.log"}},
   {errlog_type,error},
   {error_logger_mf_dir,"log/sasl"},
   {error_logger_mf_maxbytes,1048576000000},
   {error_logger_mf_maxfiles,5}]},
 {sync,
  [{excluded_modules, [procket]}]}].
```
d. start LINC-OE: 
 ```shell
 > make rel && sudo rel/linc/bin/linc console
 ```
## Packet Network
 a. Run Ryu 
 If you are using SDN hub Vm, go to `/home/ubuntu/ryu` and run Ryu: 
 ```shell
 > sudo ./bin/ryu-manager --verbose ryu/app/simple_switch_13.py
 ```
 b. Start up the Mininet network 
 ```shell
 > sudo -E python SimpleOptTopoScratch.py
 ```
