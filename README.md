# Configuring DHCP on a Router for Multiple VLANs with Switches and Multi-Layer Switches

## Configuring the Switch(es)
### 1. Create your VLANs and name them
```enable```
```conf t```
```vlan {VLAN_ID}```
```name {VLAN_NAME}```
```exit```
# Repeat the above steps for each VLAN to put in the switch

# 2. Set up ports for the VLAN
```int range {INTERFACE-RANGE}```
```switchport mode access```
```switchport access {VLAN_ID}```
```exit```

# Replace {INTERFACE-RANGE} with the appropriate port range, such as fa0/1-3
# Replace {VLAN_ID} with the VLAN number

# 3. Create a VLAN trunk
```int {INTERFACE}```
```switchport mode trunk```
```exit```

# Replace {INTERFACE} with the switch port that will co

## Configuring the Multilayer Switch
# 4. Create the VLANs and Name them
```enable```
```conf t```
```vlan {VLAN_ID}```
```name {VLAN_NAME}```
```exit```
# Repeat the above steps for each VLAN to put in the multilayer switch

# 5. Create a VLAN trunk
```int range {INTERFACE-RANGE}```
```switchport mode trunk```
```exit```

# Replace {INTERFACE} with all the ports that are connected to switches/routers
