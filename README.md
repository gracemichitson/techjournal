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
