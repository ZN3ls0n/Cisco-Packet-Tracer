This Cisco Packet Tracer lab will help you develop a NAT topology. This is a very simple one that allows you to expand and build new topologies. Feel free to change any IP addresses or add any devices. 
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

<pre><code>enable
 conf t
 int g0/0
 ip addr 172.16.1.1 255.255.255.252
 no shut
 int g0/1
 ip addr 192.168.100.1 255.255.255.0
 no shut
 ip route 10.1.1.0 255.255.255.240 172.16.1.2
 ip route 132.212.0.0 255.255.0.0 172.16.1.2
 </code></pre>


 ### R1 ###

 <pre><code>enable
   conf t
   int g0/0
   ip addr 172.16.1.2 255.255.255.252
   ip nat inside
   int g0/1
   ip addr 172.17.1.1 255.255.255.252
   ip nat outside
   int g0/2
   ip addr 10.1.1.1 255.255.255.240
   ip nat inside
 </code></pre>

 This is where you create your access lists that allow which IP addresses can be NATted.

 <pre><code>access-list 1 permit 192.168.100.0 0.0.0.255
   access-list 2 permit 10.1.0.0 0.0.15.255
    ip nat inside source list 1 int g0/1 overload
    ip nat inside source list 2 int g0/1 overload

   ip route 192.168.100.0 255.255.255.0 172.16.1.1 
   ip route 192.168.100.0 255.255.255.0 192.168.100.1 
   ip route 132.212.0.0 255.255.0.0 172.17.1.2 
 </code></pre>

### R2 ###

<pre><code>enable
 conf t
 int g0/0
 ip addr 172.17.1.2 255.255.255.252
 no shut
 int g0/1
 ip addr 132.212.0.1 255.255.0.0
 no shut
 ip route 10.1.1.0 255.255.255.240 172.17.1.1
 ip route 192.168.100.0 255.255.255.0 172.17.1.1
 </code></pre>

