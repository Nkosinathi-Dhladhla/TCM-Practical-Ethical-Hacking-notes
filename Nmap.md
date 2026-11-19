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

## Enumerating HTTP and HTTPS Part 1
- After scanning you need to think about the point of attack as an attacker
- When the scan is done you should pay attention to the port 80, 443, 139, and 445. Those ports are important because most of the time they are commonly found with exploits.
- Port 22 (SSH) is not commonly attacked but it can be
- We will start by investigating Port 443.

### Port 80/443
- First step, copy the IP address for the attacked machine and look it up on the web.
- Check the http and https of the website
- This IP address will lead us to the website's default page. We can tell that the website is running using Apache, we know that irt is running redhat linux,
- If the client is running a default web page, it brings up two questions. Firstly, are there any other web directories running on the behind page, are they hosting another website on another IP address, or maybe they are not hosting a website and they just left 443 on and running, what potential vulnerabilities can the client have since 443 is open.
- You can use the command 'nikto' to do a vulnerability scan. E.g: nikto -h 192.168.x.x
- Through the vulnerability scan we found that the mod_ssl is vulnerable
- make sure you copy the result of the vulnerability scan, create a note from your linux terminal and paste the vuln result on your linux notepad that was created. This notepad can be created through the following way:
  - mkdir foldername
  - cd foldername/
  - gedit nikto.txt
