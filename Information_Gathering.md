# Information Gathering

## Passive Recon
### Physical/Social 
- There is the physical/social side. Physical is actually going on site and doing a physical engagement. Social engineering includes phishing or any physical way.

#### Location Information
- Satellite images
- Drone recon (To check how the physical area looks)
- Building layout (badge, readers, break areas, security, fencing)

#### Job Information
- Employees (name, job, title, phone number, manager, etc.)
- Pictures (badge photos, desk photos, computer photos, etc)

### Web/Host
- Target Validation. Validating the target
  - WHOIS, nslookup, dnsrecon
- Finding Subdomains
  - Google Fu, dig, Nmap, Sublist3r, Bluto, crt.sh, etc.
- Fingerprinting
  - Nmap, Wappalyzer, WhatWeb, Builtwith, Netcat
- Data breaches
  - HavelBeenPwned, Breach-Parse, WeLeakinto

## Identifying our target 
https://bugcrowd.com/engagements/tesla

## Discovering email addresses
- You can use the following website to find someones email or a company's email:
  - https://hunter.io/
  - https://phonebook.cz/
  - https://intelx.io/
 
## Gathering breached credentials
- https://github.com/hmaverickadams/breach-parse

## Hunting breached credentials with DeHashed
- Try looking up a website that displays any historically breached data
- If you find a website you can search the name or company name or even a domain to find a pattern.
  - e.g: "@company.com"
