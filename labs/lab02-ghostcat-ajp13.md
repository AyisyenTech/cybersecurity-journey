# Week 2: AJP13, Ghostcat, and Chaining Vulnerabilities

---

## What We Covered

Week 2 built directly on the foundation from Week 1. Rather than starting 
fresh, we picked up where we left off : returning to our Metasploitable 2 
target with a new port to investigate.

For homework I ran an independent nmap scan against the target and identified 
port 8009 running a service called AJP13 : Apache JServ Protocol. I chose it 
because it seemed connected to something bigger and I wanted to understand what 
it was. That instinct turned out to be correct.

This week we explored CVE-2020-1938 — nicknamed Ghostcat — a critical 
vulnerability in Apache Tomcat's AJP connector that allows unauthenticated 
file reads from the server. We also deepened our use of the Java RMI exploit 
from Week 1, this time using it not just to gain access but as a supporting 
tool to locate files that Ghostcat couldn't reach on its own.

The biggest milestone this week was successfully chaining two separate 
vulnerabilities together to achieve a goal neither could accomplish alone.

---

## Attack Chain

| Step | Action | Tool Used |
|------|--------|-----------|
| 1 | Identified port 8009 running AJP13 via homework nmap scan | `nmap -sV` |
| 2 | Researched Ghostcat vulnerability | Metasploit `search ghostcat` |
| 3 | Loaded Ghostcat module and read web.xml successfully | `auxiliary/admin/http/tomcat_ghostcat` |
| 4 | Attempted to read tomcat-users.xml, file not found at standard path | Ghostcat module |
| 5 | Switched to Java RMI exploit to gain root shell | `exploit/multi/misc/java_rmi_server` |
| 6 | Used Linux find command to locate exact file path | `find / -name "tomcat-users.xml"` |
| 7 | Discovered file at /etc/tomcat5.5/tomcat-users.xml | Shell command |
| 8 | Read tomcat-users.xml directly through root shell | `cat /etc/tomcat5.5/tomcat-users.xml` |
| 9 | Retrieved plain text credentials for all Tomcat accounts | Shell output |

---

## MITRE ATT&CK Mapping

| Tactic | Technique ID | Technique Name |
|--------|-------------|----------------|
| Reconnaissance | TA0043 | Reconnaissance |
| Initial Access | T1190 | Exploit Public Facing Application |
| Discovery | T1046 | Network Service Scanning |
| Discovery | T1083 | File and Directory Discovery |
| Credential Access | T1552 | Unsecured Credentials |
| Execution | T1059 | Command and Scripting Interpreter |

---

## Key Concepts I Learned

**AJP13 and Apache Tomcat Architecture**
Port 8009 runs the Apache JServ Protocol, an internal communication channel
between the Apache web server and Apache Tomcat, which handles Java based web
applications. Think of Apache as the front of house taking orders and Tomcat
as the kitchen preparing them. AJP13 is the ticket system passing requests
between them. When this port is exposed publicly rather than kept internal,
it becomes a serious attack surface.

**CVE-2020-1938 : Ghostcat**
Ghostcat is a critical vulnerability discovered in 2020 that existed silently
in Apache Tomcat for over thirteen years before anyone noticed. It allows an
unauthenticated attacker to read any file within the Tomcat web application
directory by sending specially crafted AJP requests directly to port 8009.
No login required. No credentials needed.

**Vulnerability Chaining**
The most important technical lesson this week was learning to chain two
vulnerabilities together. When Ghostcat couldn't reach files outside the web
application directory, we didn't give up. We used the Java RMI exploit from
Week 1 to gain a root shell, located the exact file path using the Linux find
command, and then read the file directly. One vulnerability supported another.
This is a core technique in real penetration testing.

**Default and Weak Credentials**
Inside tomcat-users.xml we found three user accounts all sharing the same
password: tomcat. The administrator account used tomcat as both its username
and password. These were factory default credentials that were never changed.
This is one of the most common critical findings in real penetration tests and
one of the easiest things to fix.

**Linux File System Navigation**
This week I expanded my Linux command knowledge with two new commands:
- `find / -name "filename" 2>/dev/null` — searches the entire filesystem for
  a file by name
- `cat [filepath]` — reads and displays the contents of any file

---

## Tools I Used

