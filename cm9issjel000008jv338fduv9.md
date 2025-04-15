---
title: "DevOps for Beginners: Linux Basics You Can Understand"
datePublished: Tue Apr 15 2025 17:50:03 GMT+0000 (Coordinated Universal Time)
cuid: cm9issjel000008jv338fduv9
slug: devops-for-beginners-linux-basics-you-can-understand
tags: linux, devops, log-analysis, user-management, file-permissions-linux-unix-acls-access-control-lists-security-permissions-chmod-chown-setfacl-getfacl-octal-notation-symbolic-notation-user-permissions-group-permissions-other-permissions-fine-grained-access-control-file-ownership-file-system-security-command-line-operating-systems

---

Hey there! 👋  
If you've ever felt like Linux is some scary dark screen full of hacker code, don't worry — you’re not alone. Today, we're diving into a few beginner-friendly Linux tasks that are actually super fun and powerful. And yes, you *can* do this even if you’ve never used a terminal before.

Let’s go step by step. We’ll cover:

1. **User & Group Management**
    
2. **File & Directory Permissions**
    
3. **Log File Analysis using AWK, Grep & Sed**
    

Let’s gooo! 🚀

---

## 1️. User & Group Management: Who’s Allowed to Do What?

Think of Linux like a shared apartment. Every person (user) has their own keys, and groups of people can share access to certain rooms (directories).

### 🧠 What’s What?

* **User** – a person using the system.
    
* **Group** – a collection of users (like a team).
    
* **Permissions** – control what users/groups can read/write/execute.
    

All of this info lives in special files:

* `/etc/passwd` – stores user info.
    
* `/etc/group` – stores group info.
    

### ✅ Task: Create a User & Give Sudo Powers

* Create a user devops\_user and add them to a group devops\_team.
    
* Set a password and grant sudo acces
    

**Steps:**

```plaintext
# Create a user
sudo useradd -m devops_user

# Create a group
sudo groupadd devops_team

# Add user to group
sudo gpasswd -a devops_user devops_team

# Set a password
sudo passwd devops_user

# Give sudo access (admin powers)
sudo gpasswd -a devops_user sudo
```

> 🔒 **Sudo** = Superpowers. It allows a user to run admin-level commands.

✅ Done! You’ve created a user, added them to a group, and handed them some serious power (responsibly, of course).

---

## 2️. File & Directory Permissions: Who Can Access What?

Imagine a file cabinet:

* **Owner** – the person who created the file.
    
* **Group** – their team.
    
* **Others** – everyone else.
    

### ✅ Task: Create Folder & Set Permissions

**Step 1:** Create /devops\_workspace and a file project\_notes.txt.

```plaintext
# Create Group
mkdir devops_workspace

# Create File
touch project_notes.txt
```

**Step 2: Set permissions: -** Owner can edit, group can read, others have no access.

```plaintext
# Changing the permission of file
chmod 240 project_notes.txt
```

* **2 = Owner can write**
    
* **4 = Group can read**
    
* **0 = Others have no access**
    

**Step 3: Check it worked**

```plaintext
ls -l 
```

You’ll see something like:

```plaintext
--w-r----- 1 devops_user devops_team 0 Apr 15 12:00 project_notes.txt
```

> 🔍 Quick Breakdown:  
> `rw-` → Owner can read/write  
> `r--` → Group can read  
> `---` → Others get nada

Nice! You've officially locked it down like a pro.

---

## 3️. Log File Analysis: Becoming a Mini Sherlock 🕵️‍♂️

Logs are like the system’s diary. DevOps folks *love* logs — they help find problems, patterns, and performance issues.

Let’s analyze a log file using the most useful Linux command trio: **grep**, **awk**, and **sed**.

### 🗂️ Get the Log File

First, download the file (from [LogHub GitHub repo](https://github.com/cyberlabsai/loghub), or wherever the `Linux_2k.log` lives):

```plaintext
get https://your-repo-path/Linux_2k.log
```

---

### 🔎 Step 1: Find All Errors with `grep`

```plaintext
grep "authentication failure" Linux_2k.log
```

> `grep` searches for specific words or patterns. Here, we’re hunting for the word *error*.

---

### 🕒 Step 2: Extract Timestamps & Log Levels with `awk`

```plaintext
awk '/authentication failure/ {print $1, $2, $3}' Linux_2k.log
```

This grabs the first three columns — typically timestamps and log level (like INFO, ERROR).

Want both time & log type? Try:

```plaintext
awk '/authentication failure/ {print $1, $2, $3, $12, $13, $14}' Linux_2k.log
```

---

### 🛡️ Step 3: Hide IP Addresses with `sed`

```plaintext
sed -E 's/[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+/[REDACTED]/g' Linux_2k.log > secure_log.log
```

This replaces every IP address with `[REDACTED]` to keep things private.

---

### 💥 Bonus: Find the Most Frequent Log Entry

```plaintext
cat Linux_2k.log | sort | uniq -c | sort -nr | head -10
```

* `sort` – arranges lines.
    
* `uniq -c` – counts duplicates.
    
* `sort -nr` – sorts by count, highest first.
    
* `head -10` – shows top 10.
    

Boom 💣 — now you know what’s happening *most often* in your logs.

---

## 👨‍🏫 Final Thoughts

If you made it this far, you’ve done:

* User and group management 🧑‍🤝‍🧑
    
* File permissions like a gatekeeper 🔐
    
* Log file analysis like a detective 🕵️
    

Not bad for someone who thought Linux was all "matrix" stuff, huh?

> 📌 Pro Tip: Practice these in a safe environment (like a virtual machine or online Linux lab). You’ll get the hang of it faster.

Want more beginner-friendly DevOps magic? Let me know what topic you want next! 💬