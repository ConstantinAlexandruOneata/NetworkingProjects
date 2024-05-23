<h1> Routing redundancy & Security using HSRP, DHCP Snooping, DAI, Port Security and ACL</h1>

<h2> Description </h2>

<p>This lab builds on the previous topology presented in <a href="https://github.com/ConstantinAlexandruOneata/NetworkingProjects/blob/main/Connecting%20two%20Branch%20Offices%20with%20static%20routes%20%26%20dynamic%20routing%20protocols%20(OSPFv2%2C%20OSPFv3%2C%20EIGRP%2C%20EIGRPv6%2C%20BGP)%20%2B%20NAT%5CPAT.md" title="Connecting two Branch Offices with static routes & dynamic routing protocols (OSPFv2, OSPFv3, EIGRPv4, EIGRPv6 & eBGP) + NAT/PAT">“Connecting two Branch Offices with static routes & dynamic routing protocols (OSPFv2, OSPFv3, EIGRP, EIGRPv6, BGP) + NAT/PAT”</a>. The project enhances network resilience and security through the implementation of HSRP for redundancy, DHCP Snooping to prevent rogue DHCP servers, Dynamic ARP Inspection to mitigate ARP spoofing, Port Security to restrict unauthorized devices, and ACLs for traffic filtering and access control.</p>

<hr>

<h4> ➤ HSRP - Hot Standby Router Protocol</h4>

<p> The following IP addressing scheme was selected for the router interfaces</p>

<img src="Photos/image084.png" id="image84.png" data-border="0" width="624" height="108" />

<p> I will now define the HSRP instances, the virtual IP addresses for both routers, and enable preemption, starting with Router A</p>

<img src="Photos/image085.png" id="image85.png" data-border="0" width="624" height="79" />

<img src="Photos/image086.png" id="image86.png" data-border="0" width="624" height="79" />

<img src="Photos/image087.png" id="image87.png" data-border="0" width="624" height="76" />

<p> After repeating the process on Router B, I will change the priority for the instances 10 and 30 on Router A to 105 so that router A will become the active router for VLAN 10 and VLAN 30, and so that I can balance the traffic between the two Routers</p>

<img src="Photos/image088.png" id="image88.png" data-border="0" width="624" height="104" />

<p> Next, I will issue the following show command to check the configuration on Router A </p>

<img src="Photos/image089.png" id="image89.png" data-border="0" width="624" height="109" />

<p> Then, I will use a shutdown command on the sub-interface gi0/0/0.20 on Router B (the active
router for VLAN 20) </p>

<img src="Photos/image090.png" id="image90.png" data-border="0" width="526" height="70" />

<p> Now that Router B’s interface is down, I used the same show command to check if the failover mechanism works as expected </p>

<img src="Photos/image091.png" id="image91.png" data-border="0" width="624" height="113" />

<hr>

<h4>➤ DHCP Snooping</h4>

<p> The following switches will be configured for DHCP Snooping, DAI and Port Security </p>

<img src="Photos/image092.png" id="image92.png" data-border="0" width="624" height="525" />

<p> And will use the following VLAN & IP addressing scheme</p>

<img src="Photos/image093.png" id="image93.png" data-border="0" width="490" height="142" />

<p> First, I will enable DHCP snooping for each VLAN, and disable the information option</p>

<img src="Photos/image094.png" id="image94.png" data-border="0" width="624" height="133" />

<p> After the configuration has been replicated across the other two switches, I will now designate the trusted interfaces on each switch </p>

<img src="Photos/image095.png" id="image95.png" data-border="0" width="624" height="107" />

<p> And check the configuration </p>

<img src="Photos/image096.png" id="image96.png" data-border="0" width="485" height="236" />

<hr>

<h4>➤ DAI - Dynamic ARP Inspection </h4>

<p> Continuing from the previous configuration of DHCP Snooping, I will now enable DAI for every VLAN </p>

<img src="Photos/image097.png" id="image97.png" data-border="0" width="624" height="119" />

<p> And configure the trusted interfaces</p>

<img src="Photos/image098.png" id="image98.png" data-border="0" width="624" height="99" />

<p> Then, I will enable additional message checks </p>

<img src="Photos/image099.png" id="image99.png" data-border="0" width="624" height="19" />

<p> And verify the configuration using the following show command </p>

<img src="Photos/image100.png" id="image100.png" data-border="0" width="624" height="211" />

