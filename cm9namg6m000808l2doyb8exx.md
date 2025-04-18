---
title: "Git & GitHub Challenge: My Hands-on Journey"
datePublished: Fri Apr 18 2025 21:20:16 GMT+0000 (Coordinated Universal Time)
cuid: cm9namg6m000808l2doyb8exx
slug: git-and-github-challenge-my-hands-on-journey
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1745011106026/46e1dab0-b667-42b8-b029-74f5edae0e60.png
tags: github, git, devops, 90daysofdevops

---

Hi everyone!

I'm super excited to share what I did in **Week 4** of the #90DaysOfDevOps challenge. As someone new to blogging and still getting comfortable with Git and GitHub, this was a great learning experience. I'm writing this in a simple and beginner-friendly way, so even if you're not technical, you can understand what's going on. Let's get into it!

---

**📚 What This Week Was All About**

This week's focus was on learning **Git** and **GitHub** — tools that help developers keep track of their code and collaborate easily. Here’s what we covered:

* Basic Git commands (git init, git add, git commit)
    
* Managing GitHub repositories (cloning, forking)
    
* Branching and switching
    
* Authentication with PAT (Personal Access Token) and SSH
    
* Bonus task: Handling merge conflicts!
    

---

**✅ Task 1: Forking & Cloning**

I started by forking the main repository to my own GitHub profile, then cloned it using:

git clone https://github.com/&lt;your-username&gt;/90DaysOfDevOps.git

cd 2025/git/01\_Git\_and\_Github\_Basics

---

**✅ Task 2: Creating the Challenge Folder & File**

I created a folder named week-4-challenge, but I learned not to run git init inside it, or else it would become a separate Git repository (called a **submodule**) — which caused some push issues. So instead, I just created the folder, added a file, and used Git commands from the main repo root.

`mkdir week-4-challenge`

`cd week-4-challenge`

`echo "My name is Shubham, and I love DevOps!" > info.txt`

`git add info.txt`

`git commit -m "Initial commit: Add info.txt"`

`git push origin master`

---

**✅ Task 3: Pushing with Personal Access Token (PAT)**

To push without typing my PAT every time, I set the remote like this:

git remote set-url origin https://&lt;username&gt;:&lt;PAT&gt;@github.com/&lt;username&gt;/90DaysOfDevOps.git

git push origin master

This worked — but I also learned that storing PAT in the URL is not secure and should only be used for testing.

Note: For the above task, I followed these steps:

Added the remote origin using the HTTPS URL of my 90DaysOfDevOps repository:

git remote add origin Then I updated the remote URL (if already set) using:

git remote set-url origin These steps should be done from the root (main) folder of your repository — i.e., 90DaysOfDevOps.

Once that’s done, navigate to the week-4-challenge folder, make your changes, and push them using:

`git push origin master`

---

**✅ Task 4: Checking Commit History**

Super easy! Just:

`git log`

This shows all your commits with timestamps, authors, and messages.

---

**✅ Task 5: Branching, Switching & Merge Conflict**

I created a new branch for my feature:

`git branch feature-update`

`git switch feature-update`

`echo "Adding more details..." >> info.txt`

`git add info.txt`

`git commit -m "Feature update: Add more details"`

`git push origin feature-update`

Then, I created another branch experimental to simulate a merge conflict. After editing the same lines in both branches, I tried to merge and got a conflict!

I resolved it manually and committed the fix:

`git add info.txt`

`git commit -m "Resolve merge conflict"`

It was tricky but very satisfying!

---

**🔎 Task 6: Why Branching Matters**

In solution.md, I documented all the Git commands I used. **🧠 Why Branching Strategies Are Important in Collaborative Development**

When multiple people are working on the same codebase, things can get messy really fast. That's where **branching strategies** come in—they help keep everything clean, organized, and under control.

Here’s why they’re so important:

**🧩 1. Isolating Features and Bug Fixes**

Instead of working directly on the main code, developers create separate branches for new features or bug fixes. This way:

* You can work without affecting the main project.
    
* If something breaks, it doesn’t impact everyone else.
    
* It’s easy to test and review just that piece of work.
    

**👥 2. Facilitating Parallel Development**

Branching lets different people (or teams) work on different tasks **at the same time** without stepping on each other’s toes. For example:

* One person can be building a login system.
    
* Another can be fixing a design bug.
    
* Both can work independently and merge their work later.
    

**🔀 3. Reducing Merge Conflicts**

When changes are isolated in separate branches, it's easier to **merge them safely**. You get fewer situations where two people edited the same file at the same time—aka **merge conflicts**, which are annoying and tricky to fix.

**👀 4. Enabling Effective Code Reviews**

Before merging a branch into the main project, teams often review the code through **Pull Requests (PRs)**. This helps:

* Catch bugs or mistakes.
    
* Share knowledge across the team.
    
* Ensure code meets the team's quality standards.
    

---

**🎉 Final Thoughts**

I faced errors, I Googled a lot, I even broke my repo once! But every step taught me something new. This was hands-on learning at its best. If you're just starting out — don’t worry. Mistakes are part of the journey. Just keep pushing (literally and figuratively 😉).

Let me know if you faced similar issues or have tips to share. Let's grow together!

---

Thanks for reading!

---

*This post is part of the #90DaysOfDevOps challenge by Shubham Bhaiya from TWS. Connect with me on* [*LinkedIn*](https://www.linkedin.com/in/shubhamnaidu18/) *to stay updated!*