<h1>Connecting two branch offices with static routes & dynamic routing protocols (OSPFv2, OSPFv3, EIGRPv4, EIGRPv6 & eBGP) + NAT/PAT </h1>

<h2>Description</h2>

<p> In this lab, I will use NAT, dynamic routing protocols and static routes to connect two
sites (Building A & Building B) together. </p>

<p> Building A uses the following addressing scheme: </p>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image032.png"
id="image32.png" data-border="0" width="500" height="180" /></span>

<p> And Building B uses the addressing scheme below: </p>

<img src="Photos/image033.png"
id="image33.png" data-border="0" width="624" height="237" />  


<p> Firstly, I have prepared the following IP addressing scheme in IPv4 and IPv6 for the links between the routers, and assigned each interface with the corresponding
configuration </p>

<img src="Photos/image034.png" id="image34.png">

<hr>

<h3>➤ NAT/PAT </h3>

<p> Interfaces were configured with an IPv4 and IPv6 address matching the physical network diagram previously presented</p>

<img src="Photos/image035.png" id="image35.png" data-border="0" width="624" height="85" />
<img src="Photos/image036.png" id="image36.png" data-border="0" width="624" height="85" />

<p> Next, I created ACLs for the two sites, which I will later use for PAT </p>

<img src="Photos/image037.png" id="image37.png" data-border="0" width="624" height="137" />

<img src="Photos/image038.png" id="image38.png" data-border="0" width="624" height="153" />

<p> After that, the inside & outside interfaces were configured </p>

<img src="Photos/image039.png" id="image39.png" data-border="0" width="606" height="210" />

<p> Lastly, I will use the inside global address from the interface Gi0/0/1 on each router to
complete the PAT configuration </p>

<img src="Photos/image040.png" id="image40.png" data-border="0" width="625" height="21" />

<p> With that, ip hosts with private IP addresses in the above subnets can now reach other hosts on
the internet.</p>

<img src="Photos/image041.png" id="image41.png" data-border="0" width="624" height="165" />

<p> Next, I will configure a static mapping between the inside local address 172.16.10.100 of an HTTP server set up within subnet 172.16.10.0/24 to the inside global address 200.0.10.100, so that it can be reachable from other hosts on the internet</p>

<img src="Photos/image042.png" id="image42.png" data-border="0" width="623" height="53" />

<p> And since the inside and outside interfaces have already been configured, we can now check the connectivity, trying to reach the HTTP server from PC F in subnet
192.168.30.0/24 </p>

<img src="Photos/image043.png" id="image43.png" data-border="0" width="379" height="252" />

<hr>

<h3>➤ OSPFv2 & OSPFv3 </h3>

<h4> OSPFv2 Configuration </h4>

<p> OSPFv2 has been enabled on the following interfaces and subinterfaces using a single area
design. </p>

<img src="Photos/image044.png" id="image44.png" data-border="0" width="624" height="139" />

<p> The interfaces facing the private network were configured as passive-interfaces to reduce the CPU overhead and bandwidth.</p>

<img src="Photos/image045.png" id="image45.png" data-border="0" width="624" height="73" />

<p> The other 2 WAN interfaces have been configured using the newer interface configuration, and the rest of the routers in area 0 were configured in a similar
manner </p> 

<img src="Photos/image046.png" id="image46.png" data-border="0" width="624" height="140" />

<p> The point to point ethernet interfaces have been configured with the appropriate network type to reduce the CPU overhead and convergence time</p>

<img src="Photos/image047.png" id="image47.png" data-border="0" width="624" height="115" />

<p> Next, I will change the default reference bandwidth across all routers in area 0 to future proof the design for a potential bandwidth upgrade to 10Gbps </p>
<img src="Photos/image048.png" id="image48.png" data-border="0" width="625" height="89" />  
  
<p> Create a static default route on the edge router  </p>

<img src="Photos/image049.png" id="image49.png" data-border="0" width="624" height="28" />
  
<p> And enable the advertisement of default route information across the OSPF enabled routers  </p>

<img src="Photos/image050.png" id="image50.png" data-border="0" width="624" height="43" />

<p> With that, we now have dynamic entries into the OSPF routing table of RID 1.1.1.1 and a newly learnt default route</p>

<img src="Photos/image051.png" id="image51.png" data-border="0" width="624" height="552" />

<p> Lastly, a ping has been issued from PC E in VLAN 20 to the newly learnt route to 200.0.5.1 - the IP address of one of the OSPF router interfaces.</p>

<img src="Photos/image052.png" id="image52.png" data-border="0" width="624" height="264" />

<h4> OSPFv3 Configuration</h4>

<p> Now that IPv4 routes have been shared across the routers successfully, I will enable OSPFv3, starting with configuring link-local addresses across area 0.</p>

<img src="Photos/image053.png" id="image53.png" data-border="0" width="624" height="97" />

<p> And repeat the process across all the other routers for the following topology</p>

<img src="Photos/image054.png" id="image54.png" data-border="0" width="625" height="324" />

<p> Next, I will enable OSPFv3 for each router interface within the topology. Because I use an earlier version of IOS in Packet Tracer, I need to configure the routers
with the legacy commands “ipv6 router ospf”, “ipv6 ospf {process-id} area {area-id}...etc. </p>

<img src="Photos/image055.png" id="image55.png" data-border="0" width="468" height="262" />

