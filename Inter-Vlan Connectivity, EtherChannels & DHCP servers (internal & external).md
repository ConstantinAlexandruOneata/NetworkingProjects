<h1>Inter-Vlan Connectivity, EtherChannels & DHCP </h1>

<h2>Description</h2>

This project involves configuring inter-VLAN connectivity, setting up EtherChannels for redundancy, and implementing DHCP servers for dynamic IP address allocation. It also includes enabling IPv6 and ensuring seamless inter-VLAN communication.

<hr>

<p>I will start this lab by adding 3 PCs to each of the 3 Layer 2 switches in the topology. </p>

<img src="Photos/image001.png"
id="image1.png" width="625" height="319" /></span></u>

<span style="font-size:12.0pt;line-height:115%"> </span>

<p>I then created and named the 3 corresponding VLANs: Sales, Engineering and Refunds</p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image002.png"
id="image2.png" width="624" height="169" /></span>

<span style="font-size:12.0pt;line-height:115%">And decided on the
following assignment of PCs / VLAN & Subnet / VLAN</span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image003.png"
id="image3.png" width="512" height="254" /></span>

<p>Next, I designated the above PCs to their corresponding VLANs and configured the switch ports
to act in unconditional access mode.</p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image004.png"
id="image4.png" width="624" height="288" /></span>

<span style="font-size:12.0pt;line-height:115%">The above commands have
been replicated accordingly on the other 2 switches in the topology.
</span>

<hr>

<p> Next, I will configure Layer 2 EtherChannels between the 3 switches for improved redundancy and to reduce STP convergence time in the event of a link failure. I will use static mode, PAgP and LACP.</p>

<h4>➤ Static Layer 2 EtherChannel </h4>

<p>The following configuration has been applied on both ends on the link between the
first group of switches.</p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image005.png"
id="image5.png" width="624" height="135" /></span>

<p>Following the addition of the port channel, trunking was enabled, and the corresponding VLANs
have been allowed on the trunk</p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image006.png"
id="image6.png" width="624" height="92" /></span>

<h4>➤ PAgP EtherChannel</h4>

<p>The following configuration has been applied on the first of the two switches in the
second group.</p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image007.png"
id="image7.png" width="624" height="104" /></span>

<p> And the second switch has been configured to initiate the negotiation and form the etherchannel. </p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image008.png"
id="image8.png" width="624" height="93" /></span>

<p> After that, both switches have been added the previous configuration to allow traffic from VLAN 10, 20 and
30, and the native VLAN. </p>

<h4>➤ LACP EtherChannel</h4>

<p>The first of the two switches in the third group have been configured as such:</p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image009.png"
id="image9.png" width="624" height="96" /></span>

<p>With the switch on the other end being configured as:  </p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image010.png"
id="image10.png" width="624" height="48" /></span>

<hr>

<h4>➤ Inter-Vlan Connectivity with Sub-interfaces </h4>

<p>Now that the two ports on both ends of the link have been configured as an etherchannel, the trunk formed, and the VLANs have been allowed on the trunk, I will
configure the sub-interfaces on the router. </p>

<p>Starting with the Gi0/0/0.10 subinterface configuration and static ip address assignment </p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image011.png"
id="image11.png" width="624" height="95" /></span>

<p>Second subinterface for VLAN 20</p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image012.png"
id="image12.png" width="624" height="64" /></span>

<p>And the third for VLAN 30</p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image013.png"
id="image13.png" width="624" height="64" /></span>

<p>Lastly, I will configure the physical interface with an IP address and a subnet mask to allow the native VLAN traffic through. </p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image014.png"
id="image14.png" width="624" height="44" /></span>

<p>Next, I will configure the router to act as the DHCP server. To do so, I started by defining the pools, the default router, and the DNS server for each
VLAN </p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image015.png"
id="image15.png" width="624" height="339" /></span>

<p>Then I added the “ip helper-address” command on the subinterfaces corresponding to each
VLAN</p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image016.png"
id="image16.png" width="624" height="420" /></span>

<p> Now that DHCP is active, the PCs in the topology can automatically get their configuration</p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image017.png"
id="image17.png" width="624" height="274" /></span>

<p>To test the configuration done so far I issued a ping from PC A in VLAN 10 to PC E in VLAN 20</p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image018.png"
id="image18.png" width="624" height="279" /></span>

<p>After that, I have enabled IPv6 on the router and created IPv6 DHCP pools for each VLAN
using unique local addresses</p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image019.png"
id="image19.png" width="624" height="250" /></span>

<p> Then, I configured the physical interface </p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image020.png"
id="image20.png" width="624" height="85" /></span>

<p> And the three subinterfaces</p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image021.png"
id="image21.png" width="624" height="236" /></span>

<p>With that, PC A now has both an IPv4 and an IPv6 configuration from the DHCP server</p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image022.png"
id="image22.png" width="625" height="461" /></span>

<p>And pinging PC E in VLAN 20 using the IPv6 address works as intended </p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image023.png"
id="image23.png" width="624" height="289" /></span>

<hr>

<h4>➤ Inter-Vlan Connectivity with SVI </h4>

<p> For simplicity sake, I copied the topology and maintained the same IP addressing scheme, but this time I will use a multilayer switch and create SVIs </p>

<p> I’ll start enabling routing using the “Ip routing” command, create the VLAN interfaces and assign IP addresses and masks for each</p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image024.png"
id="image24.png" width="624" height="68" /></span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image025.png"
id="image25.png" width="624" height="191" /></span>

<p> I then configured the link between the Layer 2 and the Layer 3 Switch as a trunk and allowed the corresponding VLANs through</p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image026.png"
id="image26.png" width="624" height="88" /></span>

<p> The DHCP server has been statically configured with the IP address 192.168.1.2 and the mask 255.255.255.0 </p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image027.png"
id="image27.png" width="624" height="177" /></span>

<p> 4 pools have been created within the DHCP server configuration </p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image028.png"
id="image28.png" width="493" height="340" /></span>

<p> And lastly, the ip-helper command was issued within each SVI, pointing at the ip  address of the DHCP server</p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image029.png"
id="image29.png" width="624" height="197" /></span>

<p> To check that the configuration works, I issued a ping from PC A (1) in VLAN 10 to PC E (1) in VLAN 20.</p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image030.png"
id="image30.png" width="624" height="282" /></span>

<p> To connect the two sites together, I prepared a different lab in which I will configure static & dynamic routing using OSPFv2, OSPFv3, EIGRPv4, EIGRPv6, and eBGP  </p>
  
<p> The second site which was originally configured with switched virtual interfaces and the same ip addressing scheme is now using a router as
the default gateway and the following ip addressing scheme </p>
  
<img src="Photos/image031.png"
id="image31.png" width="558" height="310" /></span>

<span style="font-size:12.0pt;line-height:115%">Follow this
</span>[<span style="font-size:12.0pt;line-height:
115%;color:#1155CC">link</span>](https://github.com/ConstantinAlexandruOneata/NetworkingProjects/blob/main/Connecting%20two%20Branch%20Offices%20with%20static%20routes%20%26%20dynamic%20routing%20protocols%20(OSPFv2%2C%20OSPFv3%2C%20EIGRP%2C%20EIGRPv6%2C%20BGP)%20%2B%20NAT%5CPAT.md)<span
style="font-size:12.0pt;line-height:
115%"> to see the next project</span>
