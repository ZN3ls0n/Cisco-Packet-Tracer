This Cisco Packet Tracer lab will help you develop a NAT topology. This is a very simple one that allows you to expand and build new topologies. 
## Details ##
### LAN (192.168.100.0/24) ###
<ul>
  <li>One PC (192.168.100.23)</li>
  <li>One switch</li>
  <li>One router</li>
    <ul>
      <li>LAN Gateway (g0/1): 192.168.100.1</li>
</ul>

### DMZ/NAT Router(10.1.1.0/28) ###
<ul>
  <li>One internal web server (10.1.1.3)</li>
  <li>One router</li>
    <ul>
      <li>DMZ Gateway (g0/2): 10.1.1.1</li>
    </ul>
</ul>

### WAN (132.212.0.0/16)
<ul>
  <li>One web server (132.212.210.10)</li>
  <li>One router</li>
    <ul>
      <li>WAN Gateway (g0/1): 132.212.0.1</li>
    </ul>
</ul>

### Inter-Router Links ###
<ul>
  <li>R0 (g0/0) and R1 (g0/0) - 172.16.1.0/30</li>
    <ul>
      <li>R0 (g0/0): 172.16.1.1</li>
      <li>R1 (g0/0): 172.16.1.2</li>
    </ul>
  <li>R1 (g0/1) and R2 (g0/0) - 172.17.1.0/30</li>
    <ul>
      <li> R1 (g0/1): 172.17.1.1</li>
      <li>R2 (g0/0): 172.17.1.2</li>
    </ul>
</ul>


### R0 ###

<code>enable
 conf t
 int g0/0
 ip addr 172.16.1.1 255.255.255.252
 no shut
 int g0/1
 ip addr 192.168.100.1 255.255.255.0
 no shut
 ip route 10.1.1.0 255.255.255.240 172.16.1.2
 ip route 132.212.0.0 255.255.0.0 172.16.1.2
 </code>


