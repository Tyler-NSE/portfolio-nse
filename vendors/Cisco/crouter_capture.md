---
layout: architect
---

# Cisco Router Packet Capture Guide

* * *

This guide is for performing a packet capture on a Cisco IOS router. For more complete documentation please see vendor documentation like [here](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/epc/command/epc-cr-book/epc-cr-m1.html).

## Quick Links
----------------------------------------------

- [Monitor Capture Command Syntax](#monitor-capture-command-syntax)
- [Syntax Description](#syntax-description)
- [Enable Packet Capture](#enable-packet-capture)
- [Define Capture Point](#define-capture-point)
- [Start Packet Capture](#start-packet-capture)
- [Stop Packet Capture](#stop-packet-capture)
- [Export Captured Packets](#export-captured-packets)
- [Additional Options](#additional-options)

## Monitor Capture Command Syntax
----------------------------------------------

monitor capture < buffer size size > < circular \| linear > [dot1q] < filter acl-num \| exp-acl-num \| acl-name > < length bytes > { clear [filter] \| export buffer location \| schedule at hh : mm : ss < date < month year > > \| start < for number { seconds \| packets } > \| stop }

no monitor capture < buffer size size > < circular \| linear > [dot1q] < filter acl-num \| exp-acl-num \| acl-name > < length bytes > < clear [filter] \| export buffer location \| schedule at hh : mm : ss < date < month year > > >

## Syntax Description
----------------------------------------------

| Option             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| buffer size size   | Specifies the capture buffer size in kilobytes. Range: 32 to 65535. Default: 2048 Kb.                                                                                                                                                                                                                                                                                                                                                                     |
| circular \| linear | Specifies a circular or linear capture buffer. The default is linear.                                                                                                                                                                                                                                                                                                                                                                                     |
| clear              | Clears the capture buffer and sets the number of captured packets to zero.                                                                                                                                                                                                                                                                                                                                                                                |
| dot1q              | Includes dot1q information in the monitor capturing.                                                                                                                                                                                                                                                                                                                                                                                                      |
| export buffer      | Exports to remote location.                                                                                                                                                                                                                                                                                                                                                                                                                               |
| filter             | Specifies that packets from a specified ACLs only are sent to the capture buffer.                                                                                                                                                                                                                                                                                                                                                                         |
| acl-num            | IP access list (standard or extended). Range: 1 to 199.                                                                                                                                                                                                                                                                                                                                                                                                   |
| exp-acl-num        | IP expanded access list (standard or extended). Range: 1300 to 2699.                                                                                                                                                                                                                                                                                                                                                                                      |
| acl-name           | ACL name.                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| length size        | Specifies the capture length of each packet in bytes. Range: 0 to 9216. Default: 68.                                                                                                                                                                                                                                                                                                                                                                      |
| location           | Location to dump capture buffer. Valid values are as follows: dot1q location --Specifies the dot1q capture buffer location.  bootflash: --Location to dump buffer.  disk0: --Location to dump buffer.  ftp: --Location to dump buffer.  http: --Location to dump buffer.  https: --Location to dump buffer.  rcp: --Location to dump buffer.  scp: --Location to dump buffer.  sup-bootdisk: --Location to dump buffer.  tftp: --Location to dump buffer. |
| schedule at        | Schedules the capture at a specific time/date.                                                                                                                                                                                                                                                                                                                                                                                                            |
| hh : mm : ss       | Time in hours:minutes:seconds. Range: hours: 0 to 23; minutes: 0 to 59; seconds: 0 to 59.                                                                                                                                                                                                                                                                                                                                                                 |
| date               | (Optional) Date. Range: 1 to 31.                                                                                                                                                                                                                                                                                                                                                                                                                          |
| month              | (Optional) Month. Range: 1 to 12.                                                                                                                                                                                                                                                                                                                                                                                                                         |
| start              | Starts capturing the packets to the beginning of the buffer.                                                                                                                                                                                                                                                                                                                                                                                              |
| for                | (Optional) Specifies the length of time in seconds or the number of packets.                                                                                                                                                                                                                                                                                                                                                                              |
| number             | Stops the capture after the specified number of seconds or packets. Range: 1 to 4294967295.                                                                                                                                                                                                                                                                                                                                                               |
| stop               | Moves the capture to the OFF state.                                                                                                                                                                                                                                                                                                                                                                                                                       |

## Enable Packet Capture
----------------------------------------------

Use the command to start configuring packet capture:

```
monitor capture buffer <buffer-name> size <size-in-kb> [circular | linear]
```

Example: "monitor capture buffer PACKET_CAP size 2048 circular"

## Define Capture Point
----------------------------------------------

After defining the buffer, you need to create a capture point:

```
monitor capture point ip cef <capture-point-name> <interface> both
```

Example: "monitor capture point ip cef CAPTURE_POINT GigabitEthernet0/1 both"

## Start Packet Capture
----------------------------------------------

To start capturing packets, use:

```
monitor capture point start <capture-point-name>
```

Example: "monitor capture point start CAPTURE_POINT"

## Stop Packet Capture
----------------------------------------------

To stop the capture, use:

```
monitor capture point stop <capture-point-name>
```

Example: "monitor capture point stop CAPTURE_POINT"

## Export Captured Packets
----------------------------------------------

To export the captured packets to a file for analysis (e.g., using Wireshark), use:

```
monitor capture buffer <buffer-name> export tftp://<tftp-server-ip>/<filename>
```

Example: "monitor capture buffer PACKET_CAP export tftp://192.168.1.100/capture.pcap"

## Additional Options
----------------------------------------------

### Filters: 

Access List Example: 

ip access-list extended BUF-Filter
permit ip host 192.168.1.1 host 172.16.1.1
permit ip host 172.16.1.1 host 192.168.1.1

Buffer Example: "monitor capture buffer PACKET_CAP size 2048 circular"

You can apply access lists to filter the captured packets:

```
monitor capture buffer <buffer-name> filter access-list <acl-name>
```

Example using above access list and buffer: "monitor capture buffer PACKET_CAP filter access-list BUF-Filter

### Clear Capture Buffer:

To clear the capture buffer, use:

```
monitor capture buffer <buffer-name> clear
```

* * *

[Back](/vendors/cisco.html)
