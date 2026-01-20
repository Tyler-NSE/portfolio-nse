---
layout: default
---

# Fortinet Capture and Troubleshooting Commands

## Table of Contents

- [Real-Time Debugging of Traffic](#real-time-debugging-of-traffic)
- [Session and System Diagnostics](#session-and-system-diagnostics)
- [Packet Capture with Sniffer](#packet-capture-with-sniffer)
- [Firewall Policy Lookup](#firewall-policy-lookup)
- [Connectivity Checks](#connectivity-checks)


### Real-Time Debugging of Traffic

    # Common flow debug commands:
    diagnose debug reset
    diagnose debug flow filter clear
    diagnose debug flow filter proto <tcp|udp|icmp|...>   # Optional
    diagnose debug flow filter addr <x.x.x.x>            # Optional
    diagnose debug console timestamp enable
    diagnose debug flow show function-name enable
    diagnose debug flow show iprope enable
    diagnose debug enable
    diagnose debug flow trace start 100   # Capture 100 packets
    # -- Watch the output, then stop --
    diagnose debug disable

### Session and System Diagnostics

    # View all active sessions:
    diagnose sys session list
    # Filter sessions by source or destination:
    diagnose sys session filter src <x.x.x.x>
    diagnose sys session filter dst <x.x.x.x>
    # Clear all sessions (use with caution):
    diagnose sys session clear
    # System process usage:
    diagnose sys top
    

### Packet Capture with Sniffer

    # Basic sniffer example:
    diagnose sniffer packet any "host x.x.x.x" 4 100
    # Syntax:
    # diagnose sniffer packet <interface> "<filter>" <verbosity> <count>
    # - <verbosity> 4 = detailed; 3 = less verbose
    # - <count> = number of packets


### Firewall Policy Lookup

	# Basic policy lookup Example:
	diagnose firewall iprope lookup x.x.x.x 12345 x.x.x.x 443 6 port34
	# Syntax:
	diagnose firewall iprope Lookup <src_ip><src_port><dst_ip><dst_port><protocol><device>
	# - <src_ip> = Source IP address
	# - <src_port> = Source port
	# - <dst_ip> = Destination IP addrewss
	# - <dst_port> = Destination port
	# - <protocol> = Protocol
	# - <device> = Source interface

### Connectivity Checks

    execute ping <destination_ip>
    execute traceroute <destination_ip>

[Back](/vendors/fortinet.html)

