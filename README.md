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
