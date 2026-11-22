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

## Enumerating HTTP and HTTPS Part 2
- We will be using dirbuster to find hidden directories
  - Run the command: "dirbuster&"
  - This will open a dirbuster UI. You will have to manually navigate to the dirbuster wordlist and click next to start scanning 
  - Run 192.168.19.129:80/ in the folder: /usr/wordlists/dirbuster/directory-list-2.3-small.txt
- Burp suite can also be used to intercept and enumerate the HTTP. Burp suite could possibly expose information about the server in the header so keep note of that.
  - In this example the header exposed the version information of the server which is a vulnerability on its own. E.g: Server: Apache/1.3.20 (Unix) (Red-Hat/Linux) nod_ssl/2.8.4 OpenSSL/0.9.6b
- When the dirbuster scanner is finished your goal should be to dig through all the results and enumerate, find hints, any server info that can be useful, etc.
- When you see a website you are looking for service version information, any backend directories, potential vuln scanning, and any sort of information you can use.

### Gobuster
- This is another method that can be used to look for directories.
- -u is the target URL or Domain
- -v is the verbose output
- -w is a path t the wordlist
- -x refers to file extension to search for (dir mode only)
- e.g: gobuster dir -u http://192.168.0.103:80 -w /usr/share/wordlists/dirb/big.txt

## Enumerating SMB (Port 139)
- SMB is a file share. Think about your work environment, if you go to work and you have a drive that yiou can access, this drive can be accessed to upload and download files, and your co-workers can also see that file share. That's why it is called a file share.
- SMB is commonly used in work environments.\
- You need to know the SMB version running because the type of version running could potentially lead to an exploit. So the goal right now is to look for the version information, see if there is any connections available to us, and if we get to the file we can check if there is anything malicious.
- In the terminal we are gonna use the tool metasploit.
  - Metasploit is an exploitation framework
  - In the terminal type the command: msfconsole
  - After the command is done, type 'search SMB'
  - This command will be used to see if there are any modules for SMB enumeration.
    - you might see something like: auxiliary/scanner/smb/psexec
    - Auxiliary - this is an auxiliary module
    - scanner - this is the action
  - Use one of the modules by typing 'use auxiliary/scanner/smb/psexec'
  - Type info to get info on how to use the module
  - In this case it is showing RHOSTS which stands for remote hosts. RHOSTS is who we are attacking. We are gonna use RHOSTS by typing the following commands in order:
    - set RHOSTS 192.168.57.139
    - run
    - This will show the version of the SMB. This will make it easier to do research on exploitation against this version.

- Now we are going to use a new tool called smbclient
  - This tool is going to attempt to connect to the file share that is out there. We could potentially see files that are valuable to us. This could include exposed passwords, backup files, private files.
  - Use the following command:
    - smbclient -L \\\\192.168.57.134\\
    - This will display the file shares.
      - After accessing this file share we can accessing one of the files by adding the sharename on the command:
      - smbclient \\\\192.168.57.134\\ADMIN$ (This method might not work, try a different sharename)

## Enumerating SSH (Port 22)
- We will attempt to connect to SSH using this specific port\
- Try the command: ssh 192.168.57.134
- There isnt much to enumerate in SSH, we mostly exploit this.

## Researching potential vulnerabilities
- So far from the enumeration we have found the following information about the target:
  - Port 80/443 - 192.168.57.134
  - Default webpage - Apache - PHP
  - Information Disclosure - 404 page
  - Information Disclosure - server headers disclose version information
  - 80/tcp open http Apache httpd 1.3.20 (Unix) (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b)
  - SMB Unix (Samba 2.2.1a)
  - Webalizer Version 2.01 - http://192.168.57.134/usage_201911.html
  - SSH OpenSSH 2.9p2
- When attacking we will attack in the order: 80, 443, 139, 445
- Go to google and search mod_ssl2.8.4 exploit
- You can also look up apache httpd 1.3..20 exploit
- You can also look up Samba 2.2.1a exploit
- If you are doing this without any internet you can do it on the linux terminal
- Use the tool called searchsploit:
  - E.g: searchsploit Samba 2.2.1a
  - The previous one might not work because you cannot be too specific when using searchsploit. So try this one: 
  - searchsploit Samba 2
  - You can also say searchsploit mod ssl 2
