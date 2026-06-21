# Week 2: AJP13, Ghostcat, and Chaining Vulnerabilities

---

## Overview

Week 2 went deeper than Week 1 in every way. Not just technically but mentally.
This week taught me that penetration testing is not a straight line. It is a
series of decisions, pivots, and adjustments made in real time based on what
the target gives you back.

The homework from Week 1 set the tone. I independently ran an nmap scan,
identified port 8009, and came back with a question about what AJP13 was. That
question became the entire week's lesson.

---

## What I Learned

The movies make hacking look glamorous. One dramatic command and suddenly
you're in, with flashy visuals confirming your success. The reality is a black
screen full of text that you have to learn to read and interpret. And honestly,
once you understand what that text is telling you, it becomes just as exciting.
Maybe more so, because you actually know what you accomplished.

This week I learned that when one tool hits a wall you don't stop. You pivot.
When Ghostcat couldn't reach the file we needed, we didn't give up. We used
the Java RMI exploit from Week 1 as a supporting tool to locate the file and
read it through a different path entirely. That moment of chaining two
vulnerabilities together to achieve something neither could do alone was the
biggest technical breakthrough of the week.

I also learned that some of the most devastating findings in real penetration
tests aren't technical at all. Three accounts, all sharing the same default
password, never changed since installation. No exploit required. Just a
username and password that nobody bothered to update. That's a human problem,
not a technical one, and it's one of the most common critical findings in
real engagements.

---

## Commands I Need to Keep Practicing

This week reinforced something important. The commands don't stick from
reading them once. They stick from using them repeatedly across different
contexts. The ones I need to keep drilling:

| Command | What it does |
|---------|-------------|
| `msfconsole` | Opens Metasploit |
| `search [name]` | Finds modules in Metasploit database |
| `use [module]` | Loads a specific module |
| `show options` | Shows current module settings |
| `set [FIELD] [value]` | Configures a setting |
| `run` | Executes the module |
| `sessions -i [number]` | Connects to an open session |
| `shell` | Drops into raw Linux shell from Meterpreter |
| `find / -name "file" 2>/dev/null` | Searches filesystem for a file |
| `cat [filepath]` | Reads a file |

---

## How My Thinking Changed

I went into this week thinking that getting into a system would feel instant
and look impressive. What I found instead is that the most valuable moments
are quiet ones. A plain text file opening on your screen with credentials
nobody protected, or a find command returning the exact path you needed after
hitting a dead end.

The feeling when we succeeded was exactly what I imagined it would be:
exciting and rewarding. But now I understand that every frustrating step before
that moment is what made it possible. The methodology matters more than the
tools.

---

## What I Want to Explore Next

I want to understand brute force attacks more deeply. What happens when
credentials aren't sitting in a plain text file and you actually have to work
for them? Finding default passwords this week felt almost too easy. I want to
see what the process looks like when the target is properly hardened.

I also want to build my Linux command line confidence. After this week it is
clear that the terminal is where everything happens. The more natural it feels,
the more effective everything else becomes.

Before Week 3 I am also setting up dedicated learning tools: Anki flashcards
for command memorization, TryHackMe for hands on repetition, and a personal
command reference document, to make sure the knowledge from these labs
actually sticks between sessions.

---

## Security+ Concepts Encountered This Week

- Attack Surface Reduction
- Default Configuration Vulnerabilities
- Weak Password Policy
- Patch Management
- Principle of Least Privilege
- Vulnerability Chaining
- File and Directory Discovery

---

## CVE Referenced

**CVE-2020-1938: Apache Tomcat Ghostcat**
Critical vulnerability in the AJP connector allowing unauthenticated file
reads from the Tomcat web application directory. Present in all versions of
Tomcat for over thirteen years before discovery. Patched in versions 9.0.31,
8.5.51, and 7.0.100.

---

*Week 2 of the 12-week cybersecurity and ethical hacking journey.*
*Lab report: see labs/lab02-ghostcat-ajp13.md*