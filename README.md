# Born2beroot - /42 Lisboa/

## Table of contents :

- [Installing and acessing the VM](#installing-and-acessing-the-vm)
- [Starting and configuring our VM](#starting-and-configuring-our-vm)
	- [Installing sudo](#installing-sudo)
	- [Setting up SSH service](#setting-up-ssh-service)
	- [Setting up UFW](#setting-up-ufw)
	- [Setting more things up on sudo](#setting-more-things-up-on-sudo)
	- [Password policy](#password-policy)
	- [Configuring the network adapter](#configuring-the-network-adapter)
	- [Setting up cron](#setting-up-cron)
- [For the BONUS PART](#for-the-bonus-part)
- [Final touches](#final-touches)
- [Before finishing your project](#before-finishing-your-project)
- [For the evaluation](#for-the-evaluation)
- [Here's more info on the subject](#heres-more-info-on-the-subject)

## Regarding the project:

### 1. Why should I use a Virtual Machine?
	
A virtual machine is a software emulation of a computer operating system, that allows you to run on a host machine multiple OS simultaneously on the same computer. 

Since each VM has its own operating system and functions separately, you can have more than one VM per machine. They are used to test out new software without affecting your current system, in a safe, separate environment. That way we also eliminate the need for multiple physical configurations of hardware, which can be costly to maintain and take up space. 


### 2. Why did I choose Debian?

Besides being easier to install, when a new version is launched, updating Debian is much simpler compared to CentOS. Debian offers a user-friendly experience and supports a wide range of libraries, filesystems, and architecture, as well as providing more customization options. 

That means Debian is so much better when we are talking about personal servers. On the other hand, for larger businesses, CentOS provides more features and unparalleled support for Enterprise software.


### 3. What are the differences between APT and aptitude?

Both APT (Advanced Packaging Tool) and aptitude are tools for package management, used for searching, removing, and installing packages. However, they have different proposals.

Created for Debian, APT is an open-source tool that handles software installation and removal, working with the RPM Package Manager. In the command-line, it includes apt, apt-get, and apt-cache. Advanced Packaging Tool searches in a list of cached packages, listing the dependencies that need to be installed or updated; next, it can automatically download, configure, and install these dependencies. 

Using apt, you can syncronize the package file with its source (by using command update), install the most recent versions of these packages that are already installed on your system from the sources list (using command upgrade) and also, in addition to update, it can handle dependencies with new package versions (with commands full-upgrade (apt) y dist-upgrade (apt-get)).

On the other hand, aptitude is an interface created for APT that can show a list of software packages, allowing the user to choose which to install or remove. That being said, it has a more flexible manner of searching the packages, making it easier to understand dependencies between the packages. To use aptitude via command terminal, just like apt-get, the user must log in as super-user / use the sudo command.

The most important difference between one and the other, is that aptitude is a high-level package manager, while APT is a lower-level package manager. Overall, aptitude has more integrated functionalities, which includes apt-mark and apt-cache, and handles even more tasks than apt.


### 4. What is AppArmor?

AppArmor is a Linux kernel security module, that comes with Debian, that restricts applications to a limited set of resources. It provides a mandatory access control (MAC) system that allows administrators to have more control, as it is possible for them to restrict the access of certain applications to the system. 

We can scheck its status by running:
```
sudo aa-status
```

### 5. What is SSH?

"The Secure Shell (SSH) is a secure manner of connecting to a remote machine. It utilizes encryption to protect all communication between the client and the host, allowing users to access their servers more safely. This protocol is supported on Mac and Linux systems and can be accessed via the terminal. Unlike other remote communication methods, SSH encrypts the entire session, making it impossible for unauthorized parties to intercept sensitive information. By using the SSH protocol, security concerns are significantly reduced. Encryption enhances the security of both the client and server, and as a result, passwords, client access data, and any other sensitive information are protected from unauthorized access."

### 6. What is UFW?

The Uncomplicated Firewall (UFW) is a user-friendly tool for modifying the firewall settings of a device without sacrificing security. It enables you to control incoming connections by specifying which ports to open and which to block. This can be useful in combination with SSH, where you can set a specific port for it to use.

### 7. What is LVM?
The Logical Volume Manager (LVM) is a software tool that enables users to manage partitions or logical volumes on a storage device with ease. To work, LVM assigns disks to one or more physical volumes, which must be partitioned as LVM type. LVM storage volumes can be resized and relocated as needed, using the latest management tools. In a nutshell, it offers administrators with a more versatile solution to manage disk space compared to traditional partitioning in order to simplify the task of balancing the storage demands of multiple users.

### 8. What is cron?

A cron job, also known as cron, is a scheduling utility in the command line that allows commands or scripts to be executed at specified intervals or at a designated time each day. This tool is useful for tasks such as scheduling a server restart at a specific time daily.

Some of it scripts are: the "monitoring.sh" script, which is a tool that displays messages on the terminal screens of all users who are currently logged in, searching for specific values and storing them as variables for display purposes; and the "sleep.sh" script, that calculates the amount of time that the virtual machine has been powered on, allowing the "monitoring.sh" message to be displayed on the screen every 10 minutes since the system's startup.


## Installing and acessing the VM:

1. First, we need to go to the [link](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/), scroll all the way down and download the .iso file named `debian-xx.x.x-amd64-netinst.iso`;

2. Then we download and install the `Oracle VirtualBox`, if it's not already installed;

3. Start the program and open the `Virtual Machine` and clicking on `New`;

4. Next, we need to give a name to the VM (for example, `Born2beroot`), by changing the machine folder to the path: `sgoinfre/goinfre/Perso/mylogin`, and select `Debian 64 bits` on the version field;

5. Then we need to `allocate the RAM memory`, which is the amount of memory that the VM will have access to. For this VM, we will allocate `1024 MB`;

6. After that, we need to `Create a virtual hard disk`, and choose `VDI (VirtualBox Disk Image)`;

7. Next, we need to choose `Dynamically allocated`, to only use the space on our physical hard disk as we need it, filling up to a maximum size of our choice;

8. We then choose the `size of the hard disk`, the amount of space that the VM will have access to. For this, we will allocate `12 GB`;

9. After we created it, we need to choose the `location of the hard disk`, which is the folder where the VM will be stored. For this VM, we will click on `Settings` -> `Storage` -> `Controller: IDE` -> `Optical Drive`, and then `Choose a disk file...` to select the `.iso` we downloaded earlier;

10. We should then click on the `VM`, select `ok` to confirm the storage and click on the right green arrow to `Start`;

11. Inside our virtual machine, using only the keyboard, we should select (using the keys) `Install` and press `enter`;

12. Next, we need to select the `language`, which is` English`;

13. Then, we need to select the `location`, which is `Portugal`;

14. After that, we need to select the `keyboard layout`, which is `American English`;

15. Next, we need to select the `hostname`, which is "username42" (gubranco42);
```
The hostname works as an identifier of our system to the network.
```

16. Then, in the `domain name`, we leave it blank;
```
The domain name would be the internet's address, which we won't configure.
```

17. A `password` needs to be created for the `hostname` (keep it very well, as it's going to be needed further);

18. Next, we need to select the `full name` for the user, which is anyone you want;

19. Then, we need to select the `username` for the user, which is your same username used at the intra (gubranco);
```
The purpose to create a username is only for non-administrative reasons.
```

20. After that, we need to select the `password` for the user, which can be the same one used before for the hostname;

21. We need to select the `time zone`, which is `Central`;

22. Next, we need to select the `partition disks`, which we are going for `Manual`;

23. Then, we need to select the `hard disk`, which is `SCSI3`, and confirm `yes`;

24. The `partitioning scheme` is next, so we'll create 2 partitions, being the first one for an unencrypted/boot partition, and the other for encrypted logical volumes:

* `pri/log xxGB FREE SPACE` -> `Create a new partition` -> `500 MB` -> `Primary` -> `Beginning` -> `Mount point` -> `/boot` -> `Done`;
```
The boot will store the files that kernel needs in order to boot the system.
```

* `pri/log xxGB FREE SPACE` -> `Create a new partition` -> `max` -> `Logical` -> `Mount point` -> `Do not mount it` -> `Done`


25. Next, we are going to `configure the encrypted volumes`, by selecting "create encrypted volumes", and choosing (pressing space) only `dev/sda5` to encrypt (not the sda/boot)!

26. Then we need to click on `Done` -> `Finish` -> `Yes`, and wait for the formatting to complete;

27. Next, you're choosing a `strong password for disk encryption`;

28. The configuration of the `Logical Volume Manager (LVM)` in up next, and we'll start by creating a `Volume Group` -> `LVMGroup` -> `/dev/mapper/sda5_crypt`;

29. Then, the creation of logical volumes inside the Volume Group begins:

* `Create Logical Volume` -> `LVMGroup` -> `root` -> `2.8G`
```
The root is used to represent our root home directory.
```

* `Create Logical Volume` -> `LVMGroup` -> `home` -> `2G`
```
The home is used to store our personal files, such as documents, pictures, etc (all user's files).
```

* `Create Logical Volume` -> `LVMGroup` -> `swap` -> `1G`
```
The swap is used to store our memory, which is used when our RAM is full.
```

* `Create Logical Volume` -> `LVMGroup` -> `tmp` -> `2G`
```
Tmp is used to keep our temporary files, and its space is cleaned each time we reboot our system.
```

* `Create Logical Volume` -> `LVMGroup` -> `srv` -> `1.5G`
```
Srv is used to store our server files, such as databases, site-specific data, etc.
```

* `Create Logical Volume` -> `LVMGroup` -> `var` -> `2G`
```
Var is used to store our variable files, which are files that can change during the execution of the system, such as caches, backups, etc.
```

* `Create Logical Volume` -> `LVMGroup` -> `var-log` -> `2G`
```
Var-log is used to store our logs, which are files that are used to keep track of the system's activity.
```

30. We can select `Display configuration details` to double-check, and then `Finish`;

31. Next, we assign mount points for each logical volume:
	* For `LV home`, `#1 xxGB` -> `Use as` -> `Ext4` -> `Mount point` -> `/home` -> `Done`
	* For `LV root`, `#1 xxGB` -> `Use as` -> `Ext4` -> `Mount point` -> `/` -> `Done`
	* For `LV swap`, `#1 xxGB` -> `Use as` -> `swap area` -> `Done`
	* For `LV srv`, `#1 3GB` -> `Use as` -> `Ext4` -> `Mount point` -> `/srv` -> `Done`
	* For `LV tmp`, `#1 3GB` -> `Use as` -> `Ext4` -> `Mount point` -> `/tmp` -> `Done`
	* For `LV var`, `#1 3GB` -> `Use as` -> `Ext4` -> `Mount point` -> `/var` -> `Done`
	* For `LV var-log`, `#1 4GB` -> `Use as` -> `Ext4` -> `Mount point` -> `/var/log` (entered manually) -> `Done`
  
32. To be done with it, we go to `Finish partioning and write changes to disk` and select `Yes`;

33. When a option to `configure the package manager` appears, we have to select `no`;

34. A selection to our country `Portugal` is then made;

35. Next, we need to select the `mirror` to download the packages from, which is `deb.debian.org`;

36. We then select the `HTTP proxy`, which we can leave blank;

37. In `configuring popularity-contest` we should select `no` and enter;

38. Select the `software selection`, which we should uncheck all software;

39. Select `yes` by pressing enter to `install the GRUB boot loader on a hard disk`, and after that we select
`/dev/sda`;

40. Click on `continue` to finish the installation;

41. To verify that the installation was successfully completed, we can run the comands `lsblk` and `cat /etc/os-release`;

41. It is extremely important we have our host, username and password(s) written somewhere before we move on.



## Starting and configuring our VM

1. We first enter our `password` that we created for the `LVM encryption`, to unlock the disk, then into our user (gubranco);

2. Next we login as root in order to install vim;
```
su root
```

3. We then install `vim`, which is a text editor;
```
apt-get install vim -y
```



### Installing sudo:

* The term "sudo" stands for "SuperUser DO" and is utilized to gain access to restricted files and actions. Linux, by default, limits access to crucial parts of the system to protect sensitive information from being endangered. The sudo command, however, temporarily elevates the user's privileges, enabling them to perform crucial tasks without logging in as the root user.

1. First, we install sudo:
```
apt-get update -y apt-get upgrade -y apt-get install sudo
```
* The -y automatically answer to any prompts during the update and upgrade process)


2. Adding our user to the sudo group:
```
sudo adduser "username" sudo    or     * sudo usermod -aG sudo "username"
sudo reboot // then we need to login again
sudo whoami // checks if the user has sudo privileges - needs to answer "root")*
sudo -v // updates the user's timestamp -> makes it possible to run future sudo commands without entering a password until the authentication token is expired
sudo addgroup user42 // creates new user group called user42
sudo adduser "username" user42 // creates new username and adds it to the user42 group
sudo apt-get update
```
```
* If not, we need to add "username  ALL=(ALL:ALL) ALL" to the sudoers.tmp file with the command * sudo visudo
```

3. To check if the user was successfully added to the sudo group:
```
getent group sudo
```

### Setting up SSH service:

1. First, we need to install the openssh-server:
```
sudo apt-get update -y sudo apt-get upgrade -y sudo apt install openssh-server
```

2. Then, we need to check if the service is running:
```
sudo systemctl status ssh
```

3. It is also mandatory to change the default port 22 to 4242, by editing the line:
```
sudo vi /etc/ssh/sshd_config
```
```
"#Port 22" -> "Port 4242"
```
 
4. On the same file edition, we edit (then save and exit):
```
"#PermitRootLogin prohibit-password" -> "PermitRootLogin no"
```

5. Then we go to `VM` -> `Settings` -> `Network` -> `Adapter 1` -> `Advanced` -> `Port Forwarding`, and add a rule for `host port 4242` and` guest port 4242`

6. We restart the SSH service for the changes to take place, and check if everything is ok:
```
sudo reboot
sudo service ssh status
```

7. Then, in the terminal we need to type to connect:
```
ssh "username"@"ip" -p 4242 or * ssh "username"@localhost -p 4242 
```

8. After that, we can just type `exit` to quit the connection if we want.


### Setting up UFW

1. First, we need to install UFW:
```
sudo apt update -y sudo apt upgrade -y sudo apt install ufw
```

2. Then, we need to enable it and allow the port 4242:
```
sudo ufw enable
sudo ufw allow 4242 // (if we want to deny, we can use sudo ufw delete "portnumber")
```

3. We can check the status of the firewall:
```
sudo ufw status (numbered)
```

### Setting more things up on sudo:

1. We create a configuration file in order to add more settings to sudo:
```
sudo touch /etc/sudoers.d/sudoconfig
sudo mkdir /var/log/sudo (for the log files)
touch sudo.log
sudo vi /etc/sudoers.d/sudoconfig
```

* Inside the editor, we need to write:
```
Defaults	env_reset
Defaults	mail_badpass
Defaults	secure_path="/usr/local/sbin:/usr/local/bin:/usr/bin:/sbin:/bin"
Defaults	badpass_message="Password is wrong, please try again!"
Defaults	passwd_tries=3
Defaults	logfile="/var/log/sudo.log"
Defaults	log_input, log_output
Defaults	requiretty
```
  
### Password policy:

Some of the rules we need to use are:

* Password `expiration` is mandatory `every 30 days` with a `minimum of 2 days notice` before change. 
* Users should receive a `warning message 7 days prior to expiration` and must ensure the password 
is `at least 10 characters` in length, containing `an uppercase letter and a number`, and not exceeding 
* `3 consecutive identical characters`.
* The password cannot include the `user's name`. 
Note: This rule does not apply to the root password, but it must have a minimum of 7 non-repeated 
characters from the previous password."

	* The primary advantage of having strict password complexity guidelines is that they promote the creation of strong and distinct passwords, making them difficult to decipher. By increasing the number of mandatory requirements, the amount of potential combinations between letters, numbers, and symbols grows, enhancing password security.


1. Use the editor to open the configuration file and make the changes:
```
sudo vi /etc/login.defs
```
```
PASS_MAX_DAYS    "30" -> the maximum days that a password can be active for the user
PASS_MIN_DAYS    "2" -> the minimum days allowed between password alterations
PASS_WARN_AGE     7 -> it's already this value by default, so we can just leave it as it is
```

2. Then, to apply the changes to the existing users, we use:
```
sudo chage -M 30 "username" and sudo chage -M 30 "root"
sudo chage -m 2 "username" and sudo chage -m 2 "root"
sudo chage -W 7 "username" and sudo chage -W 7 "root"
sudo chage -l "username" -> to check the user settings
```

3. Next, we should use the following commands:
```
sudo apt install libpam-pwquality
sudo vim /etc/pam.d/common-password
```

* We need to add the following line to the end of the line containing `password requisite pam_pwquality.so retry=3)` - we can put them side by side:
```
minlen=10 // the minimum acceptable size for the new password
ucredit=-1 // the maximum credit for having uppercase characters in the new password (if > 0, it is the minimum number of uppercase characters in the new password)
lcredit=-1 // the maximum credit for having lowercase characters in the new password (if > 0, it is the minimum number of lowercase characters in the new password)
dcredit=-1 // // the maximum credit for having digits in the new password (if > 0, it is the minimum number of digits in the new password)
maxrepeat=3 // the maximum number of allowed consecutive same characters in the new password (the check is disabled if the value is 0)
reject_username // doesn't allow the username to be present in the password
difok=7 // the number of characters in the password that must be different from the old password
enforce_for_root // enforces pwquality checks on the root user password
usercheck = 1 // prompts the user 1 time before returning an error
```

4. We should then change our previous passwords, in order for them to match the new rules:
```
sudo passwd "user" and sudo passwd "root"
sudo reboot
```
* If something goes wrong, you can alway "sudo reboot".


### Configuring the network adapter

1. It is needed to go to the `Oracle VM VirtualBox Manager`, select `Settings` -> `Network` -> `Adapter 1`, and change it to `Bridged Adapter`.


### Setting up `cron`

1. First, we need to create the script file:
```
sudo apt-get install net-tools (install this tool first)
cd /usr/local/bin/
sudo vi monitoring.sh (and copy the following lines of code inside of it)
```
```
#!/bin/bash

architecture=$(uname -a)
physical_cpu=$(grep "physical id" /proc/cpuinfo | sort | uniq | wc -l)
virtual_cpu=$(grep -c ^processor /proc/cpuinfo)
memory_usage=$(free -m | awk 'NR==2{printf "%s/%sMB (%.2f%%)\n", $3,$2,$3*100/$2 }')
total_disk=$(df -Bg | grep '^/dev/' | grep -v '/boot$' | awk '{ft += $2} END {print ft}')
used_disk=$(df -Bm | grep '^/dev/' | grep -v '/boot$' | awk '{ut += $3} END {print ut}')
percent_used_disk=$(df -Bm | grep '^/dev/' | grep -v '/boot$' | awk '{ut += $3} {ft+= $2} END {printf("%d"), ut/ft*100}')
cpu_load=$(top -bn1 | grep load | awk '{printf "%.2f%%\n", $(NF-2)}')
last_boot=$(who -b | awk '$1 == "system" {print $3 " " $4}')
lvm_partitions=$(lsblk | grep -c "lvm")
lvm_is_used=$(if [ $lvm_partitions -eq 0 ]; then echo no; else echo yes; fi)
tcp_connections=$(cat /proc/net/sockstat{,6} | awk '$1 == "TCP:" {print $3}')
users_logged_in=$(w -h | wc -l)
ipv4_address=$(hostname -I)
mac_address=$(ip link show | awk '$1 == "link/ether" {print $2}')
sudo_commands_count=$(journalctl _COMM=sudo | grep -c COMMAND) 

wall "  
#Architecture: $architecture
#CPU physical: $physical_cpu
#vCPU: $virtual_cpu
#Memory Usage: $memory_usage
#Disk Usage: $used_disk/${total_disk}Gb ($percent_used_disk%)
#CPU load: $cpu_load
#Last boot: $last_boot
#LVM use: $lvm_is_used
#Connexions TCP: $tcp_connections ESTABLISHED
#User log: $users_logged_in
#Network: IP $ipv4_address($mac_address)
#Sudo: $sudo_commands_count cmd"
```
```
$architecture -> prints the name, version and more details about our machine and our OS (the architecture of the operating system and its kernel version)
$physical_cpu -> lists our CPUs (physical processors)
$virtual_cpu -> shows how many virtual processors we have (if we have multi-core processors)
$memory_usage -> shows the available RAM on our server and its utilization %
$last_boot -> the date and time of the last reboot
$lvm_is_used -> whether LVM is active or not
$tcp_connections -> the number of active connections
$users_logged_in -> the number of users using the server
$ipv4_address -> the IPv4 address of your server
$mac_address -> the MAC address (associated with the network adapter)
$sudo_commands_count -> the number of commands executed with the sudo program
```

```
sudo chmod 777 monitoring.sh // making it executable
```

2. Then, it is needed to make some changes:
```
sudo visudo 
```
* Under the line `%sudo ALL=(ALL:ALL) ALL`, we need to type: 
```
"username ALL=(root) NOPASSWD: /usr/local/bin/monitoring.sh"
```
* Also, after the line `root ALL=(ALL:ALL) ALL`, we also need to include: 
```
"username ALL=(ALL:ALL) ALL"
```

* Next, we exit and save the file.
```
sudo reboot
```

3. We then add the job that cron will do:
```
sudo /usr/local/bin/monitoring.sh
sudo crontab -u root -e
```
* And we add the following at the end:
```
@reboot /usr/local/bin/monitoring.sh
*/10 * * * * /usr/local/bin/monitoring.sh
```

4. We should then check the scheduled jobs:
```
sudo tab -u root -l
```


## For the BONUS PART:

1. First, we are going to install PHP:
```
sudo apt update
sudo apt install curl
sudo curl -sSL https://packages.sury.org/php/README.txt | sudo bash -x
sudo apt update 
sudo apt install php8.1
sudo apt install php-common php-cgi php-cli php-mysql
```
    
    
2. Next, we are going to install `Lighttpd`, but first we need to uninstall Apache - that could have been installed along with PHP, in order to avoid any conflicts)
```
 Lighttpd is a free and open-source web server software optimized for high performance and low memory footprint. 
 It is designed to be fast, secure, and flexible, and is commonly used for hosting websites and web applications.
 Lighttpd supports various web protocols and technologies, including HTTP, HTTPS, FastCGI, and SCGI, and is highly
 configurable through its configuration file.
```
```
systemctl status apache2
sudo apt surge apache2
sudo apt install lighttpd
sudo systemctl start lighttpd
sudo systemctl enable lighttpd
sudo systemctl status lighttpd
sudo ufw allow 80 // to allow incoming connections using the port 80 - `http`
sudo ufw status // to check if the port is ok
```

* We also need to go to `VM` -> `Settings` -> `Network` -> `Adapter 1` -> `Advanced` -> `Port Forwarding`, and set a rule for `host port 8080` forward to the `guest port 80`.

* It's possible to test if its working if we go to the browser of the host and go to the address `http://localhost:8080`

* Also, we need to activate Lighttpd FasCGI module, with the commands:
```
sudo lighty-enable-mod fastcgi
sudo lighty-enable-mod fastcgi-php
sudo service lighttpd force-reload
```

* To test if its working okay with PHP, we can create a file in `/var/www/html` named `info.php`, and write:
```
<?php
phpinfo();
?>
```

* Then we save and go to the host's browser "http://127.0.0.1:8080/info.php"

3. Then, we install and configure `MariaDB`
```
MariaDB is a community-driven fork of the MySQL database management system, designed as a drop-in replacement 
for MySQL. It provides robust and reliable data storage, management and retrieval capabilities. MariaDB is widely
used in web-based applications, content management systems,Cand data-driven websites. Some of its features include
support for various storage engines, advanced security measures, and a high level of compatibility with MySQL, 
which makes it an attractive alternativeCfor those seeking a drop-in replacement for it.
```
```
sudo apt install mariadb-server
sudo systemctl start mariadb
sudo systemctl enable mariadb
systemctl status mariadb
sudo mysql_secure_installation // in order to remove insecure default settings
```
* Then we should just press enter when prompted for the new password;
* Answer "y" to all of the questions (and we need to set up a new password).
```
sudo systemctl restart mariadb
```

* Next we in to the MariaDB console:
```
mysql -u root -p
```
* Then we create the database and the user: 
```
CREATE DABATASE 42lisboa;
CREATE USER 'admin'@'localhost' IDENTIFIED BY 'WPpassw0rd';
GRANT ALL ON 42lisboa.* TO '<username-2>'@'localhost' IDENTIFIED BY '<WPpassw0rd>' WITH GRANT OPTION;
FLUSH PRIVILEGES;
EXIT;
```
* To verify if the database was successfully created, we can use:
```
mariadb -u root -p
SHOW DATABASES; (confirm which database user has access to the database)
```

4. Finally, we download and configure Wordpress:
```
sudo apt-get install wget (installing wget)
sudo apt-get install tar
sudo wget http://wordpress.org/latest.tar.gz -P /var/www/html
sudo tar -xzvf /var/www/html/latest.tar.gz 
sudo rm /var/www/html/latest.tar.gz
sudo cp -r /var/www/html/wordpress/* /var/www/html
sudo rm -rf /var/www/html/wordpress
sudo cp /var/www/html/wp-config-sample.php /var/www/html/wp-config.php // creating config file
sudo vi /var/www/html/wp-config.php // configuring WP to reference the database & user created in MariaDB
```
* We then replace the lines:
```
		line 23 -> define( 'DB_NAME', '<database-name>' ); (42lisboa)
		line 26 -> define( 'DB_USER', '<username-2>' ); (admin)
		line 29 -> define( 'DB_PASSWORD', '<password-2>' );
```

5. To finish, we change the permissions on the WP directory, in order to grant rights to the web server, restarting Lighttpd:
```
sudo chown -R www-data:www-data /var/www/html/
sudo chmod -R 755 /var/www/html/
sudo systemctl restart lighttpd
```

6. Then in the browser, we go to `http://127.0.0.1:8080` to finish the installation.


### Final touches:

* We can disable `dhcpclient` - open port 68:
```
sudo vi /etc/network/interfaces
```
* And erase the comment "iface enp0s3 inet dhcp"
```
sudo reboot
```


### Before finishing your project:

* Check the script is running every 10 minutes
* Check my login with username
* Check if password is requesting on Born2beroot
* Check is password is following its strict rules
* Make sure we are not running any graphical user interface (GUI)
	
	
### Creating a signature.txt file:
* First, we need to turn off our machine, and go to the terminal and type the following commands:
```
cd sgoinfree/<VM_directory>
sha1sum "file".dvi
```
* Then we need to copy only the signature number inside this file, and create a nem one called "signature.txt", containing the VM signature's number.


### For the evaluation:	


* Check OS Debian: 
```
cat /etc/os-release | grep PRETTY_NAME
```

* Checking the partition scheme - comparing if its like the subject one:
```
lsblk
```

* Checking if sudo is installed properly:
```
dpkg -l | grep sudo
```

* Check if UFW service is properly installed and running: 
```
pdkg -l | grep ufw
sudo ufw status 
sudo ufw status | 4242
sudo ufw status numbered
sudo ufw delete $number // if you want to delete a rule
```

* Checking AppArmor status
```
sudo aa-status
```

* Check if SSH service is properly installed and running: 
```
dpkg -l | grep openssh-server
sudo service ssh status
```

* Verifying that SSH only uses port 4242
```
sudo service ssh status | grep listening
```

* Logging in with SSH from the host machine:
```
ssh gubranco@localhost -p 4242
```

* We also have to make sure we cannot login in SSH with root user:
```
login root // we need to see the message "login: Cannot possibly work without effective root"

```

* Implementation of subject's rules:
```
vi /etc/sudoers.d/sudoconfig
```

* Check password expiry: 
```
vi /etc/login.defs // check lines 160/161
```

* Check password policy (and be able to explain how they were setup)
```
vi /etc/pam.d/common-password // check line 25
```

* Check that your user is a member of user42 group: 
```
groups "user"
```

* Check group user:
```
getent group sudo
getent group "user42"
```

* Create a new user: 
```
sudo adduser "new_user"
sudo chage -l "new_user" // verify password expire info
```

* Adding the new user to sudo group:
```
sudo adduser "new_user" sudo
```

* Create a group "evaluating", adds a new user to it and checks if the user belongs to the new group:
```
sudo addgroup "evaluating"
sudo adduser "new_user" "evaluating"
groups "new_user"
```

* Check the hostname of the machine (gubranco42): 
```
uname -n or hostname
```

* Modifying the hostname with the evaluator's login and reboot to confirm:
```
sudo adduser "new_user" sudo
sudo login "new_user"
sudo vi /etc/hostname // here we change to "new_user42"
sudo reboot
```

* Restoring the original hostname:
```
sudo vi /etc/hostname // change it back to "gubranco42"
sudo reboot
```

* Verifying /var/log/sudo/ exists and has a file (seq):
```
sudo ls /var/log/sudo/
```

* Checking the files:
```
sudo ls /var/log/sudo/00/00
sudo ls /var/log/sudo/00/00/<newfolder> 
````
````
sudo cat /.../log # Input log
sudo cat /.../ttyout # Output log
````
````
sudo apt update
sudo ls /var/log/sudo/00/00
````

* Changing the run of the script in cron (to every minute):
```
sudo crontab -e 
add the line: "*/1 * * * * /usr/local/bin/monitoring.sh"
```

* To make the script stop running after we reboot without modifying it:
```
sudo crontab -e
And we remove the lines "@reboot /usr/local/bin/monitoring.sh" and "*/1 * * * * /usr/local/bin/monitoring.sh"
```

That's it! :)

### Here's more info on the subject:





