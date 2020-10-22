# techjournal
Lab 1: Virtual Firewall and WIndows 10 Configurations
Steps Involved:
Getting connected to VSphere: 
Make sure your Champlain connection is on through your settings (the VM)
Go to https://vcenter01.cyber.local and see all the connections from there\
      
 Make sure the MAC addresses match for the VSphere connection and the cyber.local connection, this ensures that they are wired and connected.
Through the vcenter connection, follow through the prompt to assign em0 and em1 to your LAN and WAN
The first interface em0 will be assigned to an address that has been given to us on a separate spreadsheet. Select option 2 to assign the interfaces. 
Follow the prompts and enter the correct addresses for the two interfaces.
Editing tracert # of hops:
tracert -h [# of hops] [address/website]
Remove the brackets, those are just placeholders


Lab 2: ADDS Role
The first step is to configure your new switch.
Ping to Google.com to insure that you are connected to the external network.
Go to (on the Server Manager) Manager>Add Roles and Features. Clicke through and select active directory domain services, and install and restart. Create a new forst name grace.local.

To add a DNS Record: invoke DNS Manager from Manager>DNS>AD01>grace.local>NewHost (A or AAAA).
If a warning pops up, it is because you must Reverse DNS. Fo to Reverse Lookup ZOnes> New Zone>network id 10.0.5. Apply as needed.

Create Named Domain Users: AD DNS>Active directory Users and COmputers. GO to New, and add a user. Then click on the user, and add it to a group. This group will give domain Admins access. 

Chnage wks01 DNS address to 10.0.5.5 (DNS on ad01)

lab 3: Linux
https://sites.google.com/a/champlain.edu/cncs-wiki/home/operating-systems/linux/network-configuration describes the process of setting a hostname and IP address on your linux server. 
Helpful tips:
1. SSH, or a secure shell, is a place where you can manage your linux systems remotemly. One does this by pulling up a shell, and typing ssh grace@dhcp01-grace, and that shall bring me to my linux system, on the wks01
2..bash_history command brings up a file with your last 10 commands entered into the shell. The file can actually contain the last 500 commands you’ve typed. It often contains users username and passwords. This can cause security issues because if someone can get access to your hidden bash history file, then they can potentially get their hands on a multitude of passwords. A pro is, of course, you’re able to keep data that could be essential in your system, and pull it up at later times. 
Helpful commands:
1. history | head -n 10 - view last 10 commands in your history
2. ls and ls-la shows hidden files
3. .bash_history is viewing your bash history files


the process for setting a static IP address on CentOS Linux :
1. Type nmtui
2. Click edit connections
3. Where it says "IPv4 CONFIGURATION" click to change it to manual. Add your ip/submet/gateway/servers
4. add your domain (grace.local)
5. click the automatically connect X
6. You should be good to go. Exit usinf the systemct1 restart network command. 

Lab04- DHCP
COnfiguring Dhcp services:
1. in the root- vi /etc/dhcp/dhcp.conf this command will help you write to the configuration file
2. to save and write changes :wq
3.to start dhcp type: systemctl start dhcpd
4. to enable dhcp: systemctl enable dhcpd
5. To configure the firewall and allow incoming dhcp requests:
      a. in root type firewall-cmd --list--all
      b.enter
      c. firewall-cmd --add-service+dhcp --permenent
      d. direwall-cmd --reload
      e. firewall-cmd --lis-all
6. Change IPv4 proterties on wks01 to automatically obtain the ip address and DNS server addresses

Wireshark ABOUT : https://docs.microsoft.com/en-us/windows-server/troubleshoot/dynamic-host-configuration-protocol-basics
DHCP Discover: The client sends this, which identifies the client and the packet as a discover packet.
DHCP Offer: This is a response packet to the discover packet. The source address is the DHCP server ip address. The destination address is the broadcast address.
DHCP Request: The client repsonds to the offer by sending a request. The clients ip is 0.0.0.0 because it has yet to recieve permission from the server that it is okay to use the ip address offered.The DHCP ip is still broadcast because it may be holding a place for an Offer to be made to the client.
DHCP ack: This is a response packet to DHCPREQUEST. It is completing the initialzation cycle. 

File Permissions:

To make a user: user add [name]

To make a group named marketing: groupadd marketing

To add people(bob) to that group(marketing): usermod -aG marketing bob

TO add file permission(marketing):

1. mkdir /marketing
2. ls -l / shows all the files and there permissions
3. su - bob (to become bob when youre in root)
4. echo newproducts >/marketing/newproducts.txt
5. to see who has permission echo bob > /marketing/newproducts.txt

TO chnage from root to marketing on who owns the file: (as well as modifying who can wrx the file)

1. ls -ld /marleting/
2.chgrp marketing / marketing
3. chmod g+w /marketing
The g repreents group premissions. It will be either owner group or other.

LAB ADDS Group Policy:

1. Go to Local Servers on your Server Manager and right click on tools. Then select Active Directory Users and Computers.
2. Create a new Organizational Unit by right clicking on grace.local.
3. Call this OU SYS255, and add 3 more OU's called accounts,computers, and groups.
4. Create users within the SYS255\accounts OU
5.DRAG WKS01-Grace from grace.local\computers OU to the SYS255\computers OU
6. Add a global security group within the SYS255\Groups, and name it custom-desktop. ALice and Bob are members. This allows you to change permissions based on the groups that some uers are in. This will be helpful if there was a different department in your system that should not have access to certian things.
7. BEST PRACTICE FOR GROUPS: Many times, organizations will have a number of groups defined in their active directory domain. For this reason, it is a best practice to have a naming convention that purposefully describes what the groups do. A lot of times, groups allow or disallow users permission to folders on the network. Think departments. For this reason, a commonly found group membership is in the form of something like this:
DepartmentName_RW_ACL or GP_WindowsIESettings_ACL
This gives administrators an idea of what the group is for, and who may need to be a member

Group policy- USER, this group policy will define the uder level settings.
1. tools > Group Policy Management
2. Right click on SYS255, and select Create a GPO in this domain, and link it here.
3. Chnage the users to custon-desltop, which would be alice and bob.
4. remove authenticated users, add domain Computers. 
5. RIght click on your new GP and click edit, and choose what you want to edit out of the homescreen.

TO CHANGE USERS AT THE LOGIN:
1.Create and Link a new GPO within the SYS255\Computers OU called DisableLastLogin
2. In the group policy management, right click and select edit for yout new OU 
3. policies>Windows settings > security settings > local policies
4. Choose at will. 

HOW TO PREPARE FOR ASSESSMENT:
1. Download all the Previous Labs done.
2. Set aside a  day to review the labs.
3. Review each topic that you had trouble with (the first three weeks). 
4. Take notes.
5. Review Github Tech Journal.
6. Ask Qustions if there is any. 
7. Pray. 

Lab7: Server Core and Administrator Tools

In FS01, type the command sconfig to configure the IP, Subnet Mask, Default Gateway, and DNS Server. Make sure to add what domain you are in in the same GUI.

NOTE** After changing everything, make sure to reboot.
Login to your adm account through the other user options

** RSAT
Log in to ad02. Within the Remote Server Administration Tool Feature, add file service tools and files server resource manager.
Add Roles and Features Wizard- RSAT>RAT>FIle Service Tools> make sure File Server Resource Manager TOols is clicked and hit next
Add FS01 to the servers section in the server manager.

You are now going to add roles and Features to your FS01 server, to do that, right click on the server. Keep the default settings down to Server Roles, then make sure you clicke File and Storage Services, Fil and iSCSI Services, and files server resourse manager

To open the irewall for managing on the file Server: run the following command on fs01:  
netsh advfirewall firewall set rule group=”Remote File Server Resource Manager Management” new enable=yes

To create a new share on FS01: go to Server Manager> Shares and right click to create a new share. Make sure the location is on the fs01 server, and the Share Name is called Sales, and it gives the remote path to share. In the permsiions setting, you can decide who has access. This will allow different permissions for different users to access the \\fs01-grace\sales.

To map a drive:
Open Group Policy Management, create a new GPO, right click and choose edit. Go to User Configuration > Preferences > Windows Settings > Drive Maps. Right-click and select New > Mapped Drive. Ubder the general tab determine the action, location, reconnection, label, drive letter, connection, and hide/show drives. CLick apply, open a command prompt, and type GPUPDATE. This will update the group policy.
APACHE Lab:

Configure Web01- go into nmtui like previous labs. Add domain, hostname, ip, netmask. Create a sudo user when done.

Disable remote root ssh access within the PermitRootLogin no flag in  /etc/ssh/sshd_config file. 
To do this:
# mv /etc/httpd/conf.d/welcome.conf /etc/httpd/conf.d/welcome.conf_backup
# systemctl restart httpd
then
# echo "<h1>This is a Test Page</h1>" > /var/www/html/index.html


Restart sshd, logout and login in again, so that your new hostname takes hold in the active session.
To instal httpd:
sudo yum update httpd
sudo yum install httpd
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https
sudo firewall-cmd --reload
sudo systemctl start httpd
sudo systemctl status httpd

To install php:
yum install php

To go into index.php:
cd /var/www/html 
once in the root command you want to vi index.php
edit and see changed. 

JOIN DOMAIN:
sudo yum install realmd samba samba-common oddjob oddjob-mkhomedir sssd

realm join --user=your-domain-admin-username@yourdomain.local yourdomain.local
realm list





