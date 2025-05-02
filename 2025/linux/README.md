# Week 2: Linux System Administration & Automation

Welcome to **Week 2** of the **90 Days of DevOps - 2025 Edition**! This week, we dive into **Linux system administration and automation**, covering essential topics such as **user management, file permissions, log analysis, process control, volume mounts, and shell scripting**.

---

## 🚀 Project: DevOps Linux Server Monitoring & Automation
Imagine you're managing a **Linux-based production server** and need to ensure that **users, logs, and processes** are well-managed. You will perform real-world tasks such as **log analysis, volume management, and automation** to enhance your DevOps skills.

---

## 📌 Tasks

### **1️⃣ User & Group Management**
- Learn about Linux **users, groups, and permissions** (`/etc/passwd`, `/etc/group`).
- **Task:**  
  - Create a user `devops_user` and add them to a group `devops_team`.
  - Set a password and grant **sudo** access.
  - Restrict SSH login for certain users in `/etc/ssh/sshd_config`.

---
-sudo adduser devops_user

-sudo groupadd devops_team
-sudo usermod -aG devops_team devops_user 

or 
---
sudo gpasswd -a devops_user devops_team

sudo passwd devops_user

sudo usermod -aG sudo devops_user
---
or
---
sudo gpasswd -a devops_user sudo
---
sudo visudo then add line devops_user ALL=(ALL) NOPASSWD:ALL

sudo nano /etc/ssh/sshd_config
---
DenyUsers user1 user2   # Deny Blocks
---
or
---
AllowUsers devops_user admin_user  #Allow only allows
---
later restart SSH Services
---
sudo systemctl restart sshd


### **2️⃣ File & Directory Permissions**
- **Task:**  
  - Create `/devops_workspace` and a file `project_notes.txt`.
  - Set permissions:
    - **Owner can edit**, **group can read**, **others have no access**.
  - Use `ls -l` to verify permissions.

---
mkdir /devops_workspace
---
touch /devops_workspace/project_notes.txt
---
cd /devops_workspace
---
sudo chmod 740 project_notes.txt
---
ls -l -->to verify

### **3️⃣ Log File Analysis with AWK, Grep & Sed**
Logs are crucial in DevOps! You’ll analyze logs using the **Linux_2k.log** file from **LogHub** ([GitHub Repo](https://github.com/logpai/loghub/blob/master/Linux/Linux_2k.log)).

- **Task:**  
  - **Download the log file** from the repository.
  - **Extract insights using commands:**
    - Use `grep` to find all occurrences of the word **"error"**.
    - Use `awk` to extract **timestamps and log levels**.
    - Use `sed` to replace all IP addresses with **[REDACTED]** for security.
  - **Bonus:** Find the most frequent log entry using `awk` or `sort | uniq -c | sort -nr | head -10`.

---
grep -i "error" log_file.log
---
awk '/authentication failure/ {print $1,$2,$3,$9,$10,$11,$12,$13,$14}' log_file.log
---
sed -E 's/([0-9]{1,3}\.){3}[0-9]{1,3}/[REDACTED]/g' log_file.log

### **4️⃣ Volume Management & Disk Usage**
- **Task:**  
  - Create a directory `/mnt/devops_data`.
  - Mount a new volume (or loop device for local practice).
  - Verify using `df -h` and `mount | grep devops_data`.

---
mkdir /mnt/devops_data
---
mkfs -t ext4 /dev/xvdf
---
mount /dev/xvdf /mnt/devops_data


### **5️⃣ Process Management & Monitoring**
- **Task:**  
  - Start a background process (`ping google.com > ping_test.log &`).
  - Use `ps`, `top`, and `htop` to monitor it.
  - Kill the process and verify it's gone.

---
ps aux|grep ping
---
top |grep ping
---
kill pid or kill -9 pid

### **6️⃣ Automate Backups with Shell Scripting**
- **Task:**  
  - Write a shell script to back up `/devops_workspace` as `backup_$(date +%F).tar.gz`.
  - Save it in `/backups` and schedule it using `cron`.
  - Make the script display a success message in **green text** using `echo -e`.

---

## 🎯 Bonus Tasks (Optional 🚀)
1. Find the **top 5 most common log messages** in `Linux_2k.log` using `awk` and `sort`.
2. Use `find` to list **all files modified in the last 7 days**.
3. Write a script that extracts and displays only **ERROR and WARNING logs** from `Linux_2k.log`.

---
 find . -type f -mtime -7


## 📢 How to Submit
- **Write a LinkedIn post** summarizing your Week 2 experience.
- Include screenshots or logs of your tasks.
- **Use hashtags**: `#90DaysOfDevOps` `#LinuxAdmin` `#DevOps`
- Share any blog posts, GitHub repos, or articles you create.

---

## 📚 Resources to Get Started
- [Linux In One Shot](https://youtu.be/e01GGTKmtpc?si=FSVNFRwdNC0NZeba)
- [Linux_2k.log (LogHub)](https://github.com/logpai/loghub/blob/master/Linux/Linux_2k.log)

---

## 📝 Example Submission Post
```markdown
Week 2 of #90DaysOfDevOps2025 done! 🏆

✅ Managed users & SSH access  
✅ Set up permissions & volumes  
✅ Analyzed logs using AWK & grep  
✅ Automated backups with a shell script  

Check out my blog here: [Your Blog/GitHub Link]  

#Linux #SysAdmin #DevOps
```

---

Happy learning, and see you in **Week 3**! 🚀

