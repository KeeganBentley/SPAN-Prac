# SPAN-Prac
Small practical activity to configure a SPAN port on CISCO OS with packet tracer. 

### Instructions 
First ping between the two PC's: 
- On PC0 > ping 1.1.1.2

Verify you see no ICMP packets on the 'sniffer' (GUI tab)

Next we will enable interface f0/24 to be a SPAN port replicating traffic on f0/1 and f0/2:
Click on the switch and go to the CLI tab
```cisco
enable
configure terminal
monitor session 1 source interface f0/1
monitor session 1 source interface f0/2
monitor session 1 destination interface f0/24
do show monitor
```
You should see the following:
```cisco
Session 1
---------
Type                   : Local Session
Description            : -
Source Ports           : 
    Both               : Fa0/1,Fa0/2
Destination Ports      : Fa0/24
    Encapsulation      : Native
          Ingress      : Disabled
```

To verify the SPAN is functioning, rerun the ping and look for the ICMP packets on the sniffer. 

This exercise effectively demonstrates the basic configuration and use of a SPAN port for monitoring network traffic. However, it is important to remember the limitations inherent in the SPAN technique when utilising it on a production network:

**Resource Limitations:**
SPAN sessions can place additional load on the switch, especially if multiple sessions or high-traffic ports are monitored. This can lead to resource contention, potentially impacting network performance.

**Incomplete Traffic Capture:**
SPAN ports may not capture all packets, especially under high traffic conditions. Some packets could be dropped due to buffer limitations or congestion, leading to an incomplete view of the network activity.

**Packet Integrity:**
The integrity of mirrored packets can be compromised, as SPAN does not guarantee that all packets will be mirrored accurately. This can be particularly problematic when monitoring time-sensitive or sensitive data.
