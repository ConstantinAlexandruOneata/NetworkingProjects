<h1>Inter-Vlan Connectivity, EtherChannels & DHCP </h1>

<h2>Description</h2>

This project involves configuring inter-VLAN connectivity, setting up EtherChannels for redundancy, and implementing DHCP servers for dynamic IP address allocation. It also includes enabling IPv6 and ensuring seamless inter-VLAN communication.

<hr>

<p>I will start this lab by adding 3 PCs to each of the 3 Layer 2 switches in the topology </p>

<img src="Photos/image001.png" id="image1.png" />

<p> I then created and named the 3 corresponding VLANs: Sales, Engineering and Refunds </p>

<img src="Photos/image002.png" id="image2.png" width="624" height="169" />

<p> And decided on the following assignment of PCs / VLAN & Subnet / VLAN </p>

<img src="Photos/image003.png" id="image3.png" width="512" height="254" />

<p>Next, I designated the above PCs to their corresponding VLANs and configured the switch ports to act in unconditional access mode </p>

<img src="Photos/image004.png" id="image4.png" width="624" height="288" />

<p> The above commands have been replicated accordingly on the other 2 switches in the topology </p>

<hr>

<p> Next, I will configure Layer 2 EtherChannels between the 3 switches for improved redundancy and to reduce STP convergence time in the event of a link failure. I will use static mode, PAgP and LACP </p>

<h3>➤ Static Layer 2 EtherChannel </h3>

<p>The following configuration has been applied on both ends on the link between the first group of switches </p>

<img src="Photos/image005.png" id="image5.png" width="624" height="135" />

<p> Following the addition of the port channel, trunking was enabled, and the corresponding VLANs have been allowed on the trunk</p>

<img src="Photos/image006.png" id="image6.png" width="624" height="92" />

<h3>➤ PAgP EtherChannel</h3>

<p> The following configuration has been applied on the first of the two switches in the second group </p>

<img src="Photos/image007.png" id="image7.png" width="624" height="104" />

<p> And the second switch has been configured to initiate the negotiation and form the etherchannel </p>

<img src="Photos/image008.png" id="image8.png" width="624" height="93" />

<p> After that, both switches have been added the previous configuration to allow traffic from VLAN 10, 20 and 30, and the native VLAN </p>

<h3>➤ LACP EtherChannel</h3>

<p> The first of the two switches in the third group have been configured as such:</p>

<img src="Photos/image009.png" id="image9.png" width="624" height="96" />

<p>With the switch on the other end being configured as:  </p>

<img src="Photos/image010.png" id="image10.png" width="624" height="48" />

<hr>

<h3>➤ Inter-Vlan Connectivity with Sub-interfaces </h3>

<p> Now that the etherchannels have been configured, the trunks formed, and the VLANs have been allowed on the trunks, I will configure the sub-interfaces on the router, starting with the Gi0/0/0.10 subinterface configuration and static ip address assignment </p>

<img src="Photos/image011.png" id="image11.png" width="624" height="95" />

<p> Second subinterface for VLAN 20 </p>

<img src="Photos/image012.png" id="image12.png" width="624" height="64" />

<p> And the third for VLAN 30 </p>

<img src="Photos/image013.png" id="image13.png" width="624" height="64" />

<p> Lastly, I will configure the physical interface with an IP address and a subnet mask to allow the native VLAN traffic through. </p>

<img src="Photos/image014.png" id="image14.png" width="624" height="44" />

<p> Next, I will configure the router to act as the DHCP server. To do so, I started by defining the pools, the default router, and the DNS server for each
VLAN </p>

<img src="Photos/image015.png" id="image15.png" width="624" height="339" />

<p> Then, I added the “ip helper-address” command on the subinterfaces corresponding to each VLAN</p>

<img src="Photos/image016.png" id="image16.png" width="624" height="420" />

<p> Now that DHCP is active, the PCs in the topology can automatically get their configuration </p>

<img src="Photos/image017.png" id="image17.png" width="624" height="274" />

<p> To test the connectivity, I issued a ping from PC A in VLAN 10 to PC E in VLAN 20 </p>

<img src="Photos/image018.png" id="image18.png" width="624" height="279" />

<p> After that, I have enabled IPv6 on the router and created IPv6 DHCP pools for each VLAN using unique local addresses</p>

<img src="Photos/image019.png" id="image19.png" width="624" height="250" />

<p> Then, I configured the physical interface </p>

<img src="Photos/image020.png" id="image20.png" width="624" height="85" />

<p> And the three subinterfaces </p>

<img src="Photos/image021.png" id="image21.png" width="624" height="236" />

<p> With that, PC A now has both an IPv4 and an IPv6 configuration from the DHCP server </p>

<img src="Photos/image022.png" id="image22.png" width="625" height="461" />

<p> And pinging PC E in VLAN 20 using the IPv6 address works as intended </p>

<img src="Photos/image023.png" id="image23.png" width="624" height="289" />

<hr>

<h3>➤ Inter-Vlan Connectivity with SVIs </h3>

<p> For simplicity sake, I copied the topology and maintained the same IP addressing scheme, but this time I will use a multilayer switch and SVIs </p>

<p> I’ll start enabling routing using the “Ip routing” command, create the VLAN interfaces and assign IP addresses and masks for each </p>

<img src="Photos/image024.png" id="image24.png" width="624" height="68" />

<img src="Photos/image025.png" id="image25.png" width="624" height="191" />

<p> I then configured the link between the Layer 2 and the Layer 3 Switch as a trunk and allowed the corresponding VLANs through</p>

<img src="Photos/image026.png" id="image26.png" width="624" height="88" />

<p> Next, I have statically configured the DHCP server with the IP address 192.168.1.2 and the mask 255.255.255.0 </p>

<img src="Photos/image027.png" id="image27.png" width="624" height="177" />

<p> And created 4 pools within the DHCP server </p>

<img src="Photos/image028.png" id="image28.png" width="493" height="340" />

<p> Lastly, I issued the ip-helper command on each SVI, pointing at the ip address of the DHCP server</p>

<img src="Photos/image029.png" id="image29.png" width="624" height="197" />

<p> To check that the configuration works, I issued a ping from PC A (1) in VLAN 10 to PC E (1) in VLAN 20.</p>

<img src="Photos/image030.png" id="image30.png" width="624" height="282" />

<p> To connect the two sites together, I have prepared a different lab in which I will configure static & dynamic routing using OSPFv2, OSPFv3, EIGRPv4, EIGRPv6, & eBGP  </p>
  
<p> The second site which was originally configured with switched virtual interfaces and the same ip addressing scheme is now using a router as
the default gateway and the following ip addressing scheme </p>
  
<img src="Photos/image031.png"
id="image31.png" width="558" height="310" /></span>

Follow this [link](https://github.com/ConstantinAlexandruOneata/NetworkingProjects/blob/main/Connecting%20two%20Branch%20Offices%20with%20static%20routes%20%26%20dynamic%20routing%20protocols%20(OSPFv2%2C%20OSPFv3%2C%20EIGRP%2C%20EIGRPv6%2C%20BGP)%20%2B%20NAT%5CPAT.md) to see the next project</span>
