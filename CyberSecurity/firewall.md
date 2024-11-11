## Packet 
- Header - what kind of packet it is 
- Data - Actual Information
- Footer - Error detection checks and stuff

## Three way handshaking

SYN - SYN-ACK - ACK
- DDOS attack 


 ### 1. Summarise different kinds of firewalls open or closed from the doc.

- Application-Layer Firewalls and Circuit-Level Gateways - Both of these works between the client and the webserver and can be used as a proxy to communicate with the web server. Application Layer firewalls works on the application layer and filters the application specific commands and act as a web server proxies. Circuit level Gateways works on the session layer of the OSI model and monitor the TCP Packets.

- Web Application firewall - It protects the website from attacks on the network like SQL injections, cross site scripting, parameter tampering,  cross-site forgery, cross-site-scripting (XSS) and file tampering. It filters and monitors the HTTP traffic to protect from attack. It is based on the OSI model.

- Next-generation firewall (NGFW) - It is a general term that refers to a stateful packet inspection firewall that includes integrated intrusion detection systems, application gateway features, and deep packet inspection.

- Blacklisting - Blacklisting involves restricting a user from visiting the blocked or restricted sites.

- Whitelisting - Whitelisting involves only allowing the user to visit specific sites.
  
### 2. What is SNORT. Summarise in 3-5 lines.

Snort is an open source Intrusion Detection system. It is a command line based IDS. It can be used on windows or linux. Some common snort commands are snort -v, which Start Snort as just a packet sniffer, snort -vd, which Start Snort as a packet sniffer but have it sniff packet data rather than just the headers and snort -dev -l ./log which start snort in a logging mode so it logs packets. snort -dev -l ./log -h
192.168.1.1/24 -c snort.conf can start snort in an IDE mode.

### 3. What are the types of wifi security discussed in firewall.docx. Give brief description of each.

- Wired Equivalent Privacy (WEP): Uses RC4 stream cipher and a CRC-32 checksum for error checking, with key lengths of 40-bit or 104-bit plus a 24-bit initialization vector. WEP is insecure due to reused IVs, making it susceptible to attacks.

- Wi-Fi Protected Access (WPA): Improves on WEP by using AES encryption and the Temporal Key Integrity Protocol (TKIP), which generates a new key for each packet, making it more secure.

- WPA2: Based on the IEEE 802.11i standard, WPA2 uses AES encryption with CCMP (Counter Mode-Cipher Block Chaining Message Authentication Code Protocol), ensuring strong data confidentiality, integrity, and origin authentication.

- WPA3: Released in 2018, WPA3 encrypts all traffic to and from the wireless access point and resists brute-force attacks by requiring interaction with the Wi-Fi for each password guess attempt, enhancing security.

### 4. What is the difference between cloud firewall and next-generation firewall?

- Cloud Firewall: A cloud firewall is deployed within the cloud to protect cloud-based assets and manage incoming and outgoing traffic between cloud environments. It provides security for resources hosted on cloud infrastructure and is typically managed by the cloud provider, offering scalable and flexible protection for virtual networks.

- Next-Generation Firewall (NGFW): An NGFW is deployed on-premises or within data centers and combines traditional firewall functions with advanced features like deep packet inspection, intrusion prevention, and application-layer filtering. NGFWs are designed to analyze traffic at multiple layers, providing more robust protection for physical networks and hybrid infrastructures.

  
