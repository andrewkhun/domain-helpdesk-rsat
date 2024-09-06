# Joining a PC to a Domain, Creating a Helpdesk User, and RSAT Tools

Our high-level objectives are as follows:
- Create a Windows 10 machine and enable local Administrator account
- Create a helpdesk user by copying the Administrator account
- Install RSAT tools onto the Windows 10 VM to allow helpdesk to provide services from VM
- Change Server 2022 and Windows 10 Lab VM IP addresses to static in order to join both to the domain group

Let's get started!

## Creating a Windows 10 Machine

In order to create a Windows 10 machine, the process is extremely similar to how we created our Windows 2022 Server. First we need to download the Media Creation Tool from Microsoft in order to create a Windows 10 ISO. Google Windows 10 installation media and download the Media Creation Tool. Once downloaded run the tool to creation installation media of Windows 10 in the form of an ISO file, as shown below:

<img src="https://imgur.com/a9MQXBM.png" height="70%" width="70%" alt="VirtualBox downloads"/>

<img src="https://imgur.com/4CGDH7t.png" height="30%" width="30%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/FlNfGoI.png" height="70%" width="70%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/AwtO982.png" height="70%" width="70%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/Phd5S3f.png" height="70%" width="70%" alt="VirtualBox downloads"/>


After you have completed those steps, create a new virtual machine in VirtualBox using the Windows 10 ISO. This steps are the same as the Windows Server 2022 installation. We will be equipping the Windows 10 machine with 2 CPUs, 4 GBs of RAM, and 50 GB of hard drive space. Click Finish when you have selected all the appropriate options:

<img src="https://i.imgur.com/pevs9MD.png" height="70%" width="70%" alt="VirtualBox downloads"/>

Boot up the Virtual Machine and complete the Windows 10 Setup. Select "I don't have a product key", Windows 10 Pro in order to join the PC to the domain, and select "Custom: Install Windows only".

After fully installing Windows, the VM will restart at the end of the process. As it is restarting, go to the bottom right corner of the VirtualBox window and right-click the disc icon and select "Remove disk from virtual drive" to remove the installation ISO from the drive. This will avoid any prompts to boot from removable media.

<img src="https://i.imgur.com/UDAVdrI.png" height="70%" width="70%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/cZsWqop.png" height="70%" width="70%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/BbcPQ2W.png" height="70%" width="70%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/IYVFaNK.png" height="30%" width="30%" alt="VirtualBox downloads"/>

Complete the Windows 10 desktop setup by selecting:
- Set up for personal use
- Offline Account
- Limited Experience
- Typing in "User" for the PC
- Leave the password blank and click "Next"
- Accept to Recent browsing data
- Selecting "No" for all "privacy settings for your device"
- Skipping the "Customize your experience"
- And finally "Not Now" for Cortana

<img src="https://i.imgur.com/8ugy1cm.png" height="70%" width="70%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/YepzMOb.png" height="70%" width="70%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/cWwHNOi.png" height="70%" width="70%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/CROKPoS.png" height="70%" width="70%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/N0n84Wu.png" height="70%" width="70%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/z7wNtv1.png" height="70%" width="70%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/uMlufsZ.png" height="70%" width="70%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/pVgnOzZ.png" height="70%" width="70%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/WNDDmQI.png" height="70%" width="70%" alt="VirtualBox downloads"/>

Once you are logged in, open up File Explorer and right click on "This PC" then select "Manage". We will be enabling the local Administrator account since we are currently logged into the Windows 10 VM as a regular user. We want to get rid of this basic User account as we want this VM to be used by our Help desk role. 

Go to Local Users and Groups and then Users. Right-click Administrator and then Properties. Uncheck the "Account is Disabled" option then click Apply and OK. Right-Click the Administrator account once more and set a password for the Administrator. 

<img src="https://i.imgur.com/AQtyNz1.png" height="50%" width="50%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/0yTUDRw.png" height="50%" width="50%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/m9LaBSi.png" height="50%" width="50%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/ZfACVM6.png" height="50%" width="50%" alt="VirtualBox downloads"/>

Once the password is set, sign out of the User account and login using our new Administrator account. Once logged in, head back to Computer management and delete the "User" account as we no longer need it.

<img src="https://i.imgur.com/xvKDglx.png" height="50%" width="50%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/zD749Uk.png" height="70%" width="70%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/Vx8GQxP.png" height="50%" width="50%" alt="VirtualBox downloads"/>

Now that is over, we can move onto creating a helpdesk user account!


## Create a helpdesk user by copying the Administrator account

If you have not already, start up with Windows Server 2022 VM and log in. Open up Active Directory Users and Computers and head into the Users folder. Right-click on Administrator and click copy. Name the new user helpdesk and set a password. Once set, hit finish.

<img src="https://i.imgur.com/6KEy5KW.png" height="50%" width="50%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/veWdURa.png" height="50%" width="50%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/bgkMsZN.png" height="50%" width="50%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/pqEa75i.png" height="50%" width="50%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/JBko6mc.png" height="50%" width="50%" alt="VirtualBox downloads"/>

To explain why we are doing this, let's compare the groups that our newly created helpdesk user is in compared to a helpdesk2 user created by just doing "Create New User". 

If we look below we can see that the helpdesk user is a part of a lot more groups than the helpdesk2 user, and the reason is because we copied the initial Administrator user. By doing this we don't need to add every single group one by one, saving us time. If the helpdesk is part of a group that we don't need it to be in, we can just remove the group. 

<img src="https://i.imgur.com/BNNr40U.png" height="70%" width="70%" alt="VirtualBox downloads"/>


## Install RSAT tools on the Windows 10 Lab VM

RSAT (Remote Server Administration Tools) is a set of tools from Microsoft that allows IT administrators to remotely manage Windows servers and services from their own computers, without having to be physically at the server. It includes tools for managing things like Active Directory, DNS, DHCP, Group Policy, and more. RSAT helps system admins handle tasks efficiently from their workstations.

In order to install RSAT tools, we have to go to Apps & Features and then Optional Features. Click on Add a Feature and search RSAT in the searchbar.

<img src="https://i.imgur.com/tOOtgxZ.png" height="50%" width="50%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/U1vjMow.png" height="50%" width="50%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/lK6oZnO.png" height="50%" width="50%" alt="VirtualBox downloads"/>

The tools we will be installing are these 7 as shown below. This should give us all the tools our helpdesk needs to accomplish most tasks.

<img src="https://i.imgur.com/51B7GhO.png" height="50%" width="50%" alt="VirtualBox downloads"/>

While those are installing let's move onto our next task of setting up our static IP addresses for the domain!


## Static IP addresses for Windows Server and Windows 10 Lab

We want to create a Local Area Network so that the Server and VM can communicate with one another. On the Windows Server, go into the Network Settings and click "Change Adapter Options". 

Once there right-click the Ethernet adapter and select Properties. Click on Internet Protocol Version 4 (TCP/IPv4) and then click Properties once more. 

<img src="https://i.imgur.com/hvYGvvT.png" height="70%" width="70%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/mzmoFbp.png" height="50%" width="50%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/zi99IAo.png" height="50%" width="50%" alt="VirtualBox downloads"/>
