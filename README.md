# Implementing OpenSSH for Secure Remote Communication: Comparing Encrypted Traffic

## Project Overview

The OpenSSH connectivity tool allows an OpenSSH client to remotely sign in to a system running an OpenSSH server. OpenSSH encrypts all traffic between the OpenSSH client and the OpenSSH server, thwarting man-in-the-middle (MITM) attacks, including eavesdropping, connecting hijacking, and more. SSH is used by systems administrators (and others) for remote management of systems and programs, software patch deployment, execution of commands, file management, and more.

## Step 1: 
### I’m going to install Windows Server 2019 (acting as a server) and Windows 10 (acting as a client) as virtual machines (I’m using VirtualBox).

![image](https://github.com/forza-dc/Implementing-OpenSSH-for-Secure-Remote-Communication-Comparing-Encrypted-Traffic/blob/main/Virtual%20box%20VM%20Setup.png) 

## Step 2:

### Performing the following steps on Windows 10 systems to install the OpenSSH Client and OpenSSH Server, so that it could be the client or server using OpenSSH.

        a. In the search bar, type settings, and select Settings.
        b. Click Apps, under Apps & Features and select Optional Features.
        c. Check to see if the OpenSSH Client or OpenSSH Server is already installed. The OpenSSH Client should be.
        d. To install the OpenSSH Server, click Add A Feature at the top of the window, put a check in the checkbox next to OpenSSH Server, and click the Install button.Ifthe OpenSSH Client was not installed, you 
           can select both the Open SSH Server and OpenSSH Client checkboxes and click the Install button.

![image](https://github.com/forza-dc/Implementing-OpenSSH-for-Secure-Remote-Communication-Comparing-Encrypted-Traffic/blob/main/OpenSSH%20Installation.png) 

Installing the openSSH Server automatically will create and enable the firewall rule named OpenSSH-Server-In-TCP, which allows unsolicited SSH traffic (port 22)
inbound to your system. This is needed since Windows Defender Firewall is stateful and will not allow anything unsolicited inbound otherwise.

## Step 3:
### Setting up Windows Server (2016 or 2019) as an OpenSSH Server:

a. Download OpenSSH server and wireshark files (located at the bottom of this screen)

![image](https://github.com/forza-dc/Implementing-OpenSSH-for-Secure-Remote-Communication-Comparing-Encrypted-Traffic/blob/main/Installing%20Wireshark.png) 

b. Copy downloaded files to Windows Server VM

c. Install Wireshark and reboot VM

d. Open the downloaded OpenSSHServer.zip and copy the first folder (named OpenSSHServer.zip) to "C:\Program Files" (located on the C drive)

e. Go to "C:\Program Files\OpenSSH-Win64" and edit the "sshd_config_default" file. That is, right click on the file and select open with and choose

![image](https://github.com/forza-dc/Implementing-OpenSSH-for-Secure-Remote-Communication-Comparing-Encrypted-Traffic/blob/main/SSH%20file%20setup.png) 

f. Find and uncomment following lines by removing the "#" at the beginning then save the file:

                   From this
                
                #Port 22
                
                #PasswordAuthentication yes
                
                   To This
                
                Port 22
                
                PasswordAuthentication yes

![image](https://github.com/forza-dc/Implementing-OpenSSH-for-Secure-Remote-Communication-Comparing-Encrypted-Traffic/blob/main/SSH%20Config%20File.png) 

We will run the below command on PowerShell with administrator privileges  to add the directory path "C:\Program Files\OpenSSH-Win64" to the system environment variable called PATH.

                setx PATH “$env:path;C:\Program Files\OpenSSH-Win64”-m

![image](https://github.com/forza-dc/Implementing-OpenSSH-for-Secure-Remote-Communication-Comparing-Encrypted-Traffic/blob/main/SSH%20Path%20addition.png) 

h. Change the OpenSSH directory and run the install script, This command will navigates to the OpenSSH directory and initiates the installation script for configuring the SSH server on Windows.

                cd "C:\Program Files\OpenSSH-Win64"; .\install-sshd.ps1



![image](https://github.com/forza-dc/Implementing-OpenSSH-for-Secure-Remote-Communication-Comparing-Encrypted-Traffic/blob/main/SSH%20Path%20addition.png) 

i. Enable automatic startup and start "sshd" and "ssh-agent" services on client side by running these commands,

         Set-Service sshd -StartupType Automatic;
         Set-Service ssh-agent -StartupType Automatic;
         Start-Service sshd;
         Start-Service ssh-agent
         
![image](https://github.com/forza-dc/Implementing-OpenSSH-for-Secure-Remote-Communication-Comparing-Encrypted-Traffic/blob/main/Services%20Status.png) 

j. Allow access to the Windows Firewall,

        New-NetFirewallRule -DisplayName "OpenSSH-Server-In-TCP" -Direction Inbound - LocalPort 22 -Protocol TCP -Action Allow

![image](https://github.com/forza-dc/Implementing-OpenSSH-for-Secure-Remote-Communication-Comparing-Encrypted-Traffic/blob/main/Access%20Srv%20Via%20SSH.png) 


## Step 4:
### Connecting to OpenSSH Server

On the system that will be acting as the client (Windows 10 PRO VM), type PowerShell in the search box, right-click Windows PowerShell, select Run As Administrator, and
click the Yes button. Execute the following command: "ssh username@servername"


![image](https://github.com/forza-dc/Implementing-OpenSSH-for-Secure-Remote-Communication-Comparing-Encrypted-Traffic/blob/main/Access%20Srv%20Via%20SSH.png) 











