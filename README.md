# Configuring DHCP on a Router for Multiple VLANs with Switches and Multi-Layer Switches

## Configuring the Switch(es)
### 1. Create your VLANs and name them
<pre><code>
enable

conf t

vlan {VLAN_ID}

name {VLAN_NAME}

exit
</code></pre>
 Repeat the above steps for each VLAN to put in the switch

### 2. Set up ports for the VLAN
<pre><code>
int range {INTERFACE-RANGE}

switchport mode access

switchport access {VLAN_ID}

exit
</code></pre>

 Replace {INTERFACE-RANGE} with the appropriate port range, such as fa0/1-3.
 
 Replace {VLAN_ID} with the VLAN number

### 3. Create a VLAN trunk
<pre><code>
int {INTERFACE}
 
switchport mode trunk

exit

</code></pre>



 Replace {INTERFACE} with the switch port


## Configuring the Router
### 4. Create subinterfaces

<pre><code>
enable

conf t

int {INTERFACE}.{VLAN_ID}

encapsulation dot1q {VLAN_ID}

ip address {IP ADDR} {SUBNET MASK}

exit
 
</code></pre>

 Replace interface with each interface used on the router. 
 Replace VLAN ID for the VLAN number that will identify tagged traffic for that VLAN
 The IP address will be for each subinterface used for inter-VLAN routing. 


 ### 5. Configure DHCP service

 <pre><code>

  service dhcp

  ip dhcp pool {TITLE}

  network {IP ADDR} {SUBNET MASK}

  default-router {IP ADDR} 
  
 </code></pre>

Replace {TITLE} with the name of your VLAN
You can choose your default router IP address to be the IP address of your subinterface
