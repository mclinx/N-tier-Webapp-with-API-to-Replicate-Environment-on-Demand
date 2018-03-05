# <h1> DB Tier
# <h2> Provisioning

1. Provision 2 new Microsoft Servers. Alternatively, you can use 1 Microsoft Server as the Domain Controller and 1 linux (Ubuntu 16.04) server as the host for the MSSQL DB host. The DB will authenticate through its Domain Membership with Window Active Directory (AD). In this case we will be using Ubuntu 16.04 as our MSSQL DB. 
	1. Ubuntu 16.04 server will host our MSSQL DB. 
	2. The Micrsoft Server 2016 will host our Windows Domain Controller 
2. Assign both Servers to the the Manual Network that you have created. (This is needed for WDC to work properly)

# <h2> Domain Controller Setup
1. Start up the Server that will act as your Domain Controller.
2. open RUN and enter sysdm.cpl (system properties)
3. Set the desired computer name (DC1) 

_Once, you change your computer name you have to restart your system. Once the system is
rebooted, sign in to the system with the Administrator account. After some time, the Server 
Manager console will be displayed._

4. Reboot

_Now, we need to configure TCP/IP settings before to install and configure Domain Controller on a Windows server._

5. Open RUN and enter ncpa.cpl  

_Select and right-click the active network adapter, and then select Properties.
On the properties dialog box, set the following TCP/IP settings on your server:_

IP address: 10.0.0.100. \
Subnet mask: 255.0.0.0. \
Default gateway: 10.0.0.1. \
Preferred DNS server: 10.0.0.100. 

_**Now we need to promote your server as Domain Controller**_

6. Open Server Manager
7. Click add Roles and Features
8. Click Next until you see the Select server roles On this page, select the Active Directory Domain Services check box
9. Accept the Default options and click Next until you reach the end of the installation wizard.
10. Click Install
11. Click Close

_Once the installation process completes on DC1. Now, you have successfully installed the **Active Directory Domain Services** on your server. The next task is to configure your server as Domain Controller. To do so, continue to the next steps._

_**Configure Domain Controller**_
1. On the Server Manager console, click the Notifications icon.
2. Click the Promote this server to a domain controller link.

_On the Deployment Configuration page, select the Add a new forest radio button. In the Root domain name text box, type a domain name such as mcsalab.local_

3. Click Next

_On the Domain Controller Options page, make sure that the Domain Name System (DNS) server check box is selected. In the Password and Confirm password text boxes, type a DSRM password, and then click Next._

4. On the DNS Options page, click Next.
5. On the Additional Options page, click Next.
6. On the Paths page, review the default location for the AD DS database file, and then click Next.
7. On the Review Options page, click Next.
8. On the Prerequisites Check page, review the prerequisites, and then click Install.
9. After some time, the system will restart automatically, sign in to DC1 with the MCSALAB\Administrator.
10. Set DNS as 127.0.0.1

# <h2> Configure DHCP/DNS
Dynamic Host Configuration Protocol (DHCP) is as service that provides TCP/IP settings, such as IP address, subnet mask, default gateway, and DNS server to the clients, automatically. In a large enterprise network, it is difficult to manage IP addresses manually. Hence, DHCP can be a useful feature to manage the IP addresses in a large enterprise network.

In this post, we will explain how to install the DHCP server role and how to configure DHCP server in Windows Server 2016. For this, we will use a system named as DC1 that is configured with 10.0.0100/8 IP address and hosts the AD DS role service for the mcsalab.local domain. If you have not configured the Domain Controller yet, visit the following link for the step by step guide.
Configure Windows Server 2016 Domain Controller.

The configuration of DHCP server in Windows Server 2016 includes the following two major tasks:

Install the DHCP Server Role in Windows Server 2016
Configure DHCP in Windows Server 2016
Install DHCP Server Role in Windows Server 2016
Installing roles and features in Windows Server 2016 is exactly same as we use for the previous version of Windows Servers. To install the DHCP Server role on your server machine, open the Server Manager console and click the Add roles and features link. Click Next until the Select server roles page is displayed.
Select the DHCP Server check box. On the Add Roles and Features Wizard dialog box, click Add Features.
The Select server roles page returns with the DHCP Server role check box selected, as shown in the following figure, click Next.install dhcp server in windows server 2016
Complete the installation process.
Configure DHCP Server in Windows Server 2016
Now you have installed the DHCP server role on your server, the next task is to configure DHCP scope and other options. To do so, perform the following steps:

