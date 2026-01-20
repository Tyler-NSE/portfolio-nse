---
layout: default
---

## Table of Contents

- [Configure Packet Capture with the CLI](#configure-packet-capture-with-the-cli)
- [Available Capture Types on the ASA](#available-capture-types-on-the-asa)
- [Defaults](#defaults)
- [View the Captured Packets](#view-the-captured-packets)
- [Download from the ASA for Offline Analysis](#download-from-the-asa-for-offline-analysis)
- [Clear a Capture](#clear-a-capture)
- [Stop a Capture](#stop-a-capture)


### Configure Packet Capture with the CLI

Start the packet capture process with the capture command in privileged EXEC mode. In this configuration example, the capture named capin is defined. Bind it to the inside interface, and specify with the match keyword that only the packets that match the traffic of interest are captured:

![Branching](https://gt-legend.github.io/assets/img/vendor_img/cisco/asa_capin.PNG)
 
Similarly, the capture named capout is defined. Bind it to the outside interface, and specify with the match keyword that only the packets that match the traffic of interest are captured:

![Branching](https://gt-legend.github.io/assets/img/vendor_img/cisco/asa_capout.PNG)

The ASA now begins to capture the traffic flow between the interfaces. In order to stop the capture at anytime, enter the no capture command followed by the capture name.

Here is an example:

no capture capin interface inside
no capture capout interface outside 


### Available Capture Types on the ASA

This section describes the different types of captures that are available on the ASA.

* asa_dataplane - Captures packets on the ASA backplane that pass between the ASA and a module that uses the backplane, such as the ASA CX or IPS module.

![Branching](https://gt-legend.github.io/assets/img/vendor_img/cisco/asa_dataplane.PNG)

* asp-drop drop-code - Captures packets that are dropped by the accelerated security path. The drop-code specifies the type of traffic that is dropped by the accelerated security path.

![Branching](https://gt-legend.github.io/assets/img/vendor_img/cisco/asa_asp-drop.PNG)

* ethernet-type type - Selects an Ethernet type to capture. Supported Ethernet types include 8021Q, ARP, IP, IP6, LACP, PPPOED, PPPOES, RARP, and VLAN.

![Branching](https://gt-legend.github.io/assets/img/vendor_img/cisco/asa-ethernet-type.PNG)

* real-time - Displays the captured packets continuously in real-time. In order to terminate a real-time packet capture, press Ctrl-C. In order to permanently remove the capture, use the no form of this command.

* This option is not supported when you use the cluster exec capture command.

![Branching](https://gt-legend.github.io/assets/img/vendor_img/cisco/asa-real-time.PNG)

* Trace - Traces the captured packets in a manner similar to the ASA packet tracer feature.

ASA#cap in interface Webserver trace match tcp any any eq 80

// Initiate Traffic

![Branching](https://gt-legend.github.io/assets/img/vendor_img/cisco/asa-trace1.PNG)

![Branching](https://gt-legend.github.io/assets/img/vendor_img/cisco/asa-trace2.PNG)
 
Note: On ASA 9.10+, the any keyword only captures packets with ipv4 addresses. The any6 keyword captures all ipv6 addressed traffic.

These are advanced settings that can be configured with Packet Captures.

Please review the command reference guide on how to set them.

* ikev1/ikev2 - Captures only Internet Key Exchange Version 1 (IKEv1) or IKEv2 protocol information.

* isakmp - Captures Internet Security Association and Key Management Protocol (ISAKMP) traffic for VPN connections. The ISAKMP subsystem does not have access to the upper-layer protocols. The capture is a pseudo capture, with the physical, IP, and UDP layers combined together in order to satisfy a PCAP parser. The peer addresses are obtained from the SA exchange and are stored in the IP layer.

* lacp - Captures Link Aggregation Control Protocol (LACP) traffic. If configured, the interface name is the physical interface name. This is useful when you work with Etherchannels in order to identify the present behavior of LACP.

* tls-proxy - Captures decrypted inbound and outbound data from the Transport Layer Security (TLS) proxy on one or more interfaces.

* webvpn - Captures WebVPN data for a specific WebVPN connection.

Caution: When you enable WebVPN capture, it affects the performance of the security appliance. Ensure that you disable the capture after you generate the capture files that are needed in order to troubleshoot.

### Defaults

These are the ASA system default values:

* The default type is raw-data.

* The default buffer size is 512 KB.

* The default Ethernet type is IP packets.

* The default packet-length is 1,518 bytes.

### View the Captured Packets

#### On the ASA

In order to view the captured packets, enter the show capture command followed by the capture name. This section provides the show command outputs of the capture buffer contents. The show capture capin command shows the contents of the capture buffer named capin:

![Branching](https://gt-legend.github.io/assets/img/vendor_img/cisco/asa-view-capin.PNG)

The show capture capout command shows the contents of the capture buffer named capout:

![Branching](https://gt-legend.github.io/assets/img/vendor_img/cisco/asa-view-capout.PNG)

### Download from the ASA for Offline Analysis

There are a couple of ways to download the packet captures for analysis offline:

*  Navigate to https://<ip_of_asa>/admin/capture/<capture_name>/pcap on any browser.

Tip: If you leave out the pcap keyword, then only the equivalent of the show capture <cap_name> command output is provided.

* Enter the copy capture command and your preferred file transfer protocol in order to download the capture:

```
copy /pcap capture:<capture-name> tftp://<server-ip-address>
```

Tip: When you troubleshoot an issue with the use of packet captures, Cisco recommends that you download the captures for offline analysis.

### Clear a Capture

In order to clear the capture buffer, enter the clear capture <capture-name> command:

![Branching](https://gt-legend.github.io/assets/img/vendor_img/cisco/asa_clear-cap.PNG)

Enter the clear capture /all command in order to clear the buffer for all captures:

```
clear capture /all
```

### Stop a Capture

The only way to stop a capture on the ASA is to disable it completely with this command:

```
no capture <capture-name>
```



[Back](/vendors/cisco.html)
