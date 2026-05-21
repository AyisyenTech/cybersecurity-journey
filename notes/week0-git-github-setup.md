# Week 0 — Git & GitHub Setup
> **Pre-Roadmap Foundation** | Completed before Week 1 of the 12-week cybersecurity journey
> 
> This note documents everything learned and accomplished before the official roadmap began. This is the foundation that makes the entire journey possible.

---

## What I Learned

### Git vs GitHub — The Core Difference

This was the first and most important concept. These two things are NOT the same.

| | Git | GitHub |
|---|---|---|
| **What it is** | Version control software | Cloud hosting platform |
| **Where it lives** | On YOUR computer (local) | On the internet (remote) |
| **What it does** | Tracks changes to your files | Stores and displays your work publicly |
| **Analogy** | Like saving backup copies of a file automatically | Like a shared network drive anyone can see |

**The workflow in simple terms:**
```
You make changes locally → Git tracks them → GitHub stores them online
```

---

### Key Concepts & Terminology

**Repository (Repo)**
A folder that Git is tracking. Every change made inside it is recorded. Think of it like a project folder with a full history of every edit ever made.

**Local Repo**
The copy of your repo living on YOUR machine. This is where you do your actual work.

**Remote Repo**
The copy of your repo living on GitHub. This is what the world sees.

**Clone**
Copying a repo from GitHub down to your local machine. Like downloading a project and its full history.
```
git clone https://github.com/username/repo-name.git
```

**Commit**
A saved checkpoint of your work. Like hitting "save" but smarter , every commit has a message explaining what changed.
```
git commit -m "Your message here"
```

**Push**
Sending your local commits up to GitHub.
```
git push
```

**Staging**
The step between making changes and committing them. Like putting items in a box before sealing and shipping it.
```
git add .       ← puts everything in the box
git commit      ← seals the box with a label
git push        ← ships the box to GitHub
```

**Branch**
A separate version of your repo. The default branch is called `main`.

**PAT (Personal Access Token)**
How Git authenticates with GitHub instead of using your password. Generated on GitHub and used as a password substitute in the terminal.

---

## The Full Git Workflow

Every time you complete work, this is the loop:

```
1. Make changes to your files locally
       ↓
2. git add .
   (stage everything)
       ↓
3. git commit -m "Describe what you did"
   (seal the checkpoint)
       ↓
4. git push
   (send it to GitHub)
```

---

## Markdown Basics

GitHub READMEs are written in Markdown , a simple formatting language. No special software needed, just symbols.

| Symbol | What it does | Example |
|---|---|---|
| `#` | Big heading (H1) | `# My Title` |
| `##` | Medium heading (H2) | `## Section` |
| `###` | Small heading (H3) | `### Subsection` |
| `-` | Bullet point | `- Item` |
| `**text**` | Bold text | `**important**` |
| `>` | Blockquote / indented note | `> Security+ Domain` |
| `[text](url)` | Clickable link | `[GitHub](https://github.com)` |

**Important rule:** Each heading or bullet point goes on its own line. Spacing matters.

---

## Repo Structure Built

```
📁 cybersecurity-journey/
├── 📄 README.md        ← Portfolio front page, roadmap lives here
├── 📄 .gitignore       ← Protects sensitive files from being pushed
├── 📁 notes/           ← Written notes from each week (you are here)
├── 📁 labs/            ← Lab writeups and hands-on work
└── 📁 certs/           ← Certification progress and achievements
```

---

## .gitignore — Why It Matters

`.gitignore` tells Git which files to **never push to GitHub**, no matter what.

This is a security control. Without it, sensitive files can accidentally become public.

**Real world risk:** Developers have accidentally pushed API keys and credentials to public GitHub repos. Attackers actively scan GitHub for exactly this. Bills of thousands of dollars have been generated within hours of an accidental credential push.

**What our .gitignore protects:**
```
# Windows system files
Thumbs.db
Desktop.ini
$RECYCLE.BIN/

# Personal notes you don't want public
personal/
private/

# Environment & credential files  ← MOST IMPORTANT
.env
*.key
*.pem
*.password

# Lab files you want to keep local
/local-only/

# OS generated files
.DS_Store
```

