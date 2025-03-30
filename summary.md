Title: Learn the Basics of Penetration Testing
Tier 0 (The Key is a Strong Foundation)

## Overview
- **Objective:**  
Learn to set up virtual network system
Learn Nmap to identify open ports
Learn basics of Linux command line interface

## Lab Description
In this lab we are introduced to the basics of virtual machine simulation and Linux. Linux is an operating system - like Windows or MacOS, that is often used by cybersecurity professionals for the wide range of tools for cybersecurity works. For this instance, we are trying to connect to a target machine and testing out various reconnaissance methods.

Using OpenVPN, we test our connection to our target machine provided by Hack-The-Box by using a simple ping function on the generated IP address:

ping 192.168.1.254

Of course, this IP address - 192.168.1.254 is made up. Please refer to the IP given by Hack-The-Box.

If the ping is successful, you should receive ping response:

XX Bytes from 192.168.1.254: icmp_seq=1 ttl=63 time=X.XX ms

If not, you should troubleshoot your connection. Find out more on how to troubleshoot your connection.

After this, the lab explains the setup of the target, explaining that "ports" are the first area to scan as it is the mode of communication between systems. This is also where we are introduced to "nmap", a powerful tool that we will learn more about in the task below.

Once we have determined that ping is successful a.k.a we have connection to the target computer, we will open a command line interface and key in:
sudo nmap -sV <XX.XXX.XXX.XX>

sudo is a command to raise your privilege to super user, or the high level. In this case there is no password required so it just runs the command as usual. Certain commands are not allowed to run on users with lower privilege.

nmap is a command to execute the network mapping tool

-sV is service version, which scans open ports and probe the services that are running on these ports. It will also identify the version numbers, so that it helps us find out what is running exactly behind a port. Common ports to be scanned are port 22 that is running ssh, a common version of ssh is OpenSSH 7.6p1. Another common port is port 80, running HTTP service, which could be running Apache httpd version.

In this case, we should receive the result of an open port, on port 23, running telnet.

The idea is to run the nmap scan on all ports to see where we can pick up a vulnerable spot. In this case it was telnet service that was not disabled. The lab encourages us to google different services to find out known vulnerability to test them.

The next step was to try to run the telnet service by the following command:

telnet <target-ip>

We should receive some response which requires us to key in a user and a password. The lab then uses some of the oldest and simplest way to "hack" into the account - trying common usernames and passwords. The lab listed:

admin
administrator
root

some other default usernames can also be:
user
guest
support

or even admin1

Once you are able to login using "root", we can poke around the system. It is as if you have access to the folders. For Linux, you have to use the command "ls" - which means list, to show the documents available. Once you run ls, you should see a flag.txt.

to "open" a file, you need to use the command cat
cat flag.txt

You should find a string of random text, which might be hexadecimal key since there is a mix of alphabets and numbers, and the alphabets generally do not go beyond "f". After this step, you would have completed the lab and you should be able to answer the questions below:

## Tasks
Task 1
What does the acronym VM stand for?
ans: Virtual Machine
Explanation: As in VMware

Task 2
What tool do we use to interact with the operating system in order to issue commands via the command line, such as the one to start our VPN connection? It's also known as a console or shell.
ans: Terminal
Explanation: It is an official term for the "way" to input our commands, and get the computer to execute it, normally by pressing enter.

Task 3
What service do we use to form our VPN connection into HTB labs?
ans: OpenVPN
Explanation: It is just one of the many ways to connect to the destination machine. OpenVPN uses web based application (common known as webapp) to simulate a Virtual Machine environment without us actually requiring to download VirtualBox or VMware. Pretty nifty tool.

Task 4
What tool do we use to test our connection to the target with an ICMP echo request?
ans: Ping
Explanation: ICMP stands for Internet Control Message Protocol, used to send error messages and operational information. NOTE: It is not the protocol to transmit data, just status info.
ICMP echo request is a two way handshake - by executing a ping command, we are requesting a response from the target machine (using its ip), whereby the target machine will respond, which is what we see in the results of pinging the destination machine.

Task 5
What is the name of the most common tool for finding open ports on a target?
ans: nmap
Explanation: nmap stands for Network Mapper. It is a powerful tool to scan host for their online status, discover open ports, detect services and versions, identify operating systems and even run vulnerability scans using Nmap scripting engine.

Task 6
What service do we identify on port 23/tcp during our scans?
ans: telnet
Explanation: Telnet is short for teletype network. This is a network protocol to remotely access and manage device through a command-line interface, such as a CLI from Linux OS. Telnet is on port 23 by default which technically can be configured to run on other ports. Telnet was used to manage multiple machines by command lines, but was soon heavily exploited so that it became a common target to be hardened. Either through instilling strict credentials - uncommon username and complicated passwords, shifting of telnet port, or even disabling the service altogether.

Task 7
What username is able to log into the target over telnet with a blank password?
ans: root
Explanation: As mentioned, there are some common usernames used by default which is a bad practice. But the headache is to remember usernames and passwords so for unimportant instances, IT professionals opt to use default usernames. This however becomes something they take for granted, which is also an opportunity for exploitation, which worked in our favor in this case. Imagine if they changed the username and password to a secure format.

Task 8
Submit root flag
ans: XXXXXXXXXXXXXXXXXXXXXXXXXXXX4c19
Explanation: If you have followed the lab so far, it is not difficult to read the flag.txt. It should be a 32 hexadecimal number (string of numbers that contains 0-9, A-F. Infact the answer is in the lab FGS.