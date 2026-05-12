

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

🔸Change ownership recursively: sudo chown -R root:root /home/ec2-user/webapp/
```
sudo chown -R root:root /home/ec2-user/webapp/
```


🔸Verify the full structure: ls -lR /home/ec2-user/webapp/
```
ls -lR /home/ec2-user/webapp/
```
## Output


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

## Question 3: User Management and File Permission Control
### Objective: Create 4 Linux users. Two of them must have write access to the log_user.sh script created in Question 2, and the other two must have read-only access. Use Linux groups and chmod to control this.

```
sudo groupadd writers
```

```
sudo useradd -m devuser1
sudo useradd -m devuser2
sudo useradd -m devuser3
sudo useradd -m devuser4
```

```
sudo usermod -aG writers devuser1
sudo usermod -aG writers devuser2
```

```
sudo chown root:writers /home/ec2-user/webapp/scripts/log_user.sh
sudo chmod 664 /home/ec2-user/webapp/scripts/log_user.sh
ls -l /home/ec2-user/webapp/scripts/log_user.sh
```


```
su - devuser1
echo 'test' >> /home/ec2-user/webapp/scripts/log_user.sh

su - devuser3
cat /home/ec2-user/webapp/scripts/log_user.sh

# Attempt write access
echo 'test' >> /home/ec2-user/webapp/scripts/log_user.sh
```
