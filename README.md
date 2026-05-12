

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

## Question 2: Write an Interactive Log Script
### Objective: Using the webapp/ structure from Question 1, write a bash script that takes user input, reads a config file, and writes timestamped log entries. The log entries you create here will be the input for Question 3.

