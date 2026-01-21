---
layout: default
---

# Domain Name System (DNS)

***

The Domain Name System (DNS) is a hierarchical and distributed naming system that translates human-readable domain names into IP addresses, enabling users to access websites easily.

- [How Does DNS Work](#how-does-dns-work)
- [DNS Architecture](#dns-architecture)
- [Types of Domains](#types-of-domains)
- [Types of DNS Queries](#types-of-dns-queries)
- [DNS Caching and TTL](#dns-caching-and-ttl)
- [DNS Security and DNSSEC](#dns-security-and-dnssec)
- [Reverse DNS Lookup](#reverse-dns-lookup)
- [DNS Record Types](#dns-record-types)

## How Does DNS Work

The DNS process can be broken down into several steps, ensuring that users can access websites by simply typing a domain name into their browser.

1. User Input: You enter a website address (for example, tyler-nse.github.io) into your web browser.

2. Local Cache Check: Your browser first checks its local cache to see if it has recently looked up the domain. If it finds the corresponding IP address, it uses that directly without querying external servers.

3. DNS Resolver Query: If the IP address isn’t in the local cache, your computer sends a request to a DNS resolver. The resolver is typically provided by your Internet Service Provider (ISP) or your network settings.

4. Root DNS Server: The resolver sends the request to a root DNS server. The root server doesn’t know the exact IP address for tyler-nse.github.io but knows which Top-Level Domain (TLD) server to query based on the domain’s extension (e.g., .io).

5. TLD Server: The TLD server for .io directs the resolver to the authoritative DNS server for github.io.

6. Authoritative DNS Server: This server holds the actual DNS records for github.io, including the IP address of the website’s server. It sends this IP address back to the resolver.

7. Final Response: The DNS resolver sends the IP address to your computer, allowing it to connect to the website’s server and load the page.

## DNS Architecture

DNS operates through a hierarchical structure, ensuring scalability and reliability across the global internet infrastructure. Here's how it’s organized:

*   Root DNS Servers: These are the highest-level DNS servers and know where to find the TLD servers. They are crucial for directing DNS queries to the correct locations.

*   TLD Servers: These servers manage domain extensions like .com, .org, .net, .edu, .gov and others. They help route queries to the authoritative DNS servers for specific domains.

*   Authoritative DNS Servers: These are the servers that store the actual DNS records for domain names. They are responsible for providing the correct IP addresses that allow users to reach websites.

## Types of Domains

DNS helps manage a wide variety of domain types to organize the vast number of websites on the internet. Here are the primary categories:

*   Generic Domains: These include top-level domains like .com, .org, .net and .edu. These are widely used and recognized across the world.

*   Country Code Domains: These domains represent specific countries or regions, such as .in for India, .us for the United States, .uk for the United Kingdom and .jp for Japan.

*   Inverse Domains: Used for reverse DNS lookups, these domains help map IP addresses back to domain names. Reverse DNS lookups are useful for diagnostics and security purposes, ensuring that the source of network traffic is legitimate. 

## Types of DNS Queries

There are basically three types of DNS Queries that occur in DNS Lookup. These are stated below.

*   Recursive Query: In this query, if the resolver is unable to find the record, in that case, DNS client wants the DNS Server will respond to the client in any way like with the requested source record or an error message.

*   Iterative Query: Iterative Query is the query in which DNS Client wants the best answer possible from the DNS Server.

*   Non-Recursive Query: Non-Recursive Query is the query that occurs when a DNS Resolver queries a DNS Server for some record that has access to it because of the record that exists in its cache.

## DNS Caching and TTL

*  DNS caching is a mechanism that stores DNS records locally to avoid querying external DNS servers repeatedly for the same information. This speeds up the browsing experience and reduces network traffic.

*  TTL (Time-to-Live) is the amount of time that a DNS record is cached before it expires. When the TTL expires, the cache is cleared and a fresh DNS query must be made. The TTL is defined by the authoritative DNS server, which can adjust this based on the nature of the domain.

## DNS Security and DNSSEC

Although DNS is essential for smooth internet navigation, it can be vulnerable to security threats. One common risk is DNS cache poisoning, where malicious actors inject harmful DNS records into caches, redirecting users to fraudulent websites.

### DNS Security Extensions (DNSSEC)

*  It is a protocol designed to address these security concerns.

*  It adds cryptographic signatures to DNS records, allowing resolvers to verify the authenticity and integrity of DNS responses.
DNSSEC ensures that the information a user receives from a DNS query has not been tampered with.

## Reverse DNS Lookup

Reverse DNS Lookup is the process of mapping an IP address back to its corresponding domain name. This is the opposite of the typical DNS lookup, where a domain name is resolved to an IP address. Reverse DNS is commonly used for:

*  Network Diagnostics: System administrators use reverse DNS to determine the domain name associated with a specific IP address. This helps identify the source of network traffic.

*  Email Security: Many email servers perform reverse DNS lookups to verify that incoming emails are coming from legitimate sources. This helps prevent spam and fraud.

## DNS Record Types

DNS records are essential for defining how domain names are used and how services are configured. Here are some of the most commonly used DNS record types:

*  A Record: This record maps a domain name to an IPv4 address (e.g., geeksforgeeks.org to 185.199.109.153). This is the most common DNS record used to point a domain to its website's IP address.

*  CNAME Record: The Canonical Name (CNAME) record allows you to alias one domain name to another. For example, www.geeksforgeeks.org can be an alias for geeksforgeeks.org.

*  MX Record: The Mail Exchange (MX) record defines which mail servers are responsible for receiving emails for a domain. This is crucial for setting up email services.

*  TXT Record: The Text (TXT) record stores text-based information. It is commonly used to verify domain ownership and to implement email security protocols like SPF (Sender Policy Framework) and DKIM (DomainKeys Identified Mail).


[back](/fundamentals/networks_and_security.html)