# Claude Code Setup Session
**Windows Edition · No coding experience required**

> 📝 **A note on Windows:** Claude Code runs in **Git Bash** — a terminal that comes bundled with Git for Windows. You'll install it in Module 1. From that point on, all commands in this guide are typed into Git Bash, not the standard Command Prompt or PowerShell.

---

## What we'll cover
1. [Git Bash — Your Terminal on Windows](#1-git-bash--your-terminal-on-windows)
2. [Git & GitHub](#2-git--github)
3. [Connecting Git and GitHub](#3-connecting-git-and-github)
4. [Claude Code Installation](#4-claude-code-installation)
5. [First Steps with Claude Code](#5-first-steps-with-claude-code)
6. [Wrap-Up & Reference](#6-wrap-up)

---

## 1. Git Bash — Your Terminal on Windows

### Why Git Bash?

Windows has its own terminals (Command Prompt and PowerShell), but Claude Code requires a Unix-style terminal. **Git Bash** provides this, and it comes bundled with Git for Windows — so you get both tools in one install.

### Installing Git for Windows (includes Git Bash)

1. Go to [git-scm.com/downloads/win](https://git-scm.com/downloads/win) and click **Download for Windows**.
2. Run the installer. Most defaults are fine. On the screen **"Choosing the default editor"**, change from Vim to **Notepad** (or Visual Studio Code if you have it) — Vim is very unfamiliar to beginners.
3. On **"Adjusting your PATH environment"**, leave the default: *Git from the command line and also from 3rd-party software*.
4. Accept all other defaults and click **Finish**.

### Opening Git Bash

1. Press the **Windows key**, type **Git Bash**, and press **Enter**.
2. A dark window opens with a blinking cursor. This is Git Bash — your terminal for the rest of this session.

> 💡 **Tip:** Pin Git Bash to your taskbar — right-click its icon while it's open and choose **Pin to taskbar**.

You'll see a prompt like this:

```
yourname@DESKTOP-XXXXX MINGW64 ~
$
```

The `$` is where you start typing.

### Your first commands

Find out where you are:
```
pwd
```
*Print working directory.* Shows your current folder, e.g. `/c/Users/yourname`.

See what's in this folder:
```
ls
```
*List.* Shows files and folders at your current location.

### Moving between folders

Move into a folder:
```
cd Desktop
```

Go up one level:
```
cd ..
```

Open the current folder in File Explorer:
```
explorer .
```

Run `pwd` any time to check where you are.

---

## 2. Git & GitHub

**Git** tracks the history of changes you make to files — like Google Docs version history, except for any file, and you control when each snapshot (called a *commit*) is saved.

**GitHub** stores your Git history in the cloud. Git runs on your computer; GitHub stores your work online. Together they give you a backup, a way to share work, and a place to publish websites for free.

### Step 1: Verify Git is installed

Git was installed alongside Git Bash in Module 1. Confirm it's working:

```
git --version
```

You should see a version number. If not, re-run the Git for Windows installer.

### Step 2: Tell Git who you are

```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Confirm the settings were saved:

```
git config --list
```

Look for lines starting with `user.name` and `user.email`.

> 📝 Use the same email address you'll use for your GitHub account.

### Step 3: Create a GitHub account

1. Go to [github.com](https://github.com) and click **Sign up**.
2. Choose a username — it will appear in your project URLs.
3. Verify your email address when the confirmation arrives.

### Step 4: Set up SSH authentication

SSH connects your terminal to GitHub securely. Once set up, you'll never be prompted for credentials again.

**Check for an existing key:**
```
ls ~/.ssh
```
If you see `id_ed25519` and `id_ed25519.pub`, skip to "Start the SSH agent." Otherwise:

**Generate a new key** (use your GitHub email):
```
ssh-keygen -t ed25519 -C "you@example.com"
```
Press **Enter** to accept the default location. Press Enter again to skip the passphrase, or enter one for extra security.

**Start the SSH agent and add your key:**
```
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

**Copy your public key to the clipboard:**
```
clip < ~/.ssh/id_ed25519.pub
```

**Add it to GitHub:**
1. Go to [github.com/settings/keys](https://github.com/settings/keys)
2. Click **New SSH key**
3. Give it a name like *My Windows PC*
4. Paste with **Ctrl+V** and click **Add SSH key**

**Test the connection:**
```
ssh -T git@github.com
```
If asked whether to trust github.com, type `yes` and press Enter. You should see:
```
Hi username! You've successfully authenticated
```

---

## 3. Connecting Git and GitHub

### Clone a public repository

To *clone* a repository means to download a complete copy — including its full history — to your computer.

```
cd ~
git clone git@github.com:WomenDefiningAI/claude-code-skills.git
cd claude-code-skills
ls
```

The `ls` output shows the files and folders inside the repository. In Module 5 you'll ask Claude to explain what's here.

### Create your own private repository

1. On GitHub, click **+** (top-right) → **New repository**
2. Name it `my-first-repo` and set visibility to **Private**
3. Leave "Initialize this repository" **unchecked**
4. Click **Create repository** — keep this tab open for the SSH URL

### Push your first code to GitHub

Create the project folder:
```
cd ~
mkdir my-first-repo
cd my-first-repo
git init
```

Create a placeholder file:
```
echo "# My First Repo" > README.md
```

Stage the file, then check what Git is about to commit:
```
git add .
git status
```
You'll see `README.md` listed under "Changes to be committed" in green.

Save the snapshot, then view your commit history:
```
git commit -m "First commit"
git log --oneline
```
You'll see a one-line entry with a short ID and your commit message. Every commit you make will appear here.

Connect your local folder to GitHub (paste the SSH URL from the tab you kept open):
```
git remote add origin git@github.com:YOUR-USERNAME/my-first-repo.git
```

Push to GitHub:
```
git push -u origin main
```

✅ Refresh your GitHub repository page — `README.md` should have appeared.

### Branches: exploring ideas in parallel

A *branch* is an independent copy of your project where you can try something new without touching the main version. With Claude Code, Claude works in a branch and you only merge when you're happy with the result.

Create a branch and switch to it:
```
git checkout -b my-first-branch
```

The `-b` flag means "create and switch." Run `git branch` to confirm — the current branch has a `*` next to it.

Make a change, commit, and push the branch:
```
echo "Experimenting on a branch" >> README.md
git add .
git commit -m "Try something on a branch"
git push -u origin my-first-branch
```

Merge back into main when you're satisfied:
```
git checkout main
git merge my-first-branch
git push
```

### Worktrees: truly working in parallel

Branches are great, but switching between them means stopping what you're doing. **Worktrees** let you have multiple branches checked out in separate folders *at the same time*. With Claude Code, you can have Claude working on a new feature in one worktree while you review something else in another — no interruptions.

Create a new worktree with its own branch:
```
mkdir -p ../worktrees
git worktree add -b feature-idea ../worktrees/feature-idea
```

This creates a new folder `worktrees/feature-idea` next to your project, already on a new branch. Both folders share the same Git history.

Work in the new worktree:
```
cd ../worktrees/feature-idea
# Make changes, run Claude, commit — without touching your main folder
```

See all active worktrees:
```
git worktree list
```

Merge and remove when done:
```
cd ~/my-first-repo
git merge feature-idea
git push
git worktree remove ../worktrees/feature-idea
```

> 📝 **The Claude Code workflow:** Before asking Claude to work on any significant change, create a new worktree. Claude works in its own folder, you can review the main project at the same time, and merging is a deliberate choice — not an accident.

---

## 4. Claude Code Installation

Claude Code requires a **Claude Pro** subscription or higher (Pro, Max, Team, or Enterprise).

1. Go to [claude.ai](https://claude.ai) and sign up or log in.
2. If you don't have a paid plan, go to [claude.ai/upgrade](https://claude.ai/upgrade). The Pro plan ($20/month) is sufficient for this tutorial.

Install Claude Code:
```
curl -fsSL https://claude.ai/install.sh | bash
```

Verify the installation:
```
claude --version
```

Run the health check:
```
claude doctor
```

✅ `claude doctor` passing is your confirmation for this module.

---

## 5. First Steps with Claude Code

Navigate into the tutorial repository:
```
cd ~/claude-code-skills
```

Launch Claude Code:
```
claude
```

The first time you launch, you'll be prompted to log in — follow the on-screen instructions. This only happens once.

### Explore the repository

Type the following prompt and press **Enter**:

```
Please explore this repository and give me a summary of how it's organized,
what the main files and folders are, and what this project appears to do.
```

Claude will read through the files and write you a plain-English summary. When it asks permission to read files, type **y** and press Enter.

Then go deeper:

```
Which file would be the best starting point to understand how this project works?
```

### Exiting and resuming sessions

Exit the session:
```
/exit
```

Resume your most recent session instantly (full context intact):
```
claude --continue
```

Choose from past sessions:
```
/resume
```
(run this from inside Claude Code)

---

## 6. Wrap-Up

You've set up:

- **Git Bash** — navigate folders and run commands
- **Git** — installed, configured, with a grasp of commits, branches, and worktrees
- **GitHub** — account created, SSH authentication set up, code pushed to the cloud
- **Claude Code** — installed, authenticated, verified, and you've had your first conversation

---

## Quick Reference

| Command | What it does |
|---|---|
| `pwd` | Show the folder you're currently in |
| `ls` | List files and folders at your current location |
| `cd foldername` | Move into a folder |
| `cd ..` | Go up one level |
| `explorer .` | Open the current folder in File Explorer |
| `git --version` | Check Git is installed |
| `git config --list` | View your Git configuration |
| `git init` | Start tracking a folder with Git |
| `git clone <url>` | Download a copy of a GitHub repository |
| `git add .` | Stage all changes for a snapshot |
| `git status` | Show what's staged and what's changed |
| `git log --oneline` | Show a compact history of commits |
| `git commit -m "msg"` | Save a snapshot with a description |
| `git push` | Upload your snapshots to GitHub |
| `git branch` | List branches and see which you're on |
| `git checkout -b name` | Create a new branch and switch to it |
| `git checkout main` | Switch back to the main branch |
| `git merge branchname` | Merge a branch into the current branch |
| `git worktree add -b branch ../worktrees/folder` | Create a new worktree on its own branch |
| `git worktree list` | See all active worktrees |
| `git worktree remove ../worktrees/folder` | Remove a worktree when done |
| `ssh-keygen -t ed25519 -C "email"` | Generate an SSH key pair |
| `ssh -T git@github.com` | Test your GitHub SSH connection |
| `claude --version` | Check Claude Code is installed |
| `claude doctor` | Run a health check on Claude Code |
| `claude` | Start a Claude Code session |
| `claude --continue` | Resume your most recent session |
| `/resume` | Choose from past sessions (inside Claude Code) |
| `/exit` | Exit a Claude Code session |