<hr>

<h4>➤ Port Security </h4>

<p> Having already configured each port as either static access or trunk, I will now enable port security on the switches interfaces</p>

<img src="Photos/image101.png" id="image101.png" data-border="0" width="624" height="85" />

<p> Since Packet Tracer doesn’t allow err-recovery, I will change the violation mode to restrict, so that the interface will stay up if a violation
occurs</p>

<img src="Photos/image102.png" id="image102.png" data-border="0" width="624" height="17" />

<p> Then, I will change the default maximum number of mac addresses allowed per interface to 20 for each interface that connects to another switch. I will also enable
dynamic learning of mac addresses through “switchport port-security mac-address sticky”. </p>

<img src="Photos/image103.png" id="image103.png" data-border="0" width="624" height="56" />

<p> Next, I will manually configure the interface gi0/1 of Switch 3 that connects to Router 0 with Router 0’s MAC address. </p>

<img src="Photos/image104.png" id="image104.png" data-border="0" width="624" height="17" />

<p> Lastly, I will check the configuration with the following show commands </p>

<img src="Photos/image105.png" id="image105.png" data-border="0" width="624" height="492" />

<img src="Photos/image106.png" id="image106.png" data-border="0" width="452" height="244" />

<hr>

<h4>➤ ACL - Access Control Lists </h4>

<p> For this section I will create 3 access lists in total - 2 extended ACLs and 1 standard, defining multiple access control entries and implementing the lists for
different purposes. </p>

<p> Starting with an extended named ACL with sequencing numbers, I will first define the ACL on Router 0 - the default gateway from the previous topology </p>

<img src="Photos/image107.png" id="image107.png" data-border="0" width="624" height="32" />

<p> Then, I will create a statement to deny access to the web server 200.0.10.100 from host 192.168.30.4 in VLAN 30 </p>

<img src="Photos/image108.png" id="image108.png" data-border="0" width="623" height="32" />

<p> After that, I will allow other hosts in VLAN 30 to access the same web server </p>

<img src="Photos/image109.png" id="image109.png" data-border="0" width="624" height="39" />

<p> Deny telnet connection attempts from addresses starting with 192.168.x.x and going to any hosts, but allow the same addresses to connect to any hosts using SSH
instead </p>

<img src="Photos/image110.png" id="image110.png" data-border="0" width="623" height="35" />

<p> Lastly, I will override the default implicit deny.</p>

<img src="Photos/image111.png" id="image111.png" data-border="0" width="624" height="36" />

<p> Next, I will check the ACL just created </p>

<img src="Photos/image112.png" id="image112.png" data-border="0" width="624" height="112" />

<p> I will remove statement 30</p>

<img src="Photos/image113.png" id="image113.png" data-border="0" width="562" height="140" />

<p> And choose the interfaces and the direction in which the ACL will filter the traffic </p>

<img src="Photos/image114.png" id="image114.png" data-border="0" width="624" height="241" />

<p> To verify the operations of this newly created ACL I tried to connect to the HTTP server using the web browser of PC F, and received the following error </p>

<img src="Photos/image115.png" id="image115.png" data-border="0" width="624" height="500" />

<p> Next, I will create a simple standard ACL and allow two internet hosts terminal access into Router 0 </p>

<img src="Photos/image116.png" id="image116.png" data-border="0" width="624" height="97" />

<p> I will now create a different extended ACL which will filter inbound traffic on Router 0’s WAN interfaces </p>

<img src="Photos/image117.png" id="image117.png" data-border="0" width="624" height="29" />

<p> Deny any telnet connection attempts into our network</p>

<img src="Photos/image118.png" id="image118.png" data-border="0" width="624" height="29" />

<p> And permit SSH sessions from a subset of trusted hosts</p>

<img src="Photos/image119.png" id="image119.png" data-border="0" width="624" height="44" />

<p> I will then give SNMP access to the same subset of hosts, and deny any other attempts to establish an SNMP session from unauthorised hosts </p>

<img src="Photos/image120.png" id="image120.png" data-border="0" width="624" height="60" />

<p> Lastly I will override the default implicit deny and configure the interfaces and the direction for this ACL</p>

<img src="Photos/image121.png" id="image121.png" data-border="0" width="624" height="36" /></p>

<img src="Photos/image122.png" id="image122.png" data-border="0" width="624" height="120" />
