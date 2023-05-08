# 🖥️ 42_IC_Ring01_Born2beRoot
## Preface:
   - This is a guide to the Born2beRoot project, and it was written using resources from several other guides, therefore the credit is to them.
   - The purpose of re-writing this updated guide is to edit some errors that I've come across using some of the guides, and to help prevent issues that I've had to troubleshoot.
   - Debian is the chosen Operating System for this project.
   - The Mandatory part of the subject.pdf involves using the Guided Partitioning Method of the Debian installation. The Bonus part of the subject.pdf involves using the Manual Partitioning Method. This guide has instructions for the Manual Partitioning Method, which I recommend you do from the start, thus passing you both the Mandatory part, and 1/3 of the Bonus part of Born2beRoot. 

## 🔷 Outline of Steps:
   - Step 1: Download the Debian installer for your Virtual Machine (VM)
   - Step 2: Installing your VM
   - Step 3: Setting up your VM partitions
   - Step 4: Starting & setting up your VM
   - Step 5: Connecting to SSH
   - Step 6: Configuring your VM - Password Policy
   - Step 7: Creating user Groups
   - Step 8: Configuring your VM - User Priviledges
   - Step 9: Configuring your VM - Script Monitoring & Crontab
   - Step 10: Self-evaluation Checklist & Testing
   - Step 11: Retrieve the Signature of your machine’s virtual disk
   - Step 12: Evaluation Questions & Answers

## 🔷 Step 1: Download the Debian installer for your Virtual Machine (VM)

### 🔸 1.1: Debian
1. [Click here to download Debian GNU/Linux](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/)
2. Scroll to the bottom of the page and select `debian-mac-xx.x.x-amd64-netinst.iso`

### 🔸 1.2: VM Directory (For 42Adelaide Students)
1. In iTerm2:
    - `cd sgoinfre/students`
    - `mkdir <your_intra_usename>`
    - `chmod 700 <your_intra_usename>`
2. Find your Debian download file from Step 1.1 and put that download in this `sgoinfre/students/<your_intra_usename>` directory that you have just created (_in iTerm2,_ `open .` _to open/find the directory, and drag/drop your Debian download file in there_). 

### 🔸 1.3: Virtual Box
1. Open the Virtual Box application

## 🔷 Step 2: Installing your VM
1. Select `New`

2. Name and operating system:
    - Name: e.g. `Born2beRoot`
    - Machine Folder: `/sgoinfre/students/<your_intra_usename>` (_Do not type this in, use the drop down option._)
    - Type: `Linux `
    - Version: `Debian (64-bit)`
    - `Continue`

3. Memory Size:
    - `1024`MB
    - `Continue`

4. Hard disk:
    - Select `Create a Virtual Hard Disk Now`
    - `Create`

5. Hard disk file type:
    - Select `VDI (VirtualBox Disk Image)`
    - `Continue`

6. Storage on physical hard disk:
    - Select `Dyamically Allocated`
    - `Continue`

7. File location and size:
    - `12.00`GB
    - `Create`

8. VM Storage:
    - Go to `Settings`
    - Select `Storage`
    - Find "Optical Drive" under "Attributes" & click on the drop down menu. Select `Choose a disk file...`
    - Select the Debian Download file (.iso) from your `/sgoinfre/students/<your_intra_usename>` directory. 
    - `Open`
    - `Ok`

## 🔷 Step 3: Setting up your VM partitions
1. Go to `Start` (_The green arrow_)
    Note: you will only be able to use your Keyboard to operate your Virtual Machine.
    Note: to increase the size of your VM window, go to the menu bar and either:
    - Select `Scaled Mode (Host+C)` then, with your mouse drag the VM window.
    - Select `Virtual Screen 1` then, select `Scale to 200% (autoscaled output)`

2. Select `Install` (_Do not select "Graphical install"_).

3. Select a language: `English`

4. Select your location: `Australia`

5. Configure the keyboard: `American English`

6. Configure the network:
    - Hostname: `<your_intra_username42>` (_ensure "42" is at the end_)
    - Domain name: leave blank

