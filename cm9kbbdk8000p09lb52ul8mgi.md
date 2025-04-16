---
title: "Bash Scripting for Real-Life Tasks (User Management & Backups)"
datePublished: Wed Apr 16 2025 19:16:21 GMT+0000 (Coordinated Universal Time)
cuid: cm9kbbdk8000p09lb52ul8mgi
slug: bash-scripting-for-real-life-tasks-user-management-and-backups
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1744741429244/4d597d6a-76ae-4a49-aa8c-ad1a27d42e27.png
tags: shell-script, usermanagement, rotation-backup

---

Bash scripting might sound intimidating — like something only seasoned system admins do while sipping coffee in dark rooms. But here's the truth: **you can totally learn it**. And in this Week 3 challenge, we’re applying Bash to **real-world problems** that even non-tech folks can appreciate.

Let’s break it down in plain English.

---

## 🔐 Challenge 1: User Account Management Script

Imagine you’re in charge of who gets to enter a building, who can stay, who should leave, and how to change their key. That’s basically what we’re doing here — but in Linux.

We’re building a **user-friendly Bash script** that helps you **create, delete, reset passwords, and list users** on your system.

### 🛠️ What Will This Script Do?

It will give you different options via the command line. You just run the script and pick what you want to do:

### 1\. ✅ Create a New User

Use the option:

```plaintext
#First, we have to create a shell script 
vim user_management.sh

# After creating the shell script, we will create function for create user
function create_user {

echo "================Creation of the user================"

read -p " enter the username that you wish to create: " username

# id cmd will filter out the username if it is already there then it come out 1 and if user is not there then outcome will be 0

id=$(cat /etc/passwd | grep "$username" | wc | awk '{print $1}' )

# if else statment the check the outcome of id variable if it is 0 then it will create the user and if it 1 then it will show that user is already there
#
if [ $id == 0 ];
then
        sudo useradd -m "$username"

read -p "enter the password: " password

echo -e "$password\n$password" | sudo passwd "$username"

else
        echo " user already exist "
fi


}
```

* It asks for the new username and password.
    
* It checks if the username is already taken.
    
* If not, it creates the user and shows a success message.
    

### 2\. ❌ Delete a User

Use:

```plaintext
function delete_user {

echo " =========== Account deleletion ========="

read -p "enter the user you wish to delete: " username

id=$(cat /etc/passwd | grep "$username" | wc | awk '{print $1}')

if [ $id != 0 ];
then
        sudo userdel -r "$username"
echo " $username has been deleted "
else
        echo "user do not exist"
fi


}
```

* You enter the username you want to delete.
    
* It confirms if the user exists.
    
* Then it deletes them and confirms it’s done.
    

### 3\. 🔁 Reset a User’s Password

Use:

```plaintext
function password_reset {

echo " ============= Password Reset =========== "

read -p " please enter the username to reset the password : " username

id=$(cat /etc/passwd | grep "$username" | wc | awk '{print $1}')

if [ $id != 0 ];

then 
        read -p " enter the new password : " password
        echo -e "$password\n$password" | sudo passwd "$username"
else
        echo " user does not exist"
fi
}
```

* Enter the username and a new password.
    
* If the user exists, the password gets updated and a message confirms it.
    

### 4\. 📋 List All Users

Use:

```plaintext
function list_user {

echo " ============ listing the users ================="

cat /etc/passwd 

}
```

* This one displays all the users on your system along with their unique user IDs.
    

### 5\. ℹ️ Help & Usage Info

Confused? Just use:

```plaintext
echo "Enter -c or --create to Create a new User"

echo "Enter -d or --delete to Delete the User"

echo "Enter -r or --reset to Reset the password"

echo "Enter -l or --list to Display the Users."



read -p " Enter your option " option

case "$option" in

        -c | --create)
        echo "You choose the option to create user "
        create_user;;

-d |--delete)
        echo "You choose the option to delete user "
        delete_user;;

-r | --reset)
        echo "You choose the option to reset the password "
        password_reset;;

-l | --list)
        echo "You choose the option to list user "
        list_user;;

esac
```

* It shows you all the available options so you’re never stuck.
    

To Run the shell script

```plaintext
./user_management.sh
```

It will show the results like below

```plaintext
ubuntu@ip-172-31-43-133:~/week3_task$ ./user_management.sh 
Enter -c or --create to Create a new User
Enter -d or --delete to Delete the User
Enter -r or --reset to Reset the password
Enter -l or --list to Display the Users.
```

---

## 💾 Challenge 2: Automated Backup & Recovery Using Cron

Now for the second part of the challenge — this one is all about **backing up your files** automatically and keeping things clean with a rotation system.

### 📦 What's the Goal?

We’re creating a script that:

1. Takes a directory as input.
    
2. Creates a timestamped backup folder.
    
3. Copies all files into it.
    
4. Deletes old backups — only keeping the last **3 most recent**.
    

> Think of it like taking 3 snapshots of your room and throwing out the oldest every time you take a new one.

### Shell Script for rotational backup

```plaintext
#!/bin/bash

<<info 
        this is backup sheel script which will backup the file in roation
It will contain only last 3 backups

info

# path of the files 

src="/home/ubuntu/devops_workspace"
dest="/home/ubuntu/documents"

# Number of backup copies to retain 

num_backup_to_keep=3

# date format for backup file

date=$(date '+%Y-%m-%d-%H-%M-%S')

# perform the backup

zip -r "$dest/backup_$date.zip" $src

echo " backup done "

# remove old backup exceeding the specified limit

num_backup=$(ls -l "$dest" | grep -c "backup")

num_backup_to_remove=$((num_backup - num_backup_to_keep))

if [ $num_backup_to_remove > 0 ]; then
        # List old backup, sort by timestamp, and remove the excess
        old_backup=$(ls -l "$dest" | grep "backup" | sort | head -n $num_backup_to_remove)

        for old_backup in $old_backup; do
                rm "$dest/$old_backup"
                echo "Removed old Back : $old_backup"
        done
fi
                                                                                                                                                                       1,8           Top
```

Cron job for Shell script

it will take backup after each 1 minute

```plaintext
*/1 * * * * bash /home/ubuntu/devops_workspace/backup_with_rotation.sh
```

---

### 🔁 Why Rotation?

Backups are great… until they take up all your storage. The rotation system ensures you always have the latest versions — **without clutter**.

---

## 🧑‍🏫 Final Words

Even if you’re a complete beginner, these tasks are super doable. Start simple, understand what each part of the script is doing, and you’ll feel more confident each week.

> 💡 Pro Tip: Add comments to your scripts. It’s like leaving notes for your future self (or your teammates) to understand what’s going on.

Happy scripting! Bash might look boring on the outside, but trust me — it’s powerful under the hood.