---
title: "Git & GitHub Advanced"
datePublished: Tue Apr 29 2025 19:14:45 GMT+0000 (Coordinated Universal Time)
cuid: cma2vze5v000409l27y0h7agi
slug: git-and-github-advanced
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1745954051285/b596b71e-8d0e-4020-b2fc-d7e629300c23.png
tags: github, git-and-github-advanced-challenge

---

Git & GitHub Advanced Challenge This challenge covers advanced Git concepts essential for real-world DevOps workflows. By the end of this challenge, you will: • Understand how to work with Pull Requests effectively. • Learn to undo changes using Reset & Revert. • Use Stashing to manage uncommitted work. • Apply Cherry-picking for selective commits. • Keep a clean commit history using Rebasing. • Learn industry-standard Branching Strategies. Topics Covered

1. Pull Requests – Collaborating in teams.
    
2. Reset & Revert – Undo changes safely.
    
3. Stashing – Saving work temporarily.
    
4. Cherry-picking – Selecting specific commits.
    
5. Rebasing – Maintaining a clean history.
    
6. Branching Strategies – Industry best practices. Challenge Tasks Task 1: Working with Pull Requests (PRs) Scenario: You are working on a new feature and need to merge your changes into the main branch using a Pull Request.
    
7. Fork a repository and clone it locally.
    
8. git clone cd
    
9. Create a feature branch and make changes.
    
10. git checkout -b feature-branch
    
11. echo "New Feature" &gt;&gt; feature.txt
    
12. git add . git commit -m "Added a new feature"
    
13. Push the changes and create a Pull Request. git push origin feature-branch
    
14. Open a PR on GitHub, request a review, and merge it once approved.
    

Steps :- • Open your GitHub profile. • Navigate to the repository and lick “Compare & Pull Request”

