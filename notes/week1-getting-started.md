# Week 1: First Steps into Ethical Hacking

---

## What We Covered

This week was about building the foundation for everything that comes next.
Before touching a single security tool, we built a complete isolated home lab
environment from scratch : installing VirtualBox, setting up Kali Linux as our
attacker machine, and deploying Metasploitable 2 as our target. We configured
an isolated NAT network called HackLab so both machines could communicate
privately without touching my real home network or the internet.

Once the lab was live we jumped straight into our first real engagement ,
scanning, enumerating, exploiting, and documenting a vulnerable machine from
start to finish.

---

## Tools I Used

| Tool | Purpose |
|------|---------|
| VirtualBox | Virtualization — running multiple OS environments on one laptop |
| Kali Linux | Attacker machine — industry standard penetration testing OS |
| Metasploitable 2 | Target machine — intentionally vulnerable for safe practice |
| nmap | Network scanner — identified open ports and running services |
| Metasploit Framework | Exploitation framework — searched and launched exploits |
| Meterpreter | Post-exploitation shell — interacted with the compromised machine |

---

## Key Concepts I Learned

**Ports and Attack Surface**
The biggest early revelation was looking at a list of open ports on a machine
and recognizing that each one is a potential entry point. As someone new to
this, seeing that list come back from nmap and realizing those open ports
represented real vulnerabilities was a genuine turning point in how I think
about systems.

**Reconnaissance Before Exploitation**
I learned that real penetration testers never jump straight to attacking. Every
action is methodical , gather information first, understand what you're looking
at, then move forward. Rushing gets you caught or causes you to miss critical
findings.

**The /etc/passwd and /etc/shadow Files**
Linux stores user account information in `/etc/passwd` and password hashes in
`/etc/shadow`. I learned that passwords are never stored in plain text , they
are run through a hashing algorithm. The `$1$` identifier revealed that
Metasploitable was using MD5, a dangerously outdated algorithm that modern
hardware can crack at billions of attempts per second.

**Principle of Least Privilege**
The Java RMI service we exploited was running as root , meaning the moment we
compromised it we inherited full system access. This taught me that services
should only ever have the minimum permissions they need to function. Nothing
more.

**MITRE ATT&CK Framework**
I was introduced to the industry standard framework used by professional red
teams and threat intelligence analysts to categorize attacker techniques. Every
action I took in this lab maps to a real technique in this framework.

---

## How My Thinking Changed

Before this week I had never used a Linux terminal in a security context or
heard of Metasploit. By the end of the week I had used both to successfully
compromise a machine, read its password hashes, and document the findings in a
professional report.

The thing that changed most wasn't the technical knowledge , it was the
mindset. I started seeing systems differently. Every open port is a question.
Every running service has a history. Every misconfiguration is a story about
what someone didn't think about when they built or maintained that system.

The moment that crystallized everything was getting that Meterpreter shell back
and running `getuid` to see `root`. It felt like completing something I had
always dreamed of doing. And the fact that I understood exactly how I got there
, every step, every command, every decision , made it mean something.

---

## Hardest Part

The hardest part right now is retaining terminology and Linux commands. There
is a lot of new vocabulary in this field and it does not always stick
immediately. But I know from experience that repeated exposure and hands on
practice is how it becomes second nature. Every lab we run reinforces it a
little more.

---

## What I Want to Explore Next

I am most curious about password cracking : specifically how hashing tools like
John the Ripper and Hashcat work. Seeing those MD5 hashes in `/etc/shadow` this
week and knowing they are crackable made me want to understand that process
deeply. Password cracking has always been one of those things that seemed almost
mythical from movies and TV. Now that I understand the mechanics behind hashing
I want to see how those tools actually break them.

That lines up perfectly with Week 9 of our roadmap : Password Attacks and
Privilege Escalation , and I am genuinely looking forward to it.

---

## Security+ Concepts Encountered This Week

- Attack Surface Reduction
- Patch Management
- Vulnerability Management
- Principle of Least Privilege
- Key Stretching
- Cryptographic Hashing Algorithms
- CIA Triad
- Default Configuration Vulnerabilities

---

*Week 1 of the 12-week cybersecurity and ethical hacking journey.*
*Lab report: see labs/lab01-java-rmi-exploitation.md*