7. Set up users and passwords:
    - Root password: it is reccomended you use the same passwords for all passwords. Write it down should you forget it. 
    - Full name for the new user: personally, I used `<your_intra_username>` without the "42". 
    - Username for your account: `<your_intra_username>` without the "42". 
    - Choose a password for the new user: use the same password as "Root password".

8. Partition disks:
   
   🔸
    - Select `Manual`
    - Select `SCSI1 (0,0,0) (sda) 8.6 GB ATA VBOX HARDDISK`
    - Create new empty partition table on this device?: `Yes`
    - Select `pri/log 8.6 GB FREE SPACE`
    - How to use this free space: `Create a new partition`
    - New partition size: `500M`
    - Type for the new partition: `Primary`
    - Location for the new partition: `Beginning`
    - Partition settings: `Mount point:     /`
    - Mount point for this partition: `/boot - static files of the boot loader`
    - Partition settings: `Done setting up the partition`
    
   🔸
    - Select `pri/log 8.6 GB FREE SPACE`
    - How to use this free space: `Create a new partition`
    - New partition size: `max`
    - Type for the new partition: `Logical`
    - Partition settings: `Mount point:     /`
    - Mount point for this partition: `Do not mount it`
    - Partition settings: `Done setting up the partition`
    
   🔸
    - Select `Configure encrypted volumes`
    - Write changes to disk and configure encrypted volumes?: `Yes`
    - Encryption configuration actions: `Create encrypted volumes`
    - Devices to encrypt: using <Space bar> to select/de-select, ensure that: 
        - `[ ] /dev/sda1` is de-selected
        - `[*] /dev/sda5` is selected 
    - Select `Done setting up the partitions`
    - Encryption configuration actions: `Finish`
    - Really erase the data on SCSI1 (0,0,0), partition #5 (sda)?: `Yes`
    - Encryption passphrase: Personally, I used the same password set previously, x2, to avoid forgetting it.

   🔸
    - Select `Configure the Logical Volume Manager`
    - Write the changes to disks and configure LVM?: `Yes`
    - LVM configuration action: `Create volume group`
    - Volume group name: `LVMGroup`
    - Devices for th new volume group:
        - `[*] /dev/mapper/sda5_crypt` is selected
        - `[ ] /dev/sda1` is de-selected
    
   🔸
    - LVM configuration action: `Create logical volume`
    - Volume group: `LVMGroup`
    - Logical volume name: `root`
    - Logical volume size: `2G`
    
   🔸
    - LVM configuration action: `Create logical volume`
    - Volume group: `LVMGroup`
    - Logical volume name: `swap`
    - Logical volume size: `1024MB`
    
   🔸
    - LVM configuration action: `Create logical volume`
    - Volume group: `LVMGroup`
    - Logical volume name: `home`
    - Logical volume size: `1G`
    
   🔸
    - LVM configuration action: `Create logical volume`
    - Volume group: `LVMGroup`
    - Logical volume name: `var`
    - Logical volume size: `1G`
    
   🔸
    - LVM configuration action: `Create logical volume`
    - Volume group: `LVMGroup`
    - Logical volume name: `srv`
    - Logical volume size: `1G`
    
   🔸
    - LVM configuration action: `Create logical volume`
    - Volume group: `LVMGroup`
    - Logical volume name: `tmp`
    - Logical volume size: `1G`
    
   🔸
    - LVM configuration action: `Create logical volume`
    - Volume group: `LVMGroup`
    - Logical volume name: `var-log` (_yes, type only one '-' which will be automatically updated to '--'_)
    - Logical volume size: `1056MB`
    - LVM configuration action: `Finish`
    
   🔸
    - Under the line with "LV home" in it, select `#1`
    - Partition settings: `Use as:    do not use`
    - How to use this partition: `Ext4 journaling file system`
    - Partition settings: `Mount point:   none`
    - Mount point for this partition: `/home - user home directories`
    - Partition settings: `Done setting up the partition`
   
   🔸
    - Under the line with "LV root" in it, select `#1`
    - Partition settings: `Use as:    do not use`
    - How to use this partition: `Ext4 journaling file system`
    - Partition settings: `Mount point:   none`
    - Mount point for this partition: `/ - the root file system`
    - Partition settings: `Done setting up the partition`

   🔸
    - Under the line with "LV srv" in it, select `#1`
    - Partition settings: `Use as:    do not use`
    - How to use this partition: `Ext4 journaling file system`
    - Partition settings: `Mount point:   none`
    - Mount point for this partition: `/srv - data for services provided by this system`
    - Partition settings: `Done setting up the partition`
   
   🔸
    - Under the line with "LV swap" in it, select `#1`
    - Partition settings: `Use as:    do not use`
    - How to use this partition: `swap area`
    - Partition settings: `Done setting up the partition`
   
   🔸
    - Under the line with "LV tmp" in it, select `#1`
    - Partition settings: `Use as:    do not use`
    - How to use this partition: `Ext4 journaling file system`
    - Partition settings: `Mount point:   none`
    - Mount point for this partition: `/tmp - temporary files`
    - Partition settings: `Done setting up the partition`
   
   🔸
    - Under the line with "LV var" in it, select `#1`
    - Partition settings: `Use as:    do not use`
    - How to use this partition: `Ext4 journaling file system`
    - Partition settings: `Mount point:   none`
    - Mount point for this partition: `/var - variable data`
    - Partition settings: `Done setting up the partition`

   🔸
    - Under the line with "LV var-log" in it, select `#1`
    - Partition settings: `Use as:    do not use`
    - How to use this partition: `Ext4 journaling file system`
    - Partition settings: `Mount point:   none`
    - Mount point for this partition: `Enter manually`
    - Mount point for this partition: `/var/log`
    - Partition settings: `Done setting up the partition`
    - At the end of the list, select `Finish partitioning and write changes to disk`
    - Write the changes to disk?: `Yes`
   
