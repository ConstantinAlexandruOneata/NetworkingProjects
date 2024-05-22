<div class="WordSection1">

**<span style="font-size:20.0pt;line-height:115%">1.<span
style="font:7.0pt &quot;Times New Roman&quot;"> </span></span><span
style="font-size:20.0pt;line-height:115%">Inter-Vlan Connectivity,
EtherChannels & DHCP servers (internal & external)</span>**

**<span style="font-size:20.0pt;line-height:115%"> </span>**

<u><span
style="font-size:12.0pt;line-height:115%">Description</span></u>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">I will start this lab by
adding 3 PCs to each of the 3 Layer 2 switches in the topology.</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<u><span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image001.png"
id="image1.png" width="625" height="319" /></span></u>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">I then created and named
the 3 corresponding VLANs: Sales, Engineering and Refunds</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image002.png"
id="image2.png" width="624" height="169" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">And decided on the
following assignment of PCs / VLAN & Subnet / VLAN</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image003.png"
id="image3.png" width="512" height="254" /></span>

<span style="font-size:12.0pt;line-height:115%">Next, I designated the
above PCs to their corresponding VLANs and configured the switch ports
to act in unconditional access mode.</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image004.png"
id="image4.png" width="624" height="288" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">The above commands have
been replicated accordingly on the other 2 switches in the topology.
</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Next I will configure
Layer 2 EtherChannels between the 3 switches for improved redundancy and
to reduce STP convergence time in the event of a link failure. I will
use static mode, PAgP and LACP.</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">●<span
style="font:7.0pt &quot;Times New Roman&quot;">     </span></span><span
style="font-size:12.0pt;line-height:115%">Static Layer 2 EtherChannel
</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">The following
configuration has been applied on both ends on the link between the
first group of switches.</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image005.png"
id="image5.png" width="624" height="135" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Following the addition
of the port channel, trunking was enabled, and the corresponding VLANs
have been allowed on the trunk</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image006.png"
id="image6.png" width="624" height="92" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">●<span
style="font:7.0pt &quot;Times New Roman&quot;">     </span></span><span
style="font-size:12.0pt;line-height:115%">PAgP EtherChannel</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">The following
configuration has been applied on the first of the two switches in the
second group.</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image007.png"
id="image7.png" width="624" height="104" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">The second switch has
been configured to initiate the negotiation and form the etherchannel  
  
</span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image008.png"
id="image8.png" width="624" height="93" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Both switches have been
added the previous configuration to allow traffic from VLAN 10, 20 and
30, and the native VLAN</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">●<span
style="font:7.0pt &quot;Times New Roman&quot;">     </span></span><span
style="font-size:12.0pt;line-height:115%">LACP EtherChannel</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">The first of the two
switches in the third group have been configured as such:</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image009.png"
id="image9.png" width="624" height="96" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">With the switch on the
other end being configured as:  
  
</span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image010.png"
id="image10.png" width="624" height="48" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Now that the two ports
on both ends of the link have been configured as an etherchannel, the
trunk formed, and the VLANs have been allowed on the trunk, I will
configure the sub-interfaces on the router. </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Starting with the
Gi0/0/0.10 subinterface configuration and static ip address assignment
</span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image011.png"
id="image11.png" width="624" height="95" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Second subinterface for
VLAN 20</span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image012.png"
id="image12.png" width="624" height="64" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">And the third for VLAN
30</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image013.png"
id="image13.png" width="624" height="64" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Lastly, I will configure
the physical interface with an IP address and a subnet mask to allow the
native VLAN traffic through. </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image014.png"
id="image14.png" width="624" height="44" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Next I will configure
the router to act as the DHCP server.</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">To do so, I started by
defining the pools and the default router, and the DNS server for each
VLAN</span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image015.png"
id="image15.png" width="624" height="339" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Then I added the “ip
helper-address” command on the subinterfaces corresponding to each
VLAN</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image016.png"
id="image16.png" width="624" height="420" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Now that DHCP is active,
the PCs in the topology can automatically get their configuration</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image017.png"
id="image17.png" width="624" height="274" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">To test the
configuration done so far I issued a ping from PC A in VLAN 10 to PC E
in VLAN 20</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image018.png"
id="image18.png" width="624" height="279" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">After that, I have
enabled ipv6 on the router and created ipv6 DHCP pools for each VLAN
using unique local addresses</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image019.png"
id="image19.png" width="624" height="250" /></span>

<span style="font-size:12.0pt;line-height:115%">  
Then, I configured the physical interface  
  
</span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image020.png"
id="image20.png" width="624" height="85" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">And the three
subinterfaces</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image021.png"
id="image21.png" width="624" height="236" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">With that, PC A now has
both an IPv4 and an IPv6 configuration from the DHCP server</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image022.png"
id="image22.png" width="625" height="461" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">And pinging PC E in VLAN
20 using the ipv6 address works as intended  
  
</span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image023.png"
id="image23.png" width="624" height="289" /></span>

<span style="font-size:12.0pt;
line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">●<span
style="font:7.0pt &quot;Times New Roman&quot;">     </span></span><span
style="font-size:12.0pt;line-height:115%">Inter-Vlan Connectivity with
SVI & External DHCP Server</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">For simplicity sake, I
copied the topology and maintained the same IP addressing scheme, but
this time I will use a multilayer switch and create SVIs </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">I’ll start enabling
routing using the “Ip routing” command, create the VLAN interfaces and
assign IP addresses and masks for each</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image024.png"
id="image24.png" width="624" height="68" /></span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image025.png"
id="image25.png" width="624" height="191" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">I then configured the
link between the Layer 2 and the Layer 3 Switch as a trunk and allowed
the corresponding VLANs through</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image026.png"
id="image26.png" width="624" height="88" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">The DHCP server has been
statically configured with the IP address 192.168.1.2 and the mask
255.255.255.0</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image027.png"
id="image27.png" width="624" height="177" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">4 pools have been
created within the external DHCP server configuration</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image028.png"
id="image28.png" width="493" height="340" /></span>

<span style="font-size:12.0pt;line-height:115%">And lastly, the
ip-helper command was issued within each SVI, pointing at the ip 
address of the DHCP server</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image029.png"
id="image29.png" width="624" height="197" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">To check that the
configuration works, I issued a ping from PC A (1) in VLAN 10 to PC E
(1) in VLAN 20.</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image030.png"
id="image30.png" width="624" height="282" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">To connect the two sites
together, I prepared a different lab in which I will configure static &
dynamic routing using OSPFv2, OSPFv3, EIGRP, EIGRPv6, and eBGP  
  
The second site which was originally configured with switched virtual
interfaces and the same ip addressing scheme is now using a router as
the default gateway and the following ip addressing scheme  
  
<img src="Photos/image031.png"
id="image31.png" width="558" height="310" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Follow this
</span>[<span style="font-size:12.0pt;line-height:
115%;color:#1155CC">link</span>](https://github.com/ConstantinAlexandruOneata/NetworkingProjects/blob/main/Connecting%20two%20Branch%20Offices%20with%20static%20routes%20%26%20dynamic%20routing%20protocols%20(OSPFv2%2C%20OSPFv3%2C%20EIGRP%2C%20EIGRPv6%2C%20BGP)%20%2B%20NAT%5CPAT.md)<span
style="font-size:12.0pt;line-height:
115%"> to see the next project</span>

<span style="font-size:12.0pt;line-height:115%"> </span>