<p> After identifying the interfaces that will enable OSPFv3, I will manually assign router IDs to each router in the topology</p>

<img src="Photos/image056.png" id="image56.png" data-border="0" width="624" height="69" />

<p> Change the network type to point-to-point for the ethernet interfaces </p>

<img src="Photos/image057.png" id="image57.png" data-border="0" width="624" height="51" />

<p> And configure the passive interfaces </p>

<img src="Photos/image058.png" id="image58.png" data-border="0" width="624" height="127" />

<p> Next, I will configure a static default route on the edge router</p>

<img src="Photos/image059.png" id="image59.png" data-border="0" width="624" height="60" />

<p> And enable the advertisement of default route information across the OSPFv3 enabled
routers</p>

<img src="Photos/image060.png" id="image60.png" data-border="0" width="624" height="47" />

<p> With that, we now have IPv6 routes and a new default route </p>

<img src="Photos/image061.png" id="image61.png" data-border="0" width="624" height="425" />

<p> And a ping was issued from PC D in VLAN 10 to 2001:1234:5678:9BBB::1, the IPv6 address on Router 11 GigabitEthernet Interface to test the connectivity  </p>

<img src="Photos/image062.png" id="image62.png" data-border="0" width="529" height="220" />

<h3>➤ EIGRPv4 & EIGRPv6 </h3>

<h4> EIGRPv4 Configuration</h4>

<p> I will start the configuration by creating the EIGRP process and defining the interfaces which will enable EIGRP on each router, starting with Router 1</p>

<img src="Photos/image063.png" id="image63.png" data-border="0" width="624" height="116" />

<p> The same configuration with the appropriate parameters has been applied across the rest of the
routers. </p>

<p> Next, I will configure the passive-interfaces </p>

<img src="Photos/image064.png" id="image64.png" data-border="0" width="624" height="96" />

<p> Configure a static default route on the edge router </p>

<img src="Photos/image065.png" id="image65.png" data-border="0" width="624" height="57" />
  
<p> And enable the redistribution of the recently configured static default route across the EIGRPv4 enabled routers </p>
  
<img src="Photos/image066.png" id="image66.png" data-border="0" width="624" height="53" /> 
  
<p> With that, we now have newly learnt IP routes in our routing table, including a default route </p>

<img src="Photos/image067.png" id="image67.png" data-border="0" width="624" height="515" />

<p> And we can issue a ping to 200.0.7.1/24 from PC A’s 172.16.10.7/24</p>

<img src="Photos/image068.png" id="image68.png" data-border="0" width="624" height="279" />

<h4> EIGRPv6 Configuration</h4>

<p> Firstly, I will create the EIGRPv6 process, assign router IDs and enable EIGRP with the “no shutdown” command across the routers, starting with router 0</p>

<img src="Photos/image069.png" id="image69.png" data-border="0" width="624" height="97" />

<p> Next, I will configure the interfaces for EIGRPv6 </p>

<img src="Photos/image070.png" id="image70.png" data-border="0" width="437" height="274" />

<p> And select which interfaces will act as passive interfaces</p>

<img src="Photos/image071.png" id="image71.png" data-border="0" width="624" height="127" />

<p> Configure a static default route on the edge router </p>
  
<img src="Photos/image072.png" id="image72.png" data-border="0" width="624" height="21" />  
  
<p> And enable the redistribution of the recently configured static default route across the EIGRPv6 enabled routers </p>
  
<img src="Photos/image073.png" id="image73.png" data-border="0" width="624" height="79" />

<p> With that, we now have newly learnt IPv6 routes in our routing table, including a default route </p>

<img src="Photos/image074.png" id="image74.png" data-border="0" width="623" height="467" />

<p> Lastly, I will send a ping from PC F in VLAN 30 to 2001:1234:5678:9BBC::1 - the IPv6 address of one of the routers interfaces</p>

<img src="Photos/image075.png" id="image75.png" data-border="0" width="624" height="253" />

<h3>➤ eBGP </h3>

<p> Now that the OSPF and EIGRP networks have been configured and the routes learnt by every device in each topology, I will connect the two together using
eBGP.</p>

<p> The following IP addressing scheme and AS numbers assignment has been applied</p>

<img src="Photos/image076.png" id="image76.png" />

<p> I will start by configuring the edge routers to enable BGP for AS 65100 and AS 65200, and specify the neighbours on each router</p>

<img src="Photos/image077.png" id="image77.png" data-border="0" width="624" height="96" />

<img src="Photos/image078.png" id="image78.png" data-border="0" width="624" height="60" />

<img src="Photos/image079.png" id="image79.png" data-border="0" width="624" height="59" />

<p> Next, I will enable the routers to exchange prefixes, starting with the OSPF routers</p>

<img src="Photos/image080.png" id="image80.png" data-border="0" width="624" height="63" />

<p> Then the EIGRP routers </p>

<img src="Photos/image081.png" id="image81.png" data-border="0" width="624" height="56" />

<p> With that, both OSPF and EIGRP routes show up in the routing tables of the BGP enabled routers </p>

<img src="Photos/image082.png" id="image82.png" data-border="0" width="606" height="607" />

<p> And a ping from PC I in AS 65100 was sent to check connectivity with Router 0(1) in AS
65200</p>

<img src="Photos/image083.png" id="image83.png" data-border="0" width="624" height="277" />
