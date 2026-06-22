# Command Reference Sheet

Personal cheat sheet built throughout the 12-week cybersecurity journey.
Updated weekly as new tools and commands are introduced.

---

## Metasploit Framework

| Command | What it does |
|---------|-------------|
| `msfconsole` | Opens Metasploit |
| `search [name]` | Searches for modules by keyword |
| `use [module name]` | Loads a specific module |
| `show options` | Displays current module settings |
| `set [FIELD] [value]` | Configures a specific setting |
| `run` | Executes the loaded module |
| `sessions -i [number]` | Connects to an open session |
| `shell` | Drops into raw Linux shell from Meterpreter |
| `getuid` | Shows what user you are on the target |
| `sysinfo` | Shows system information from target |
| `exit` | Exits current module or closes Metasploit |

---

## Nmap

| Command | What it does |
|---------|-------------|
| `nmap [IP]` | Basic port scan of target |
| `nmap -sV [IP]` | Scan for open ports and service versions |

---

## Linux Commands

| Command | What it does |
|---------|-------------|
| `ping [IP]` | Tests if a target machine is reachable |
| `ifconfig` | Shows network interface information and IP address |
| `cat [filepath]` | Reads and displays contents of a file |
| `find / -name "filename" 2>/dev/null` | Searches entire filesystem for a file by name |
| `ls` | Lists files in current directory |
| `cd [folder]` | Navigates into a folder |
| `pwd` | Shows your current location in the filesystem |
| `Ctrl + C` | Stops a running command |

---

## Git Commands

| Command | What it does |
|---------|-------------|
| `git add [filename]` | Stages a file for commit |
| `git add .` | Stages all changed files |
| `git commit -m "message"` | Commits staged files with a description |
| `git push` | Pushes commits to GitHub |
| `git status` | Shows what files have changed locally |
| `cd /c/Users/[username]/Documents/cybersecurity/cybersecurity-journey` | Navigates to your repository |

---

## Key IP Addresses

| Machine | IP Address |
|---------|-----------|
| Kali Linux (attacker) | 10.0.2.15 |
| Metasploitable 2 (target) | 10.0.2.3 |

---

## Metasploit Workflow (Every Time)

1. msfconsole
2. search [service or CVE name]
3. use [module name or number]
4. show options
5. set RHOSTS [target IP]
6. set [any other missing fields]
7. run

---

*Updated: Week 2*
*Part of the cybersecurity-journey repository*