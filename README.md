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

