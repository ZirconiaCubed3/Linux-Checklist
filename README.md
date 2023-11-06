For more items, look at https://github.com/Forty-Bot/linux-checklist

<details open>
<summary><h2>Remove Unauthorized Users</h2></summary>
<br>
<pre>sudo userdel $user</pre>
Be careful, if you delete a user that is authorized, you can't get points back by re-creating it
</details>

<details open>
<summary><h2>Remove Users from Sudo Group</h2></summary>
<br>
<pre>sudo deluser $user $group</pre>
</details>

<details open>
<summary><h2>Add Users to Groups According to README</h2></summary>
<br>
<pre>sudo usermod -a -G $group $user</pre>
</details>

<details open>
<summary><h2>Create New Users According to README</h2></summary>
<br>
<pre>sudo adduser $user</pre>
</details>

<details open>
<summary><h2>Password Rules</h2></summary>
Edit /etc/login.defs and add to the bottom:
<pre>
PASS_MIN_DAYS 7
PASS_MAX_DAYS 90
PASS_WARN_AGE 14
</pre>
</details>

<details open>
<summary><h2>Enable UFW</h2></summary>
<br>
<pre>sudo ufw enable</pre>
</details>

<details open>
<summary><h2>Remove Rogue Services</h2></summary>
<br>
<pre>sudo service --status-all</pre>
<pre>sudo systemctl disable $service</pre>
</details>


<details open>
<summary><h2>Enable Automatic Updates (Daily)</h2></summary>
<br>
<pre>sudo apt install unattended-upgrades</pre>
</details>

<details open>
<summary><h2>Update Systemd</h2></summary>
<br>
<pre>sudo apt upgrade systemd</pre>
</details>

<details open>
<summary><h2>Update OpenSSH if README requires it</h2></summary>
<br>
<pre>sudo apt upgrade openssh</pre>
</details>

<details open>
<summary><h2>Look for txt files in home directories</h2></summary>
<br>
<pre>sudo find /home -name '*.txt'</pre>
</details>

<details open>
<summary><h2>Look for mp3 files in home directories</h2></summary>
<br>
<pre>sudo find /home -name '*.mp3'</pre>
</details>

<details open>
<summary><h2>Look for image files in home directories</h2></summary>
<br>
<pre>sudo find /home -name '*.jpg'; sudo find /home -name '*.jpeg'; sudo find /home -name '*.png'</pre>
</details>

<details open>
<summary><h2>Remove hacker stuffs</h2></summary>
<br>
<pre>sudo apt purge wireshark* ophcrack* john* deluge* nmap* hydra*</pre>
</details>

<details open>
<summary><h2>Disable SSH root login</h2></summary>
<h3>Edit /etc/ssh/sshd_config</h3>
<h3>Replace:</h3>
<pre>PermitRootLogin yes</pre>
<h3>With:</h3>
<pre>PermitRootLogin no</pre>
</details>

<details open>
<summary><h1>Somewhat Useful Snippets:</h1></summary>

<h2>List all files in a directories and its subdirectories:</h2>
<pre>sudo ls -Ra *</pre>

<h2>Check for blank passwords:</h2>
<pre>sudo passwd -S $user | grep NP</pre>

<h2>List non-system users:</h2>
<pre>awk -F: '($3>=1000)&&($3<60000)&&($1!="nobody"){print $1}' /etc/passwd</pre>

<h2>Check Ports:</h2>
<pre>sudo ss -ln</pre>

<h2>Close a Port:</h2>
<pre>sudo lsof -i :$port</pre>

<h2>Find Where a Program is Located:</h2>
<pre>whereis $program</pre>

<h2>Enable Cookie Protection:</h2>
<pre>sudo sysctl -n net.ipv4.tcp_syncookies</pre>
</details>
