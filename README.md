# linux-demo
demo project

# Level 1 – Basic (Foundational Skills)

- Set up users, groups for devops team

```bash
sudo useradd rakesh23
sudo passwd rakesh23
sudo groupadd devopsteam
sudo usermod -aG devopsteam rakesh23
```
![alt text](Evidance/Capture.PNG)

- Manage permissions for project directories

``` bash
sudo mkdir /opt/linux-projectA
sudo chown root:devopsteam /opt/linux-projectA
sudo chmod 770 /opt/linux-projectA
```
![alt text](image.png)

- Install required packages (Git, Nginx, Java)

``` bash
sudo yum install git  -y
sudo yum install nginx -y 
sudo yum install java-17 -y

sudo systemctl enable --now nginx
```
![alt text](image-2.png)

![alt text](image-3.png)

![alt text](image-4.png)

![alt text](image-6.png)

- Check system info (Memory, CPU, Disks)

``` bash
free -h
top
lsblk
df -h
uname -a
htop
```
![alt text](Evidance/1-4.PNG)

![alt text](Evidance/1-4b.PNG)

![alt text](Evidance/1-4c.PNG)

![alt text](Evidance/1-4d.PNG)

![alt text](Evidance/1-4e.PNG)

![alt text](Evidance/1-4f.PNG)

![alt text](Evidance/1-4g.PNG)

## Level 2 – Intermediate (Daily DevOps Tasks)

- Automate backups with Cron

``` bash
crontab -e
0 2 * * * tar -czf /backup/html-$(date +\%F).tar.gz /var/www/html
```
![alt text](Evidance/2-1.PNG)

![alt text](Evidance/2-1a.PNG)

![alt text](Evidance/2-1b.PNG)

- Create shell scripts: Log cleanup

``` bash 
#!/bin/bash
find /var/log -type f -mtime +7 -delete
```
![alt text](Evidance/2-2.PNG)

service restart

``` bash 
#!/bin/bash
systemctl restart nginx
```
![alt text](Evidance/2-2a.PNG)

![alt text](Evidance/2-2aa.PNG)

 health checks

```bash
#!/bin/bash
curl -I http://localhost | grep "200 OK"
```
![alt text](Evidance/2-2b.PNG)

- Manage logs under /var/log

``` bash
cd /var/log
tail -f messages
tail -f secure
journalctl -u nginx
```
![alt text](Evidance/2-3.PNG)

![alt text](Evidance/2-3aa.PNG)

- Monitor system performance and troubleshoot services

``` bash 
top
vmstat 1
iostat
systemctl status nginx
journalctl -xe
```
![alt text](Evidance/2-4.PNG)

![alt text](Evidance/2-4b.PNG)

![alt text](Evidance/2-4c.PNG)

![alt text](Evidance/2-4d.PNG)

![alt text](Evidance/2-4e.PNG)

## Level 3 – Advanced (Production-Ready Linux Admin)

- Create custom systemd service for your application

``` bash 
[Unit]
Description=My Node App
After=network.target

[Service]
ExecStart=/usr/bin/node /opt/app/server.js
Restart=always
User=ec2-user

[Install]
WantedBy=multi-user.target
#### Enable it:

sudo systemctl daemon-reload
sudo systemctl enable --now myapp
```
![alt text](Evidance/3-a.PNG)

![alt text](Evidance/3-b.PNG)

![alt text](Evidance/3-c.PNG)

- SSH hardening for security

``` bash 
PermitRootLogin no
PasswordAuthentication no
AllowUsers rakesh23
Then :
sudo systemctl restart sshd
```
![alt text](Evidance/3-2a.PNG)

![alt text](Evidance/3-2b.PNG)

![alt text](Evidance/3-2c.PNG)

- LVM setup for storage scaling

``` bash
pvcreate /dev/xvdb
vgcreate appvg /dev/xvdb
lvcreate -L 10G -n applv appvg
mkfs.xfs /dev/appvg/applv
mount /dev/appvg/applv /opt/app
```
![alt text](Evidance/3-3a.PNG)

![alt text](Evidance/3-3b.PNG)

![alt text](Evidance/3-3c.PNG)

- Configure firewall rules

``` bash
For Firewalld:
sudo firewall-cmd --add-port=80/tcp --permanent
sudo firewall-cmd --reload
For UFW:
sudo ufw allow 80/tcp
sudo ufw enable
```
![alt text](Evidance/3-4a.PNG)

![alt text](Evidance/3-4b.PNG)

![alt text](Evidance/3-4c.PNG)

- Implement logrotate for app logs

``` bash
/var/log/myapp/*.log {
    daily
    rotate 7
    compress
    missingok
    notifempty
}
```
![alt text](Evidance/3-5a.PNG)

![alt text](Evidance/3-5b.PNG)

![alt text](Evidance/3-5c.PNG)