9. Confugure the package manager:
    - Scan another CD or DVD?: `No`
    - Debian archive mirror country: `Australia`
    - Debian archive mirror: `deb.debian.org`
    - HTTP proxy information (blank for none): leave blank

10. Software selection:
    - Choose software to install: ensure all items are de-selected

11. GRUB boot loader:
    - Install the GRUB boot loader to the master boot record?: `Yes`
    - Device for boot loader installation: `/dev/sda (ata-VBOX_HARDDISK_xxxxxxxxxx-xxxxxxxx)`
   
12. Finish the installation:
    - Installation complete: `Continue`


## 🔷 Step 4: Starting & setting up your VM
   
### 🔸 4.1: Starting up your VM
1. At every start up, use your encryption password.
2. You can either:
    - Login as `root` or
    - Login as `<your_intra_username>`, then later use `su -` to log in as root if required.

### 🔸 4.2: Installing Sudo
1. Ensure you are logged in as root: `su -`
2. `apt-get update -y`
3. `apt-get upgrade -y`
4. `apt install sudo`
5. `sudo usermod -aG sudo <your_intra_username>` to add user in the group 'sudo'.
6. `getent group sudo` to check if user is in sudo group.
7. `sudo visudo` to open the sudoers file.
8. Find the line: # User privilege specification. Underneath that line, type `<your_intra_username>  	ALL=(ALL) ALL`

### 🔸 4.3: Installing Git
1. `sudo apt-get install git -y`

### 🔸 4.4: Installing Vim
1. `sudo apt-get install vim -y`

### 🔸 4.5: Installing & Configuring SSH (Secure Shell Host)
1. `sudo apt install openssh-server`
2. `sudo systemctl status ssh` to check SSH Server Status.
3. `sudo vim /etc/ssh/sshd_config`
4. Find the line #Port22. Edit it to `Port 4242` without the '#' in front of it.
5: Save and Exit Vim. (_Use `:q` then follow the prompts to save. '^' means `<Ctrl>`_).
6. `sudo service ssh restart` to restart the SSH Service.
   
