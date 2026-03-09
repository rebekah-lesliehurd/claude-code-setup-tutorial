# Claude Code Office Hours — File Navigation Session

**Time:** ~25–30 minutes  
**Pre-requisites**: Claude Code installation (terminal or app) and Pro subscription

---

## Warm-Up: Where Are We?

**Prompt to try:**
```
Where am I right now? Show me what files and folders are here
```

**What to look for:**  
- Claude tells you your current directory (e.g., `/Users/yourname`)  
- It lists files and folders it can see  

**Why this matters:** Before you move or create anything, you need to know where you are. Claude can always orient you — you never have to memorize a command.

---

## Exercise 1: Create Your First Folder 

**Goal:** See how Claude translates plain English into a file operation.

**Prompt to try:**
```
Create a new folder called my-project in the current directory
```

**What to watch for:**  
- Claude will attempt to run a terminal command like `mkdir ~/my-project`  
- Before it runs, it will ask for permission to run the command (type Ctrl-e for an explanation)  
- Use the arrows and return key to select "Yes" to give Claude Code permission to run the command

**Note:** You can control which commands Claude Code will ask permission to run by editing `.claude/settings.json`
 

**Follow-up prompt:**
```
Now show me the contents of my home directory again so I can confirm the folder was created.
```

**Follow-up prompt:**  
```
Let's switch to working in my-project
```

---

## Exercise 2: Create a CLAUDE.md Instruction File

**Goal:** Tell Claude how to behave — so it always explains commands before running them

Some terminal commands are hard to undo. `rm -rf` for example can permanently delete files. As we saw, Claude can explain the commands it is trying to run - let's make this the default by creating a `CLAUDE.md` file for our project

> 💡 **What is a .md file?** Markdown is just a text file with lightweight formatting rules — asterisks for bold, hashtags for headings, that kind of thing. It's used everywhere: GitHub READMEs, documentation, notes apps. You don't need to learn the syntax — Claude can write it for you 

**Prompt to try:**
```
Create a CLAUDE.md file inside my-project. It should tell you to always explain what a command does in plain English before running it, and to warn me clearly if a command could be difficult or impossible to reverse.
```

**What to watch for:**  
- Claude will ask for permission to create a new file, `CLAUDE.md` (select yes)  
- You can open the .md file in a text editor or ask Claude Code to show you the contents  
- At start up, Claude Code automatically reads CLAUDE.md as its instructions for that project.  Think of it like leaving a note for Claude that says "here's how I want you to work with me"  
- You will need to exit Claude Code and launch from the my-project directory for the instructions to take effect

**Follow-up prompt:** Confirm the new instructions are working  
```Create a folder called test-folder```
```Delete the test folder we just created```

---

## Exercise 3: Build a Terminal Cheat Sheet

**Goal:** Create a reference for common terminal commands

**Prompt to try:**
```
Create a markdown file called terminal-cheatsheet.md inside my-project. Include the 10 most common terminal commands a beginner should know. For each one, write a plain-English explanation of what it does and note whether it's reversible or not.
```

**What to watch for:**
Claude will create an .md file with an explanation of commands like `ls`, `cd`, `mkdir`, `mv`, `cp`, `rm` — including guidance on which commands to be careful with.

**Tip:** Use Claude Code to extend this reference with new commands over time

**Follow-up to try:**. 
```
Show me what terminal-cheatsheet.md looks like.
```

---

## Wrap-Up

Ask Claude:
```
Show me everything inside my-project so I can see what we've created.
```

You should see your `CLAUDE.md` and `terminal-cheatsheet.md`. You've created a folder, set up instructions for Claude, and built a reference guide — well done!

---
---

## ⭐ Bonus Exercise: Clean Up Your Downloads Folder

**Best for:** After the session, on your own, or if time permits.

**Goal:** Use everything from today on a real task — and see your CLAUDE.md guardrails in action.

**Before you start:** Copy your `CLAUDE.md` to your home directory so Claude follows those rules everywhere, not just inside `my-project`.

```
Copy the CLAUDE.md file from my-project to my home directory.
```

**Then try:**
```
Look at my Downloads folder and tell me what's in there. Don't move or delete anything yet — just give me a summary of what you see.
```

Then, once you've reviewed:
```
I'd like to clean up my Downloads folder. Can you suggest a plan? Group files by type and flag anything that looks safe to delete. Explain each step before you do anything.
```

**What to watch for:**
- Claude should explain every command before running it (your CLAUDE.md at work!)
- It should flag any deletions as irreversible and ask you to confirm
- You may see new commands — check your cheat sheet, or just ask: *"What does that command do?"*

> ⚠️ **Go slow here.** This is real data. If Claude proposes deleting something, read the explanation carefully before approving. This is exactly the scenario your CLAUDE.md was built for.
