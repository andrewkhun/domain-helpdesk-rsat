# Joining a PC to a Domain, Creating a Helpdesk User, and RSAT Tools

Our high-level objectives are as follows:
- Create a Windows 10 machine and join it to our domain
- Create a helpdesk user to imitate the role of a help desk role on the domain
- Provide said user RSAT tools to provide services from the Windows 10 machine

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

<img src="https://i.imgur.com/AQtyNz1.png" height="70%" width="70%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/0yTUDRw.png" height="70%" width="70%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/m9LaBSi.png" height="70%" width="70%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/ZfACVM6.png" height="70%" width="70%" alt="VirtualBox downloads"/>

Once the password is set, sign out of the User account and login using our new Administrator account. Once logged in, head back to Computer management and delete the "User" account as we no longer need it.

<img src="https://i.imgur.com/xvKDglx.png" height="70%" width="70%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/zD749Uk.png" height="70%" width="70%" alt="VirtualBox downloads"/>

<img src="https://i.imgur.com/Vx8GQxP.png" height="70%" width="70%" alt="VirtualBox downloads"/>


