# Networking

## IP Addresses (Layer 3)
- The command 'ifconfig' can be used in the linux terminal to look for the IP address of the device.
  - 'inet' is the IP address and inet6 is the IPv6
Private IP address (An IP address that is only known by you):
- 192.168.x.x
- 10.0.0.0

## Mac Address (Media Access Control) (Layer2)
- A Mac address routes data packets between devices on the same local area network (LAN), Wi-Fi, or Bluetooth segment. While an IP address finds a device across the global internet (Layer 3), a MAC address makes sure the data reaches the exact physical machine on the local network (Layer 2)
- In the ifconfig it is the ether (e.g: 00:0c:29:0a:42:05)
- MAC addresses have identifiers. Take the first three pairs and look it up on google to identify what the device is. (e.g: 00:0c:29) 

## TCP (Transmission Control Protocol) vs UDP (User Datagram Protocol) ( (Layer4)
- TCP Connection oriented protocol
  - A website, SSH, FTP (File transfer Protocol)
- UDP Connectionless protocol
  - Streaming, Video calls, DNS

 ### Three way handshake
 - TCP is the one you will mostly be scanning using a protocol called the three-way-handshake:
   - SYN > SYN ACK > ACK
     - SYN: The client wants to start a connection, so it sends a TCP segment with the SYN (Synchronize Sequence Number) flag set to 1.
     - SYN ACK: The server receives the client's request and responds with a segment that has both the SYN and ACK (Acknowledgment) flags set to 1
     - ACK: The client receives the server's SYN-ACK and replies with an ACK packet (with the ACK flag set to 1)

## Common Ports and Protocols
### TCP
- FTP (21) (File Transfer Protocol)
- SSH (22) Similar to Telnet but this one is encrypted
- Telnet (23) The ability to login to a machine remotely
- SMTP (25)
- DNS (53) (Domain Name System is A way to resolve IP addresses to names. Instead of typing IP addresses on the web we type the domain name)
- HTTP (80)/HTTPS (443)
- POP3 (110)
- SMB (139+445) (Relates to file shares, it is a very common port) 
- IMAP (143)

### UDP 
- DNS (53)
- DHCP (67,68)
- TFTP (69)
- SNMP (161)

## The OSI Model
- 1: Physical Layer - Data cables, cat6 (Anything you have to plug in)
- 2: Data link Layer - Switching, MAC Addresses
- 3: Network Layer _ IP Addresses, routing
- 4: Transport Layer - TCP/UDP
- 5 Session Layer - session management
- 6 Presentation Layer - WMV, JPEG, MOV
- 7: Application Layer - HTTP, SMTP


## Subnetting 
- Subnetting is the practice of dividing a large IP network into smaller, more manageable sub-networks (subnets) to improve performance, boost security, and conserve IP addresses
