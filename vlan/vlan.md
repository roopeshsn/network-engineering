# VLAN

Virtual Extensible LAN - VLAN

## Why VLAN?

Think of this scenario. The company you work for has a 5-floor office building. Each team works on each floor. Your team works on the 5th floor. Your company's IT team has a Switch setup for every floor to serve the employees. These switches are connected in series from bottom to top. Say if an employee wants to connect with the intranet and internet, they need to use Ethernet cables. One fine day you are a bit late to the office and immediately want to see the messages that your team sent via your office intranet chat application. So you stood up on the first floor and connected your device with the switch. You opened the chat application and saw the messages. 

What are your inferences, right? Take 2 minutes and think before reading further.

The inferences in this situation are
- Your whole office's employees, including you, are part of one single big broadcast domain, meaning no segmentation across teams.
- One team's messages will be seen by other teams also, meaning no security. 

TODO: Complete the above scenario.

## What is a VLAN?

VLAN is a solution to have multiple broadcast domains in a single switch. Each VLAN corresponds to a broadcast domain, meaning one VLAN's traffic will be switched to only the ports that are part of that VLAN, not to every VLAN. This is achieved by giving an identity to every frame. This is known as VLAN tagging.

## VLAN Tagging or 802.1Q

Every frame will be tagged with a VLAN ID or number. So that when the peer switch receives a frame, it will identify which VLAN that frame belongs to.

## Modes of Switchport
- Access Mode
- Trunk Mode

### Access Mode
A port that is configured as access mode, then any frame that is sent or received from that port will be untagged. An access is meant to work with a single VLAN. That's why the switch won't tag a frame that is sent out from an access port; it also expects an untagged frame that is received in this port.

### Trunk Mode
A trunk port will carry traffic of multiple VLANs. A port that is configured as trunk mode will both tag and untag the frame that it is sent out or received in from that port.

What if a trunk port receives an untagged frame? How should it handle it? There is no VLAN configuration on a trunk port until now, like an access port.

#### Native VLAN
To handle this, the concept of the native VLAN arose. If a port that is configured as a trunk and native VLAN 10 receives an untagged frame, then it will be considered as VLAN 10's traffic.

Also, the point to note here is that we know that the trunk port will always tag a frame with the VLAN ID. But in the scenario of a native VLAN, that trunk port won't tag a frame if it belongs to the VLAN that is configured as a native VLAN. In this case, VLAN 10. In other words, that trunk port won't tag a frame that originated from VLAN 10 because the native VLAN configuration of that port is also VLAN 10. That frame will be sent as untagged.

### Summary

| Switchport Mode / Frame Type | Tagged Frame                  | Untagged Frame                                |
| -----------------------------| ----------------------------- | ----------------------------------------------|
| Access                       | Drops the frame               | Assigns it to the VLAN configured on the port |
| Trunk                        | Untag it, forward or flood it | Assigns it to the Native VLAN of the port     |

## What is SVI?

Let's discuss a bit about SVIs. SVIs are abbreviated as Switch Virtual Interfaces. As the name says, it's a virtual interface, meaning you can't see it physically. You can think of it as a Layer-3 or routed port. It is configurable using an IP address.