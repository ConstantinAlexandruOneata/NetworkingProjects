**<span style="font-size:20.0pt;line-height:115%">Routing redundancy &
Security using HSRP, DHCP Snooping, DAI, Port Security and ACL</span>**

**<span style="font-size:20.0pt;line-height:115%"> </span>**

<u><span
style="font-size:12.0pt;line-height:115%">Description</span></u>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">I will start this lab by
adding a second router to building B from the previous topology
presented in </span>[<span style="font-size:12.0pt;
line-height:115%;color:#1155CC">“Connecting two Branch Offices with
static routes & dynamic routing protocols (OSPFv2, OSPFv3, EIGRP,
EIGRPv6, BGP) + NAT/PAT”</span>](https://github.com/ConstantinAlexandruOneata/NetworkingProjects/blob/main/Connecting%20two%20Branch%20Offices%20with%20static%20routes%20%26%20dynamic%20routing%20protocols%20(OSPFv2%2C%20OSPFv3%2C%20EIGRP%2C%20EIGRPv6%2C%20BGP)%20%2B%20NAT%5CPAT.md)<span
style="font-size:12.0pt;line-height:115%">  
  
</span>

1.  **<span style="font-size:12.0pt;line-height:115%">HSRP - Hot Standby
    Router Protocol</span>**

**<span style="font-size:12.0pt;
line-height:115%"> </span>**

<span style="font-size:12.0pt;line-height:115%">The following ip
addressing scheme was selected for the router interfaces</span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image084.png"
id="image84.png" data-border="0" width="624" height="108" /></span>

<span style="font-size:12.0pt;line-height:115%">I will now define the
HSRP instances, the virtual IP addresses for both routers, and enable
preemption, starting with Router A</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image085.png"
id="image85.png" data-border="0" width="624" height="79" /></span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image086.png"
id="image86.png" data-border="0" width="624" height="79" /></span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image087.png"
id="image87.png" data-border="0" width="624" height="76" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">After repeating the
process on Router B, I will change the priority for the instances 10 and
30 on Router A to 105 so that router A will become the active router for
VLAN 10 and VLAN 30, and so that I can balance the traffic between the
two Routers</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image088.png"
id="image88.png" data-border="0" width="624" height="104" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Next, I will issue the
following show command to check the configuration on Router A  
  
</span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image089.png"
id="image89.png" data-border="0" width="624" height="109" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Then, I will use a
shutdown command on the sub-interface gi0/0/0.20 on Router B (the active
router for VLAN 20)  
  
</span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image090.png"
id="image90.png" data-border="0" width="526" height="70" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Now that Router B’s
interface is down, I used the same show command to check if the failover
mechanism works as expected  
  
</span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image091.png"
id="image91.png" data-border="0" width="624" height="113" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

2.  **<span style="font-size:12.0pt;line-height:115%">DHCP
    Snooping</span>**

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">The following switches
will be configured for DHCP Snooping, DAI and Port Security </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image092.png"
id="image92.png" data-border="0" width="624" height="525" /></span>

<span style="font-size:12.0pt;line-height:115%">And will use the
following VLAN & IP addressing scheme</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image093.png"
id="image93.png" data-border="0" width="490" height="142" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">First, I will enable
DHCP snooping for each VLAN, and disable the information option</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image094.png"
id="image94.png" data-border="0" width="624" height="133" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">After the configuration
has been replicated across the other two switches, I will now designate
the trusted interfaces on each switch </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image095.png"
id="image95.png" data-border="0" width="624" height="107" /></span>

<span style="font-size:12.0pt;line-height:115%">And check the
configuration </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image096.png"
id="image96.png" data-border="0" width="485" height="236" /></span>

3.  **<span style="font-size:12.0pt;line-height:115%">DAI - Dynamic ARP
    Inspection </span>**

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Continuing from the
previous configuration of DHCP Snooping, I will now enable DAI for every
VLAN </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image097.png"
id="image97.png" data-border="0" width="624" height="119" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">And configure the
trusted interfaces</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image098.png"
id="image98.png" data-border="0" width="624" height="99" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Then, I will enable
additional message checks </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image099.png"
id="image99.png" data-border="0" width="624" height="19" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">And verify the
configuration using the following show command </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image100.png"
id="image100.png" data-border="0" width="624" height="211" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

4.  **<span style="font-size:12.0pt;line-height:115%">Port Security
    </span>**

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Having already
configured each port as either static access or trunk, I will now enable
port security on the switches interfaces</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image101.png"
id="image101.png" data-border="0" width="624" height="85" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Since Packet Tracer
doesn’t allow err-recovery, I will change the violation mode to
restrict, so that the interface will stay up if a violation
occurs</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image102.png"
id="image102.png" data-border="0" width="624" height="17" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Then, I will change the
default maximum number of mac addresses allowed per interface to 20 for
each interface that connects to another switch. I will also enable
dynamic learning of mac addresses through “switchport port-security
mac-address sticky”. </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image103.png"
id="image103.png" data-border="0" width="624" height="56" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Next, I will manually
configure the interface gi0/1 of Switch 3 that connects to Router 0 with
Router 0’s MAC address. </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image104.png"
id="image104.png" data-border="0" width="624" height="17" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Lastly, I will check the
configuration with the following show commands </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image105.png"
id="image105.png" data-border="0" width="624" height="492" /></span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image106.png"
id="image106.png" data-border="0" width="452" height="244" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

5.  <span style="font-size:12.0pt;line-height:115%">ACL - Access Control
    Lists</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">For this section I will
create 3 access lists in total - 2 extended ACLs and 1 standard,
defining multiple access control entries and implementing the lists for
different purposes. </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Starting with an
extended named ACL with sequencing numbers, I will first define the ACL
on Router 0 - the default gateway from the previous topology </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image107.png"
id="image107.png" data-border="0" width="624" height="32" /></span>

<span style="font-size:12.0pt;line-height:115%">Then, I will create a
statement to deny access to the web server 200.0.10.100 from host
192.168.30.4 in VLAN 30  
  
</span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image108.png"
id="image108.png" data-border="0" width="623" height="32" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">After that, I will allow
other hosts in VLAN 30 to access the same web server         </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image109.png"
id="image109.png" data-border="0" width="624" height="39" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Deny telnet connection
attempts from addresses starting with 192.168.x.x and going to any
hosts, but allow the same addresses to connect to any hosts using SSH
instead</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image110.png"
id="image110.png" data-border="0" width="623" height="35" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Lastly, I will override
the default implicit deny.</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image111.png"
id="image111.png" data-border="0" width="624" height="36" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Next, I will check the
ACL just created </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image112.png"
id="image112.png" data-border="0" width="624" height="112" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">I will remove statement
30</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image113.png"
id="image113.png" data-border="0" width="562" height="140" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">And choose the
interfaces and the direction in which the ACL will filter the traffic  
  
</span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image114.png"
id="image114.png" data-border="0" width="624" height="241" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">To verify the operations
of this newly created ACL I tried to connect to the HTTP server using
the web browser of PC F, and received the following error </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image115.png"
id="image115.png" data-border="0" width="624" height="500" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Next, I will create a
simple standard ACL and allow two internet hosts terminal access into
Router 0</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image116.png"
id="image116.png" data-border="0" width="624" height="97" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">I will now create a
different extended ACL which will filter inbound traffic on Router 0’s
WAN interfaces </span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image117.png"
id="image117.png" data-border="0" width="624" height="29" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Deny any telnet
connection attempts into our network</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image118.png"
id="image118.png" data-border="0" width="624" height="29" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">And permit SSH sessions
from a subset of trusted hosts</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image119.png"
id="image119.png" data-border="0" width="624" height="44" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">I will then give SNMP
access to the same subset of hosts, and deny any other attempts to
establish an SNMP session from unauthorised hosts  
  
</span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image120.png"
id="image120.png" data-border="0" width="624" height="60" /></span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span style="font-size:12.0pt;line-height:115%">Lastly I will override
the default implicit deny and configure the interfaces and the direction
for this ACL</span>

<span style="font-size:12.0pt;line-height:115%"> </span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image121.png"
id="image121.png" data-border="0" width="624" height="36" /></span>

<span
style="font-size:12.0pt;line-height:115%"><img src="Photos/image122.png"
id="image122.png" data-border="0" width="624" height="120" /></span>

</div>