On the Server Manager console, click Tools, and then click DHCP.
On the DHCP console, expand your server name mcsalab.local.
Select and right-click your server name and then select Authorize to authorize your DHCP server.authorize dhcp server in windows server 2016
Refresh the DHCP console to enforce the changes. Notice that the icons next to IPv4 and IPv6 nodes change from red to green as shown in the following figure.Refresh DHCP console
Now, create a new DHCP scope to specify the IP address ranges for your DHCP server. To do so, select and right-click IPv4 and then select New Scope.
On the welcome page of the New Scope Wizard, click Next.
On the Scope Name page, specify a DHCP scope name as shown in the following figure, and then click Next.Create a new DHCP scope in Windows Server 2016
On the IP Address Range page, specify the start and end IP addresses from which the DHCP server will allocate the IP addresses to the clients. For example, we will use the following IP address range, as shown in the following figure. Click Next.
Start IP address: 10.0.0.225
End IP address: 10.0.0.250
Length: 8
Subnet mask: 255.0.0.0Configure DHCP scope in windows server 2016
On the Add Exclusions and Delay page, exclude the IP addresses that you want to be not distributed by the DHCP server. For example, we will exclude the following IP address range, as shown in the following figure.
Start IP address: 10.0.0.225
End IP address: 10.0.0.230Configure DHCP exclusion range in Windows Server 2016
Click Add, and then click Next. On the Lease Duration page, review the default lease duration limit, and then click Next.
On the Configure DHCP Options page, make sure that the Yes, I want to configure these option now radio button is selected and then click Next.
On the Router (Default Gateway) page, in the IP address text box, type the address of your router. In this demonstration, we will use 10.0.0.1 as a default gateway for the DHCP clients. If you don’t want to specify the router address, leave the IP address box blank and proceed to the next page.Configure DHCP default gateway
Click Add, and then click Next. On the Domain Name and DNS Servers page, make sure that your DNS server IP address is already populated. In this case, 10.0.0.100 as shown in the following figure, click Next.Specify dns options for DHCP server in windows server 2016
On the WINS Servers page, we are not going to use WINS server, hence, leave it as is and click Next.
On the Activate Scope page, make sure that the Yes, I want to activate this scope now radio button is selected, as shown in the following figure. Click Next and complete the wizard.Activate DHCP scope
Refresh the DHCP console. Make sure that the IPv4 node is marked with the green color as shown in the following figure.Install and Configure DHCP Server in Windows Server 2016
Now, your DHCP server is configured and ready to allocate TCP/IP settings to the DHCP clients

# <h2> MSSQL on Linux


# <h2> MSSQL on Microsoft
1. Download Microsoft SQL server 2016 SP1
2. Run through the Wizard configuration steps
3. 


**Resources**
https://protechgurus.com/configure-domain-controller-in-windows-server-2016/
https://protechgurus.com/configure-dhcp-server-in-windows-server-2016/
https://gallery.technet.microsoft.com/Step-by-Step-Installation-fae6cf20/file/169948/1/Step%20by%20Step%20Installation%20of%20Windows%20Server%202016%20Domain%20Controller.pdf

https://www.youtube.com/watch?v=0WyBxwJD_c0
https://www.youtube.com/watch?v=ZfsXh_LSkgE&list=PLJcaPjxegjBVnEN8c6O8w1mNit4WGeAWN&index=8
https://www.youtube.com/watch?v=6c3mwjjr3AQ&list=PLJcaPjxegjBVnEN8c6O8w1mNit4WGeAWN&index=9
https://www.youtube.com/watch?v=h9fmQ0crCsg&index=10&list=PLJcaPjxegjBVnEN8c6O8w1mNit4WGeAWN
https://www.youtube.com/watch?v=DrNwJraGfjQ&index=11&list=PLJcaPjxegjBVnEN8c6O8w1mNit4WGeAWN
https://www.youtube.com/watch?v=amzSIpx9fvA&index=18&list=PLJcaPjxegjBVnEN8c6O8w1mNit4WGeAWN

Install all these packages and create NAT\

http://funwithlinux.net/2014/04/join-ubuntu-14-04-to-active-directory-domain-using-realmd/
https://serverfault.com/questions/598476/how-to-use-realmd-in-ubuntu-14-04-lts-to-join-an-active-directory-domain

Nat \
http://www.nairabytes.net/81-linux/418-how-to-set-up-a-nat-router-on-ubuntu-server-16-04
http://nairabytes.net/81-linux/415-how-to-install-a-dhcp-server-in-ubuntu-server-16-04
http://nairabytes.net/81-linux/413-ubuntu-server-16-how-to-properly-set-hostname-domain-name-and-fdqn

https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-active-directory-authentication
https://www.mssqltips.com/sqlservertip/5075/configure-sql-server-on-linux-to-use-windows-authentication/
https://serverfault.com/questions/573160/sql-server-running-under-a-domain-account-cannot-register-its-spn

ENABLE ACCOUNT IN AD to get SPN to work

edit /etc/hosts in windows


https://vandewalle.me/connect-to-ms-sql-server-in-php-on-ubuntu-linux-16-04-lts/

https://docs.microsoft.com/en-us/sql/connect/php/installation-tutorial-linux-mac
https://docs.microsoft.com/en-us/sql/connect/php/pdo-exec
http://php.net/manual/en/datetime.format.php
http://php.net/manual/en/function.sleep.php