### 🔸 4.6: Installing & Configuring UFW (Uncomplicated Firewall)
1. `sudo apt-get install ufw` to install UFW.
2. `sudo ufw enable` to enable UFW.
3. `sudo ufw status numbered` to check the status of UFW.
4. `sudo ufw allow ssh` to configure the Rules.
5. `sudo ufw allow 4242` to configure the Port Rules.
6. `sudo ufw status numbered` to check the status of UFW 4242 Port.
   
## 🔷 Step 5: Connecting to SSH
Note: press `<command>` on your Apple Keyboard & your mouse should re-appear
1. Go to your Virtual Box Program.
2. Click on your Virtual Machine and go to `Settings`
    - Go to `Network`
    - Select `Adapter 1`
    - Select `Advanced`
    - Click on `Port Forwarding`
    - Change the Host Port & Guest Port to `4242`:
         - Name: Rule 1
         - Protocol: TCP
         - Host IP: (_blank_)
         - Host Port: 4224
         - Guest IP: (_blank_)
         - Guest Port: 4242
    - `Ok`
3. Go back to your Virtual Machine.
4. `sudo systemctl restart ssh` to restart your SSH Server.
5. `sudo service sshd status` to check your SSH Status.
6. Open an iTerm & type `ssh <your_intra_username>@127.0.0.1 -p 4242`
    - Note: In case an error occurs, type `rm ~/.ssh/known_hosts` in your iTerm & then retype `ssh <your_intra_username>@127.0.0.1 -p 4242`
7. Type `exit` to quit your SSH iTerm Connection.

## 🔷 Step 6: Configuring your VM - Password Policy
1. `sudo apt-get install libpam-pwquality` to install Password Quality Checking Library
2. `sudo vim /etc/pam.d/common-password`
3. Find this line: `password		requisite		pam_deny.so`
    - Add to the end of that line `minlen=10 ucredit=-1 dcredit=-1 maxrepeat=3 reject_username difok=7 enforce_for_root`
    - The line should now look like this: `password  requisite     pam_pwquality.so  retry=3 minlen=10 ucredit=-1 dcredit=-1 maxrepeat=3 reject_username difok=7 enforce_for_root`
4. Save and Exit Vim
5. `sudo vim /etc/login.defs` to configure the Password Policy.
6. Find this part `PASS_MAX_DAYS 9999 PASS_MIN_DAYS 0 PASS_WARN_AGE 7`. Edit that part to: 
    - `PASS_MAX_DAYS 30` 
    - `PASS_MIN_DAYS 2`
    - `PASS_WARN_AGE 7`
7. `sudo reboot` to reboot the change affects.
   
## 🔷 Step 7: Creating user Groups

### 🔸 7.1: Creating a group
1. `sudo groupadd user42` to create the group 'user42`.
2. `getent group` to check if the group has been created.

### 🔸 7.2: Group allocation
1. `sudo usermod -aG user42 <your_intra_username> to add your username to the group 'user42' as per subject requirements. 
2. `getent group user42` to check if the user is in the group.
3. `cut -d: -f1 /etc/passwd` to check all local users.

## 🔷 Step 8: Configuring your VM - User Priviledges

### 🔸 8.1: Creating the sudo.log  
1. `cd ~/../`
2. `cd var/log`
3. `mkdir sudo` 
4. `cd sudo`
5. `touch sudo.log`
6. `cd ~/../`

### 🔸 8.2: Configuring the Sudoers Group
1. `sudo visudo` to open to Sudoers file.
2. Edit your sudoers file by adding the rest of the defaults so it should read like this:
   `Defaults	env_reset
Defaults	mail_badpass
Defaults	secure_path="/usr/local/sbin:/usr/local/bin:/usr/bin:/sbin:/bin"
Defaults	badpass_message="Password is wrong, please try again!"
Defaults	passwd_tries=3
Defaults	logfile="/var/log/sudo/sudo.log"
Defaults	log_input, log_output
Defaults	requiretty`
  
   - Step 9: Configuring your VM - Script Monitoring & Crontab
   - Step 10: Self-evaluation Checklist & Testing
   - Step 11: Retrieve the Signature of your machine’s virtual disk
   - Step 12: Evaluation Questions & Answers