![image](https://github.com/user-attachments/assets/ef2cd693-e5a2-4972-ac27-b603d8be0fff align="left")

• Select the base branch where you want to merge and select from which branch you want to merge. • Then create pull request.

![image](https://github.com/user-attachments/assets/3cead55f-8102-4ee8-85b1-95727e4382a6 align="left")

• Once click on the Create pull request.

![image](https://github.com/user-attachments/assets/1fc0a5e8-b3ae-4ff2-9e32-dc21d06bac45 align="left")

• You need to add the Description also you can ask your senior or colleague to review the pull request and the file that you have created. • Once you have assigned the reviewers and the description, then you can create pull request.

![image](https://github.com/user-attachments/assets/f7a892bb-f511-453c-b605-07904284cac4 align="left")

• As you can see in the screenshot there is no reviewers in it but assume you have assigned the reviewer and they have reviewed the request and approved it. • Once it is approved you can see the latest comment. • If it is mentioned that it is approved then you just need to click on merge pull request. • Then it will ask you to confirm the merge before that always put description.

![image](https://github.com/user-attachments/assets/205e931f-bf12-4c75-9964-e99fa31c3a91 align="left")

• Once you click on confirm merge then pull request will be succeed.

![image](https://github.com/user-attachments/assets/dff7fdd0-0282-4a5a-8f65-82d25eddd467 align="left")

Document in [solution.md](http://solution.md) • Steps to create a PR. • Best practices for writing PR descriptions. • Handling review comments. 🛠️ Pull Request (PR) Workflow Guide ✅ Steps to Create a Pull Request (PR)

1. Create a Feature Branch
    

git checkout -b feature/your-feature-name 2. Make Changes and Commit git add . git commit -m "Add a meaningful commit message" 3. Push the Feature Branch git push origin feature/your-feature-name 4. Open a Pull Request on GitHub o Navigate to the repository. o Click "Compare & Pull Request". o Choose the base branch (e.g., main or develop) and your feature branch. o Add a title and description, then click "Create Pull Request".

---

✍️ Best Practices for Writing PR Descriptions Clear communication in PRs improves collaboration and code quality. Structure your description like this: 🔍 What does this PR do? Brief summary of the change. E.g., "Implements login functionality using JWT." 📋 Changes made • Added authService.ts for token generation. • Updated login API to validate credentials. • Added unit tests. ✅ Checklist • Code is linted • Unit tests added • No breaking changes 📝 Related Issue Closes #123 or Fixes bug described in \[link\]

---

💬 Handling Review Comments

1. Stay open to feedback Reviews are about the code, not you.
    
2. Reply to each comment Acknowledge the feedback. Use: o ✅ Fixed o 🤔 Need clarification o 🚫 Won’t fix (with reason)
    
3. Make necessary changes Update your branch with changes and push again: git add . git commit -m "Refactor: address review feedback" git push origin feature/your-feature-name
    
4. Resolve comments on GitHub Mark them as "Resolved" once handled.
    

Task 2: Undoing Changes – Reset & Revert Scenario: You accidentally committed incorrect changes and need to undo them.

1. Create and modify a file.
    
2. echo "Wrong code" &gt;&gt; wrong.txt
    
3. git add .
    
    ![image](https://github.com/user-attachments/assets/a9c154fd-1ae3-4a18-bdaf-745b77da128f align="left")
    

git commit -m "Committed by mistake"

4. Soft Reset (keeps changes staged). git reset --soft HEAD~1:- it will untrack and stag the file last committed file.
    
5. Mixed Reset (unstages changes but keeps files). git reset --mixed HEAD~1 :- it will untrack the file last committed file.
    
6. Hard Reset (removes all changes). git reset --hard HEAD~1 :- it will delete the file last committed file.
    

As you can see wrong file is deleted and it also not in untrack.

7. Revert a commit safely. git revert HEAD :- it will revert the last head commit. As per last command git reset –hard it will delete the committed the file(wrong file) and the log for it. Not when you do revert HEAD then it will revert the last committed file that will feature file which was committed in task 1.
    

Document in [solution.md](http://solution.md) • Differences between reset and revert. • When to use each method.

🔁 Differences Between git reset and git revert 🧠 Conceptual Difference Feature git reset git revert What it does Moves the branch pointer to an earlier commit Creates a new commit that undoes a previous one Affects history Rewrites commit history Preserves history Safe for shared branches ❌ No (can cause issues for others) ✅ Yes (safe for collaboration) Undo visibility Changes are not visible to others (unless pushed with --force) Revert is visible as a new commit

---

🧪 When to Use Each Method ✅ Use git reset when: • You're working locally, and • You want to undo commits or unstage files without keeping the history. • Useful during development or practice. Example: bash CopyEdit git reset --soft HEAD~1 # Undo commit but keep changes staged git reset --mixed HEAD~1 # Undo commit and unstage changes git reset --hard HEAD~1 # Undo commit and discard changes (use with caution!) ✅ Use git revert when: • You're working on a shared branch (e.g., main, develop) • You want to safely undo a specific commit while keeping the history. • You need traceability and accountability for changes. Example: bash CopyEdit git revert # Creates a new commit that undoes the target

---

💡 Tip: Use reset during local development. Use revert when collaborating with others.

Week 4: Git & GitHub Advanced Challenge This challenge covers advanced Git concepts essential for real-world DevOps workflows. By the end of this challenge, you will: • Understand how to work with Pull Requests effectively. • Learn to undo changes using Reset & Revert. • Use Stashing to manage uncommitted work. • Apply Cherry-picking for selective commits. • Keep a clean commit history using Rebasing. • Learn industry-standard Branching Strategies. Topics Covered

1. Pull Requests – Collaborating in teams.
    
2. Reset & Revert – Undo changes safely.
    
3. Stashing – Saving work temporarily.
    
4. Cherry-picking – Selecting specific commits.
    
5. Rebasing – Maintaining a clean history.
    
6. Branching Strategies – Industry best practices. Challenge Tasks Task 1: Working with Pull Requests (PRs) Scenario: You are working on a new feature and need to merge your changes into the main branch using a Pull Request.
    
7. Fork a repository and clone it locally.
    
8. git clone cd
    
9. Create a feature branch and make changes.
    
10. git checkout -b feature-branch
    
11. echo "New Feature" &gt;&gt; feature.txt
    
12. git add . git commit -m "Added a new feature"
    
13. Push the changes and create a Pull Request. git push origin feature-branch
    
14. Open a PR on GitHub, request a review, and merge it once approved.
    

Steps :- • Open your GitHub profile. • Navigate to the repository and lick “Compare & Pull Request”

• Select the base branch where you want to merge and select from which branch you want to merge. • Then create pull request.

• Once click on the Create pull request.

• You need to add the Description also you can ask your senior or colleague to review the pull request and the file that you have created. • Once you have assigned the reviewers and the description, then you can create pull request.

• As you can see in the screenshot there is no reviewers in it but assume you have assigned the reviewer and they have reviewed the request and approved it. • Once it is approved you can see the latest comment. • If it is mentioned that it is approved then you just need to click on merge pull request. • Then it will ask you to confirm the merge before that always put description.

• Once you click on confirm merge then pull request will be succeed.

Document in [solution.md](http://solution.md) • Steps to create a PR. • Best practices for writing PR descriptions. • Handling review comments. 🛠️ Pull Request (PR) Workflow Guide ✅ Steps to Create a Pull Request (PR)

1. Create a Feature Branch
    

git checkout -b feature/your-feature-name 2. Make Changes and Commit git add . git commit -m "Add a meaningful commit message" 3. Push the Feature Branch git push origin feature/your-feature-name 4. Open a Pull Request on GitHub o Navigate to the repository. o Click "Compare & Pull Request". o Choose the base branch (e.g., main or develop) and your feature branch. o Add a title and description, then click "Create Pull Request".

---

✍️ Best Practices for Writing PR Descriptions Clear communication in PRs improves collaboration and code quality. Structure your description like this: 🔍 What does this PR do? Brief summary of the change. E.g., "Implements login functionality using JWT." 📋 Changes made • Added authService.ts for token generation. • Updated login API to validate credentials. • Added unit tests. ✅ Checklist • Code is linted • Unit tests added • No breaking changes 📝 Related Issue Closes #123 or Fixes bug described in \[link\]

---

💬 Handling Review Comments

1. Stay open to feedback Reviews are about the code, not you.
    
2. Reply to each comment Acknowledge the feedback. Use: o ✅ Fixed o 🤔 Need clarification o 🚫 Won’t fix (with reason)
    
3. Make necessary changes Update your branch with changes and push again: git add . git commit -m "Refactor: address review feedback" git push origin feature/your-feature-name
    
4. Resolve comments on GitHub Mark them as "Resolved" once handled.
    

Task 2: Undoing Changes – Reset & Revert Scenario: You accidentally committed incorrect changes and need to undo them.

1. Create and modify a file.
    
2. echo "Wrong code" &gt;&gt; wrong.txt
    
3. git add .
    

git commit -m "Committed by mistake"

4. Soft Reset (keeps changes staged). git reset --soft HEAD~1:- it will untrack and stag the file last committed file.
    
5. Mixed Reset (unstages changes but keeps files). git reset --mixed HEAD~1 :- it will untrack the file last committed file.
    
6. Hard Reset (removes all changes). git reset --hard HEAD~1 :- it will delete the file last committed file.
    

As you can see wrong file is deleted and it also not in untrack.

7. Revert a commit safely. git revert HEAD :- it will revert the last head commit. As per last command git reset –hard it will delete the committed the file(wrong file) and the log for it. Not when you do revert HEAD then it will revert the last committed file that will feature file which was committed in task 1.
    

Document in [solution.md](http://solution.md) • Differences between reset and revert. • When to use each method.

🔁 Differences Between git reset and git revert 🧠 Conceptual Difference Feature git reset git revert What it does Moves the branch pointer to an earlier commit Creates a new commit that undoes a previous one Affects history Rewrites commit history Preserves history Safe for shared branches ❌ No (can cause issues for others) ✅ Yes (safe for collaboration) Undo visibility Changes are not visible to others (unless pushed with --force) Revert is visible as a new commit

---

🧪 When to Use Each Method ✅ Use git reset when: • You're working locally, and • You want to undo commits or unstage files without keeping the history. • Useful during development or practice. Example: bash CopyEdit git reset --soft HEAD~1 # Undo commit but keep changes staged git reset --mixed HEAD~1 # Undo commit and unstage changes git reset --hard HEAD~1 # Undo commit and discard changes (use with caution!) ✅ Use git revert when: • You're working on a shared branch (e.g., main, develop) • You want to safely undo a specific commit while keeping the history. • You need traceability and accountability for changes. Example: bash CopyEdit git revert # Creates a new commit that undoes the target

---

💡 Tip: Use reset during local development. Use revert when collaborating with others.

🔧 Task 3: Stashing - Save Work Without Committing Scenario: I was working on a file (temp.txt) but had to switch branches. The catch? I didn’t want to commit half-done work. That’s where git stash saved the day. ✅ Steps Performed: bash CopyEdit echo "Temporary Change" &gt;&gt; temp.txt git add temp.txt git stash git checkout main git stash pop 🧠 What I Learned: • When to use git stash: Use it when you want to temporarily save changes that aren't ready to be committed — especially useful when you need to switch branches quickly. • git stash pop vs git stash apply: o git stash pop: Applies the most recent stash and deletes it from the stash list. o git stash apply: Applies the stash but keeps it in the list in case you need it again. 📸 Screenshot of stash in action:

---

🍒 Task 4: Cherry-Picking - Selectively Apply Commits Scenario: I had a bug fix committed in another branch. Instead of merging the whole branch, I used cherry-pick to bring over just that fix. ✅ Steps Performed: bash CopyEdit git log --oneline git cherry-pick

# In case of conflicts:

git cherry-pick --continue 🧠 What I Learned: • Use case in bug fixes: Cherry-picking is perfect for quickly applying bug fixes or patches from one branch to another without merging unrelated work. • Risks of cherry-picking: o Can create duplicate commits if misused. o Might cause confusion in commit history if not documented properly. 📸 Screenshot of cherry-pick execution:

![image](https://github.com/user-attachments/assets/8e7b0783-e355-4f5e-bf64-aaba8e4be53a align="left")

---

🔄 Task 5: Rebasing - Keeping a Clean Commit History Scenario: My feature-branch was behind main. Instead of using a merge (which creates extra commits), I opted for rebase to keep the history clean. ✅ Steps Performed: bash CopyEdit git fetch origin main git rebase origin/main

# Resolve any conflicts:

git rebase --continue 🧠 What I Learned: • Merge vs Rebase: o Merge: Brings all commits together but creates a merge commit. o Rebase: Rewrites your local commits on top of the latest main — much cleaner history. • Best Practices: o Always rebase local branches before opening a PR. o Avoid rebasing shared/public branches to prevent history rewrite issues. 📸 Screenshot of rebase process:

![image](https://github.com/user-attachments/assets/367182ae-463b-401b-845c-d4b7327f098c align="left")

---

🚀 Final Thoughts These advanced Git tools — stashing, cherry-picking, and rebasing — are game changers for maintaining productivity and code hygiene in collaborative environments. Practicing them during this challenge has given me deeper confidence in handling real-world Git workflows.