**How to test it's working:**
```
touch .env          ← create a test file that should be ignored
git status          ← .env should NOT appear in the output
rm .env             ← clean up the test file
```

---

## Laptop Setup — Step by Step

### 1. Install Git
- Download from **git-scm.com**
- Version installed: **2.54.0**

**Key installation choices made:**
| Option | Choice | Why |
|---|---|---|
| Default editor | VS Code | Beginner friendly, industry standard |
| Default branch | main | Matches GitHub's default |
| Line endings | Windows style checkout, Unix commit | Compatible with Linux labs |
| Terminal emulator | MinTTY | Unix-like experience for cybersecurity work |
| Credential helper | Git Credential Helper | Saves PAT so you don't retype it |
| Scalar | Unchecked | Enterprise tool, unnecessary for our use |
| Auto-update | Unchecked | Control what changes on your lab machine |

### 2. Configure Git Identity
```
git config --global user.name "Your Name"
git config --global user.email "your-noreply@users.noreply.github.com"
```
> ⚠️ Use your GitHub no-reply email, NOT your personal email. This protects your privacy on public repos.

**Verify your config:**
```
git config --global --list
```

### 3. Set VS Code as Default Editor
```
git config --global core.editor "'C:/Users/YourUsername/AppData/Local/Programs/Microsoft VS Code/bin/code.cmd' --wait"
```
> The `--wait` flag tells Git to wait for you to close VS Code before continuing.

### 4. Add VS Code to Git Bash PATH
```
echo 'export PATH="$PATH:/c/Users/YourUsername/AppData/Local/Programs/Microsoft VS Code/bin"' >> ~/.bashrc
source ~/.bashrc
```
> This lets you type `code filename` directly in Git Bash without needing the full path.

### 5. Clone Your Repo
```
cd Documents
mkdir cybersecurity
cd cybersecurity
git clone https://github.com/yourusername/cybersecurity-journey.git
cd cybersecurity-journey
```

### 6. Verify Everything Works
```
git --version         ← confirms Git is installed
git config --global --list  ← confirms your identity is set
ls                    ← confirms repo contents are there
git status            ← confirms repo is clean and connected
```

---

## Commit Message Convention

Good commit messages follow this format:
- **Short** - under 72 characters
- **Action oriented** - start with a verb
- **Present tense** - written as an instruction

```
✅ Add 12-week cybersecurity roadmap to README
✅ Add notes, labs, and certs folders
✅ Add .gitignore to protect sensitive files

❌ Added some folders
❌ Stuff
❌ I made changes to the repository files today
```

---

## Repo Naming Convention

GitHub repo names follow developer conventions:
- **Lowercase** - terminals are case sensitive
- **Hyphens** - instead of spaces : spaces break terminal commands
- **No special characters** - `&`, `@`, `!` can break commands

```
✅ cybersecurity-journey
❌ Cybersecurity Journey
❌ Cybersecurity & Ethical Hacking Journey
```

---

## Important Commands Reference

```
git --version                    Check Git version
git config --global --list       See your Git configuration
git status                       See what's changed locally
git add .                        Stage all changes
git add filename                 Stage a specific file
git commit -m "message"          Commit with inline message
git commit --amend --reset-author  Fix author info on last commit
git push                         Push to GitHub
git clone [url]                  Clone a repo locally
ls                               List files in current folder
cd foldername                    Navigate into a folder
mkdir foldername                 Create a new folder
touch filename                   Create an empty file
rm filename                      Delete a file
source ~/.bashrc                 Reload Git Bash configuration
```

---

## Lessons Learned

- **GitHub is the connective tissue** between all your learning projects and machines
- **Git lives on your machine, GitHub lives in the cloud** — they work together but are separate things
- **Empty folders are invisible to Git** — use `.gitkeep` as a placeholder file
- **Always test your controls** — we tested `.gitignore` before committing it
- **Proofread before committing** — just like reviewing a GPO before pushing it to production
- **Control what changes on your lab machine** — don't auto-update tools mid-session
- **Your no-reply email protects your privacy** on public repos

---

*Note compiled from hands-on learning session — Week 0 of the cybersecurity journey.*
*Everything in this note was learned by doing, not just reading.*
