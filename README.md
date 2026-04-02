# Traceroute, DNS steering, TTL 


## Objective 
The objective of this lab is to demonstrate my ability to analyze network paths, DNS behavior, and packet lifecycles using tools like dig, traceroute, and Wireshark. I walk through how DNS steering affects IP resolution, how traceroute uses probe packets to map network hops, and how TTL expiration generates ICMP Time Exceeded messages. This lab highlights my understanding of routing behavior, load balancing, and packet inspection at a protocol level.

##Tools Used
Wireshark
Linux VM 
Putty

### LAB SUMMARY
1. DNS Resolver Change & Multiple A Records
When the DNS resolver was changed, the dig output returned a different set of IP addresses.

Why this happens:
Different resolvers may use different DNS caches or geographic routing policies.
Google returns multiple A records because it uses load balancing and geo‑based routing, directing users to the closest or least‑loaded server.

“Changing the DNS resolver returned different sets of IP addresses. Google provides multiple A records because it uses load balancing and geo‑based routing.”

2. Traceroute Probe Type Evidence
Wireshark captured the traceroute packets as UDP probes.

How we know:

The protocol column shows UDP.
The filter ip.dst == 104.18.4.215 && udp confirms the probe traffic.
Traceroute commonly uses UDP packets with high destination ports to trigger ICMP responses.

“The packets are identified as UDP in the protocol column and the filter confirms the traceroute probes.”

3. TTL Proof with ICMP Time Exceeded
Traceroute works by sending packets with increasing TTL values. Each router that decrements the TTL to zero sends back an ICMP Time Exceeded message.

What this proves:

TTL controls how far a packet can travel.
Each hop reveals itself when TTL expires.
This is how traceroute maps the full path to a destination.

“ICMP Time Exceeded indicates that a packet’s TTL expired before reaching the destination.”

4. ASN Context & Neighboring Networks
Using Hurricane Electric (HE) tools, the ASN lookup shows:

The Autonomous System responsible for the IP address
Its upstream and downstream neighbors
The broader routing context of the destination network

This demonstrates how traceroute and ASN lookups together reveal both the path and the ownership of each hop.
