# Nmap 
## Scanning with Nmap 
- We are attacking Kioptrix vulneribile machine from vulnhub.
- We will start by trying to find the Kioptrix IP address by scanning it from the kali linux virtual machine using the following command in root access:
  - ifconfig (to check our original kali IP address)
  - then netdiscover -r 192.168.x.0/24
  - The discovered IP address is 192.168.19.129
- Nmap will be used to scan open ports and services. The process that will be used is stealth scan
  - nmap -T4 -p- -A
    - T4 is a speed that can be chosen between 1-5. In this example we are using 4
    - -p- means you want to scan all ports. You could say -p or leave -p completely. If you leave -p out completely it will only scan the important ports.
    - -A stands for everything. This means this will tell you everything including version information, operating system information, etc.
    - This is how the address is used: nmap -T4 -p- -A 192.168.19.129
    - If you want to know more about nmap use the command nmap --help
  - MAKE SURE YOU USE Nmap --help!!!!
  - Most of the time you are gonna be using the -sS (TCP scan) and the -sU (UDP scan)
    - to use -sU you can use the command 'nmap -sU -T4 -p 192.168.19.129. -A was removed because UDP takes a long time to scan so it is more efficient to use it without -A.
    - it is always much faster to remove the dash A
  - The open port (-p) can be defined/specified. This will directly scan the port that has been defined.
- When the Nmap is done scanning you should start investigating. The first thing you should investigate is the open port and the service that is running on that open port. 
