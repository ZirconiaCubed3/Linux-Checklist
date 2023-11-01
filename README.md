For more items, look at https://github.com/Forty-Bot/linux-checklist

# Do Forensics Questions
# Remove Unauthorized Users
```sudo userdel $user```
# Remove Users from Sudo Group
```sudo usermod -G $group $user```
# Add Users to Groups According to README
```sudo usermod -a -G $group $user```
# Create New Users According to README
```sudo adduser $user```
# Password Rules
## Edit /etc/login.defs and add to the bottom:
```
PASS_MIN_DAYS 7
PASS_MAX_DAYS 90
PASS_WARN_AGE 14
```
# Enable UFW
```sudo ufw enable```
# Remove Rogue Services
```sudo service --status-all```
```sudo systemctl disable $service```
# Enable Automatic Updates (Daily)
```sudo apt install unattended-upgrades```
# Update Systemd
```sudo apt upgrade systemd```
# Update OpenSSH if README requires it
```sudo apt upgrade openssh```
# Look for txt files in home directories
```sudo find /home -name '*.txt'```
# Look for mp3 files in home directories
```sudo find /home -name '*.mp3'```
# Look for image files in home directories
```sudo find /home -name '*.jpg'; sudo find /home -name '*.jpeg'; sudo find /home -name '*.png'```
# Remove hacker stuffs
```sudo apt purge wireshark* ophcrack* john* deluge* nmap* hydra*```
# Disable SSH root login
## Edit /etc/ssh/sshd_config
## Replace:
```PermitRootLogin yes```
## With:
```PermitRootLogin no```


# Somewhat Useful Snippets:
## List all files in a directories and its subdirectories:
```sudo ls -Ra *```
## Check for blank passwords:
```sudo passwd -S $user | grep NP```
## List non-system users:
```awk -F: '($3>=1000)&&($3<60000)&&($1!="nobody"){print $1}' /etc/passwd```
## Check Ports:
```sudo ss -ln```
## Close a Port:
```sudo lsof -i :$port```
## Find Where a Program is Located:
```whereis $program```
## Enable Cookie Protection:
```sudo sysctl -n net.ipv4.tcp_syncookies```
