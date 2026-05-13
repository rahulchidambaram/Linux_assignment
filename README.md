# Linux Administration & Bash Scripting Assignment

A hands-on DevOps practice repository covering Linux administration, Bash scripting, file permissions, user management, and networking fundamentals.

---

# 📂 Project Structure

```bash
/home/ec2-user/webapp/
│
├── scripts/
│   └── log_user.sh
│
├── logs/
│   └── app.log
│
└── config/
    └── app.conf
```

---

 ## Question 1: Set Up Your DevOps Project Structure
 ### Objective: Create a complete project directory from scratch, apply correct permissions, and set ownership. The structure you build here will be used directly by your script in Question 2.

🔸Create all directories at once: mkdir -p /home/ec2-user/webapp/scripts /home/ec2-user/webapp/logs /home/ec2-user/webapp/config
```
mkdir -p /home/ec2-user/webapp/{scripts,logs,config}
```

🔸Create app.conf with content: cat > /home/ec2-user/webapp/config/app.conf  (type content, then Ctrl+D)
```
cat > /home/ec2-user/webapp/config/app.conf
APP_NAME=WebApp
PORT=8080
```

🔸Create empty log file: touch /home/ec2-user/webapp/logs/app.log
```
touch /home/ec2-user/webapp/logs/app.log
ls -l /home/ec2-user/webapp/logs/app.log
```

🔸Set permissions: chmod 755 /home/ec2-user/webapp/scripts  &&  chmod 644 /home/ec2-user/webapp/config/app.conf
```
chmod 755 /home/ec2-user/webapp/scripts
chmod 644 /home/ec2-user/webapp/config/app.conf
```

### Permission Explanation

**Read - 4 | Write - 2 | eXecute - 1**

The command `chmod 755 /home/ec2-user/webapp/scripts` gives the **owner** full permissions (read, write, and execute) on the `scripts` directory, while the **group members and others** are allowed only to read and execute the directory contents. This permission is commonly used for directories and executable scripts.

The command `chmod 644 config/app.conf` gives the **owner** read and write permissions on the `app.conf` file, while the **group members and others** are given read-only access. This is commonly used for configuration and text files where modification should only be allowed by the owner.

🔸Change ownership recursively: sudo chown -R root:root /home/ec2-user/webapp/
```
sudo chown -R root:root /home/ec2-user/webapp/
```


🔸Verify the full structure: ls -lR /home/ec2-user/webapp/
```
ls -lR /home/ec2-user/webapp/
```
## Output

 <img width="771" height="607" alt="Op1" src="https://github.com/user-attachments/assets/a25f5704-1e53-420a-b671-6581d5452055" />
<img width="777" height="377" alt="op1 1" src="https://github.com/user-attachments/assets/1f08c7bf-3342-4aa7-863b-56b0111fb707" />

---

## Question 2: Write an Interactive Log Script
### Objective: Using the webapp/ structure from Question 1, write a bash script that takes user input, reads a config file, and writes timestamped log entries. The log entries you create here will be the input for Question 3.

🔸Create a new script file at /home/ec2-user/webapp/scripts/log_user.sh using vim. Start with the correct shebang line. Use read -p to prompt the user to enter their name and store it in a variable called username. Use cat with the absolute path to display the contents of config/app.conf to the screen. Append a log entry to logs/app.log using echo >> in this exact format: Login: $username Date: $(date). Then display the full log file contents.
```
# Navigate to scripts directory
cd /home/ec2-user/webapp/scripts/
vim log_user.sh

# Add the below script in the log_user.sh file
#!/bin/bash

read -p "Enter your name: " username

cat /home/ec2-user/webapp/config/app.conf

echo "Login: $username Date: $(date)" >> /home/ec2-user/webapp/logs/app.log

cat /home/ec2-user/webapp/logs/app.log
```
Hit **Esc + :wq** to save

🔸Give the script execute permission with chmod +x and run it at least 3 times using different names (e.g., Chirag, Priya, Ravi) so the log file has multiple entries for Question 3.

```
chmod +x log_user.sh
#Run the script using 3 different username
./log_user.sh

# Verify log file
cat /home/ec2-user/webapp/logs/app.log
```
## Output

<img width="778" height="527" alt="op2_bash" src="https://github.com/user-attachments/assets/840c55df-6f62-4f41-a6a3-7071061584eb" />
<img width="768" height="492" alt="OP2 1" src="https://github.com/user-attachments/assets/7fa544e8-f473-433a-81ad-19bec34e0ac6" />

---

## Question 3: User Management and File Permission Control
### Objective: Create 4 Linux users. Two of them must have write access to the log_user.sh script created in Question 2, and the other two must have read-only access. Use Linux groups and chmod to control this.

🔸Create a group called writers:
```
sudo groupadd writers
```

🔸Create 4 users with home directories:
```
sudo useradd -m devuser1
sudo useradd -m devuser2
sudo useradd -m devuser3
sudo useradd -m devuser4
```

🔸Add the two write-access users to the writers group:
```
sudo usermod -aG writers devuser1
sudo usermod -aG writers devuser2
```

🔸Change the group ownership of log_user.sh to writers: 
```
sudo chown root:writers /home/ec2-user/webapp/scripts/log_user.sh
```

🔸Set permissions to 664 so writers group gets rw and others get r only: 
```
sudo chmod 664 /home/ec2-user/webapp/scripts/log_user.sh
```

🔸Verify the permission output shows: -rw-rw-r--  root  writers  log_user.sh
```
ls -l /home/ec2-user/webapp/scripts/log_user.sh
```

🔸Switch to each user and test access to confirm it is working correctly:

```
su - devuser1
echo 'test' >> /home/ec2-user/webapp/scripts/log_user.sh

su - devuser3
cat /home/ec2-user/webapp/scripts/log_user.sh

# Attempt write access
echo 'test' >> /home/ec2-user/webapp/scripts/log_user.sh
```

## Output

<img width="777" height="522" alt="OP3" src="https://github.com/user-attachments/assets/f7e1fc78-285a-49bf-8e7a-37c9f8ca4ba8" />
<img width="778" height="328" alt="Op3 1" src="https://github.com/user-attachments/assets/1a10945f-4a05-4fb9-bde6-e498abd4e1cb" />

---