| Tool | Purpose |
|------|---------|
| nmap | Independent homework scan: identified port 8009 |
| Metasploit Framework | Searched, loaded, and configured exploit modules |
| Ghostcat module | Read web.xml from Tomcat web application directory |
| Java RMI exploit | Gained root shell to support Ghostcat investigation |
| Meterpreter | Post-exploitation shell for interacting with target |
| Linux shell commands | Located and read tomcat-users.xml directly |

---

## How My Thinking Changed

Before this week I assumed hacking looked like the movies: one dramatic
command, instant access, and some flashy visual confirmation that you were in.
The reality is completely different. It's methodical, it's iterative, and a
lot of it looks like plain text on a black screen that you have to learn to
read and interpret.

When Ghostcat hit a wall and couldn't find the file we were after, the old
version of me might have assumed it failed and stopped there. Instead I learned
to pivot, use a different tool, approach the problem from another angle, and
keep moving toward the goal. That shift in thinking from "this didn't work"
to "what else can I try" is what separates a real penetration tester from
someone just running tools blindly.

The feeling when we finally read those plain text credentials was exactly what
I imagined it would feel exciting and rewarding. But now I understand
that every step leading up to that moment is what made it possible. The
reconnaissance, the enumeration, the troubleshooting, the pivoting. None of
it is glamorous but all of it matters.

---

## What I Want to Explore Next

I am curious about more aggressive techniques. Things like brute force attacks
and understanding how tools automate the process of trying thousands of
credentials automatically. Finding plain text passwords this week felt almost
too easy. I want to understand what happens when credentials are properly
protected and how attackers get around that.

I also want to continue following the roadmap as planned. Week 3 covers Linux
fundamentals and deeper command line proficiency, which after this week I
understand is not optional. The more comfortable I am in a Linux shell the
more effective everything else becomes.

---

## Defensive Recommendations

**1. Never Expose AJP Port 8009 Publicly**
The AJP connector is designed for internal communication between Apache and
Tomcat only. It should never be accessible from outside the server itself.
Firewall rules should block port 8009 from any external access entirely.

*Security+ Concept: Attack Surface Reduction*

---

**2. Change All Default Credentials Immediately**
Every account on this Tomcat installation used the default password tomcat,
including the administrator account which used tomcat as both username and
password. Default credentials should be changed before any service is deployed
and a strong password policy should be enforced across all accounts.

*Security+ Concept: Weak Password Policy · Security Program Management*

---

**3. Implement a Strong Password Policy**
All three accounts shared the same password. A proper password policy would
require unique, complex passwords for every account, enforce minimum length
and complexity requirements, and prevent passwords from matching usernames.

*Security+ Concept: Password Policy · Security Program Management*

---

**4. Upgrade or Decommission Legacy Software**
Apache Tomcat 5.5 is severely outdated and no longer receives security patches.
CVE-2020-1938 affected all versions prior to 9.0.31, 8.5.51, and 7.0.100.
Any production system running Tomcat should be upgraded to a current supported
version immediately.

*Security+ Concept: Patch Management*

---

**5. Apply Principle of Least Privilege to Service Accounts**
The tomcat account held both admin and manager roles simultaneously. Service
accounts should only hold the minimum roles required for their function.
Separating administrative and operational roles limits the damage an attacker
can do with a single set of compromised credentials.

*Security+ Concept: Principle of Least Privilege*

---

## Overall Risk Rating: Critical

An unauthenticated attacker with network access to port 8009 was able to read
sensitive server files via the Ghostcat vulnerability. By chaining this with
a separate Java RMI vulnerability, plain text administrative credentials were
recovered without any password cracking required. These credentials provide
full administrative access to the Tomcat management interface and could be
used to deploy malicious applications directly to the server.

---

## Lab Environment

| Component | Details |
|-----------|---------|
| Host Machine | Windows Laptop |
| Virtualization | Oracle VirtualBox |
| Attacker OS | Kali Linux 2026.1 |
| Target OS | Metasploitable 2 — Linux 2.6.24 |
| Network | Isolated NAT Network — HackLab 10.0.2.0/24 |
| CVE Referenced | CVE-2020-1938 — Apache Tomcat Ghostcat |

---

*Week 2 of the 12-week cybersecurity and ethical hacking journey.*
*Previous lab: see labs/lab01-java-rmi-exploitation.md*