# <h1> DB Tier
# <h2> Provisioning

1. Provision 2 new Microsoft Servers. In this case we will be using Microsoft Server 2016. 
	1. One of these servers will host our MSSQL DB. 
	2. The other will host our Windows Domain Controller 
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

# <h2> MSSQL Server Setup
1. Download Microsoft SQL server 2016 SP1
2. Run through the Wizard configuration steps
3. 
credits to https://protechgurus.com/configure-domain-controller-in-windows-server-2016/
