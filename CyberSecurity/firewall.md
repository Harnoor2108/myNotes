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

  
