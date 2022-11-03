# Cyberpatriot Linux Checklist
This is a checklist to go over when competing in Cyberpatriot competitions with the linux image.
## Notes Before Reading
I will put variables in commands in the $variable bash notation, but I will explain what each of them is prior to displaying the command. To edit files, I use the following, where $file is the file to edit:
```
sudo nano $file
```
To view files, I use the following, where $file is the file to edit:
```
sudo cat $file
```
If you have any problems or wish to add something, feel free to start a thread in the Issues tab.
## ALWAYS READ THE README
Seriously though. The readme might just be the most important file in the image. It tells you everything you need to know about the system to get a perfect score.
## Forensics Questions
Do the forensics questions before anything else. If you do something to the system before you answer the questions, you might accidentally remove something you needed for the questions, and you will have to restart to answer them. And you probably don't want that. The files tell you exactly how to submit the answer, so don't sweat it. They are usually something to do with permissions in linux, so make sure you are thoroughly familiar with that.
## Users
This is one of the best things you can do to get early points.
### Check the README
The readme tells you what users are allowed, the admins, and the admins' passwords, so it is very important to go through them with a fine-tooth comb.
### List Non-System Users
This is very easy to do. The commands may look complicated, but they are rather simple. To see all non-system users, execute this:
```
awk -F: '($3>=1000)&&($3<60000)&&($1!="nobody"){print $1}' /etc/passwd
```
(Courtesy of Nick ODell on StackOverflow)
What this does is look through /etc/passwd which contains all the users on the system, and filters out users with a GID (Group Identification) >1000 but <60000, because those users will not be system-created.
### Delete Unauthorized Users
Look through the list of users the previous command generated, and cross-check it with the list of authorized users in the readme. If you see a user in the generated list that is not in the readme, best practice is to just delete it entirely. Use this command to do so, where $username is the name of the user you want to delete:
```
sudo userdel $username
```
### Group Management
Sometimes the readme wants you to make a new group and add users to it, or delete a group. To make a new group, use this command, where $group is the name of the new group:
```
sudo groupadd $group
```
To add users to a group, use this command, where $group is the name of the group to add to and $user is the name of the user to add:
```
sudo usermod -a -G $group $user
```
Just to make this clear, deleting a group does NOT delete the user within in. It simply deletes the group, whereas the users are unaffected. To delete a group, use this command, where $group is the group to be deleted:
```
sudo groupdel $group
```
To remove a user from a group, use this command, where $user is the name of the user to remove and $group is the group to remove from:
```
sudo gpasswd --delete $user $group
```
(Courtesy of tshepang on StackExchange)
### Change Passwords
The passwords of admin users are listed in the readme, but they are not always secure right off the bat. Best practice is to have passwords be at least 10 characters long, with at least 1 special character and 1 number. To change the password of a user, use this command, where $user is the name of the user to change the password of:
```
sudo passwd $user
```
The command will have you enter the password into a fingerprint (a text input where you can't see what is being typed) twice for verification.
### Blank Passwords
Some users that aren't admins do not have passwords, and you have to set them yourself. To test an account and see if it has a passwd set, use this command, where $user is the name of the user to test:
```
sudo passwd -S $user | grep NP
```
If the user has a password set, it will output nothing, but if it doesn't have a password set, it will output something like this:
```
$user NP XXXX-XX-XX X XX XX X
````
and NP will be highlighted.
### Password Policies
Password policies are very important and will almost always supply points in any round. The policies are minimum and maximum days between changing passwords, and warning days for password changes. They are found in the /etc/login.defs file, and it is very straightforward on how to change it. Make sure you save the file so it looks like this:
```
PASS_MIN_DAYS 7
PASS_MAX_DAYS 90
PASS_WARN_AGE 14
```
These are generally the best password policies to use in Cyberpatriot competitions.
## Checking for Hacker Stuffs
I can't really give you a definite list of hacker things to look out for, but I will list some things I have seen in the past:
  Deluge
  Postfix
  Hydra
  Nmap
  Wireshark
These are all things you should probably delete on sight, unless told otherwise. Generally, if you do not know what something is, google it, then determine what to do with it. I like going to the root /home directory and running a recursive ls command to look through the home directories of all the users. This command does a recursive listing of all files in the cwd and down:
```
sudo ls -Ra *
```
### Services
Services can sometimes be a little hard to figure out because something that looks completely innocent could be malicious, and vice versa. To see all active services, use this command:
```
sudo service --status-all
```
If you find a service that you think to be malicious or untrustworthy, disable it right away using this command, where $service is the name of the service to disable:
```
sudo systemctl disable $service
```
## Packages
Some packages can also be malicious or untrustworthy. To see a list of all installed packages on the system, which you probably don't want to do because it is very long, use this command:
```
sudo apt list --installed
```
This is not recommended because, just in the ubuntu image I was testing these commands on, there were 1,701 packages installed. That is a lot to go through.


For more items, look at swcta_checklist.md and https://github.com/Forty-Bot/linux-checklist
