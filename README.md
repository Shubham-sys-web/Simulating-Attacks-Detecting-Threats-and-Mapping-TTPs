# **Simulating Attacks, Detecting Threats, and Mapping TTPs**

![](https://miro.medium.com/v2/resize:fit:613/1*HrN2ZJDrUHLVSn4G8bBfIQ.png)

# **Summary**

This project provided hands-on experience with enterprise-style networks, enhancing my practical understanding of core cybersecurity concepts. Key highlights include:

- **Network Design**: Built a virtual network enabling seamless system communication.
- **Active Directory Administration**: Configured organizational units (OUs), managed user accounts, and implemented role-based access control (RBAC).
- **Simulating Attacks**: Executed TTPs using Kali Linux, Crowbar, and Atomic Red Team to replicate real-world threats.
- **Log Monitoring and Analysis**: Utilized Splunk to collect and analyze logs, detect suspicious activity, and map incidents to MITRE ATT&CK techniques.

This lab reinforced critical skills in secure network design, structured user management, and proactive monitoring, foundational for organizational security and threat detection.

# **Architecture**

![](https://miro.medium.com/v2/resize:fit:700/0*1kjQzbRXgXzmsnWd.png)

To begin, I created a network architecture diagram using draw.io to map the connections between servers, switches, and machines. This visualization outlined roles for each component, including the Active Directory server, Splunk server, Windows 10 target machine, and Kali Linux attacker machine. Planning this architecture ensured organized project execution and provided a clear understanding of how components would interact in my domain environment, aligning with real-world enterprise IT practices.

# **Tools & Tech**

**Workflow Software**: draw.io

**Virtualization**: Oracle VirtualBox

**Target:** Win 10, Splunk Universal Forwarder, Sysmon, Atomic Red Team

**Attacker:** Kali Linux VM, Crowbar

**Splunk Server:** Ubuntu Server

**Active Directory:** Win Server 2022, Splunk Universal Forwarder, Sysmon

***Download Link Below required things;***

> Video Link: https://youtu.be/2cEj3bS5C0Q?si=KM_NVhHe0uXlBesI
> 
> 
> ***Oracle VirtualBox:** https://www.virtualbox.org/wiki/Downloads*
> 
> ***Server 2022 ISO:** https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022*
> 
> ***Windows 10 ISO :** https://www.microsoft.com/en-us/software-download/windows10*
> 
> ***Ubuntu Server 24.04.2 LTS** : https://ubuntu.com/download/server*
> 

Here I setup My all machine

## **Objective**

> Install & Configure
> 
> 
> ***Sysmon & Splunk***
> 
> ***Windows target Machine <Windows Server***
> 

First Click on **Tools** then Click on bullet **Point**

![](https://miro.medium.com/v2/resize:fit:463/1*nhwZMJ8U8ULIyyKVVvmCYA.png)

Select **Network**

![](https://miro.medium.com/v2/resize:fit:448/1*aakmEOIRuU66DiJskjyk3w.png)

First Select here Nat network

![](https://miro.medium.com/v2/resize:fit:700/1*iAZWVGHENd0_fa62F7hpwg.png)

click on create

![](https://miro.medium.com/v2/resize:fit:700/1*6ndN9unXClF3OEdW4JMM4A.png)

Set the **Ipv4** According to the **architecture click on apply**

![](https://miro.medium.com/v2/resize:fit:700/1*WZmyKQBorYUMg_t887UGuA.png)

Now we create our own **AD-POJECT**

![](https://miro.medium.com/v2/resize:fit:700/1*mYyI9qU07xEDmjUbuxw12w.png)

Click On Settings now we change our Network settings to Nat network

![](https://miro.medium.com/v2/resize:fit:700/1*M9nSZSTm4VMh3mWasgLmSQ.png)

Click on Networks

![](https://miro.medium.com/v2/resize:fit:662/1*xk1SM-amoD7-XuLqpEa5Ww.png)

change to **NAT to NAT Network**

![](https://miro.medium.com/v2/resize:fit:494/1*4ms9JTtOYHrerV3HawR77Q.png)

click on ok

![](https://miro.medium.com/v2/resize:fit:639/1*m7JHC5fmit9ahliq8NURVA.png)

**Doings same process for all virtual machine remaining Windows ISO ,Sever 2022 ,Kali**

This is the my ip of **Ubuntu Server**

![](https://miro.medium.com/v2/resize:fit:700/1*XP2DJFyS_aVv41PD7_3b6g.png)

**Now we set our Static IP in Ubuntu that reflect our network ip**

![](https://miro.medium.com/v2/resize:fit:388/1*gJY6djhLZ4ch40PjkFNE7g.png)

I configured the static IP setting for Ubuntu/Splunk Server VM.

```
# This is the network config written by 'subiquity'
network:
  ethernets:
    enp0s3:
      dhcp4: no
      addresses: [192.168.1.10/24]
      nameservers:
        addresses: [8.8.8.8]
      routes:
        - to: default
          via: 192.168.1.1
  version: 2
```

![](https://miro.medium.com/v2/resize:fit:441/1*vBXR2UBg7lPXH2DQkncABw.png)

Then Run this Command

![](https://miro.medium.com/v2/resize:fit:468/1*b5hR0cDyr-aD8TnzuTgaAw.png)

Now You can see here my static **IP**

![](https://miro.medium.com/v2/resize:fit:700/1*yofw6G2bSp79F4czO_OMJA.png)

My Ping is also work

![](https://miro.medium.com/v2/resize:fit:700/1*mQO4ZYVGusxwPXKdh3AXIA.png)

**I downloaded Splunk on my host machine, setup a shared folder, and used the .deb file to install Splunk on the Ubuntu/Splunk Server VM. I also configured the Ubuntu Server to run Splunk upon each boot.**

![](https://miro.medium.com/v2/resize:fit:700/1*vIyeREIKgDKe64NeENtbMw.png)

![](https://miro.medium.com/v2/resize:fit:516/1*L1bvngoW_BD_bTIIxC5Xdg.png)

Click on **Plus sign**

![](https://miro.medium.com/v2/resize:fit:637/1*obfxTdMj_QfLcsbyi6L5YA.png)

I Give here Folder path where I save my splunk

![](https://miro.medium.com/v2/resize:fit:490/1*wC6yJK0GMcZDXSDA5pA8jg.png)

then run this

![](https://miro.medium.com/v2/resize:fit:246/1*7jqdYRJlucUF4A9UnnRDrw.png)

run this

![](https://miro.medium.com/v2/resize:fit:529/1*uW3zlYn1tp2wNyDMR11ctA.png)

after install reboot system one more time

![](https://miro.medium.com/v2/resize:fit:405/1*Yhyw0ztslo8umImISS_uxw.png)

I make a share directory

![](https://miro.medium.com/v2/resize:fit:603/1*yJkrfFC7PFqPDOhq7e3lyQ.png)

I shared my Splunk file run this commad

![](https://miro.medium.com/v2/resize:fit:700/1*QkX0BEIU81aNKgPPh1CVuw.png)

do ls -la

![](https://miro.medium.com/v2/resize:fit:613/1*J-cdTLNoqS9-YuemwtGIoQ.png)

Go share directory

![](https://miro.medium.com/v2/resize:fit:700/1*NhZk-rzY-spYmiG1KP7c1g.png)

Here I installed my splunk server run this command

![](https://miro.medium.com/v2/resize:fit:660/1*sl42JnkX3eXN0-cim8E6qQ.png)

go this directory to run your splunk server

![](https://miro.medium.com/v2/resize:fit:700/1*5wV5kAhp2BQ8n4b_SbOYmw.png)

run according to the

![](https://miro.medium.com/v2/resize:fit:427/1*2YpP0veaMJMirK6GHJPDHQ.png)

You can see the my server is running now

![](https://miro.medium.com/v2/resize:fit:700/1*v__kneKamHHKoYCXEzK2vg.png)

Here I change my host IP according to the my ubuntu Ip Follow this command

```
cd /opt/splunk/etc
nano splunk-launch.conf
BINDIP = 0.0.0.0    #add this line
```

after this run

![](https://miro.medium.com/v2/resize:fit:635/1*pCs-B4tFEzpsvGP6hnGSkg.png)

Here I run my splunk server in Windows 10 machine successfully run

![](https://miro.medium.com/v2/resize:fit:671/1*deZwHVp6UccziIl6UE5o8w.png)

**splunk forwarder windows 10 target machine**

**change target machine name pc**

![](https://miro.medium.com/v2/resize:fit:682/1*llIWXC9DsAloRAnr1i8-ig.png)

Click on Rename this PC

![](https://miro.medium.com/v2/resize:fit:451/1*Tx3nECxwshJys1GhUTfX-Q.png)

here my target Ip means windows 10

![](https://miro.medium.com/v2/resize:fit:578/1*4HZyxOcm_Y4HuTYL6Liejw.png)

I convert **Dynamic IP in static IP**

**click on Network 2**

![](https://miro.medium.com/v2/resize:fit:356/1*6_SNRWJNL-1FSj8MKe6XWw.png)

**click on change adapter options**

![](https://miro.medium.com/v2/resize:fit:570/1*oIsiN_lXB4S_7Q-PIBdNDQ.png)

Right click on Ethernet on click on properties

![](https://miro.medium.com/v2/resize:fit:397/1*5lwWnjHR2VeP701dV_MYBA.png)

Double click on IPv4

![](https://miro.medium.com/v2/resize:fit:363/1*cYwbBih0ROBhkcq5kewZkQ.png)

Set According to the **architecture** click on ok

![](https://miro.medium.com/v2/resize:fit:399/1*acIOSeqHjmFvmNYZ5lTZvg.png)

Now You can see here my **static IP**

![](https://miro.medium.com/v2/resize:fit:542/1*ASO6cjT8uA1XebKedNHBRg.png)

# **Installing/Configuring Sysmon and Splunk on the Windows 10 Target VM & Windows Server VM**

**Here I installed splunk Universal forwarder**

![](https://miro.medium.com/v2/resize:fit:700/1*toruInw4nt9bKZ646GcYyA.png)

Set according to the diagram all

![](https://miro.medium.com/v2/resize:fit:499/1*CAGba1eOQQK52voESyCKCA.png)

![](https://miro.medium.com/v2/resize:fit:498/1*9CGiQzCDsC-syAomzMxpbg.png)

deployment server we don’t have leave it

![](https://miro.medium.com/v2/resize:fit:490/1*BtCODr9j93iEcQQsw1ATwA.png)

I set here my splunk server IP

![](https://miro.medium.com/v2/resize:fit:493/1*dDYvCXTqefmNeoBFypB68Q.png)

click on install

![](https://miro.medium.com/v2/resize:fit:492/1*6p4r7MQ7T7M2XmNxHa4Jqw.png)

**Download Sysmon**

# **🔍 What is Sysmon?**

**Sysmon (System Monitor)** is a Windows system service and device driver that logs important events for security monitoring and threat detection. It is part of Microsoft Sysinternals.

When installed, Sysmon can log events like:

- Process creation
- Network connections
- File creation
- Registry changes
- Process injection

![](https://miro.medium.com/v2/resize:fit:700/1*mwI_CqUxGbdU4Ej0NAQjpg.png)

But by default, **Sysmon doesn’t log much**. That’s where a **good configuration file** comes in.

# **🛠️ What is OLAF Config?**

**OLAF config** is a custom configuration file created by security expert **Olaf Hartong**. It tells Sysmon **exactly what to log**, and **how to log only useful events** while ignoring unnecessary ones.

# **🔑 Why is OLAF config important?**

Without a config:

- Sysmon logs only basic events.
- Many important attacks go undetected.
- Too much noise and useless logs.

With OLAF config:

- Logs important attack behaviors (like PowerShell abuse, privilege escalation, etc.).
- Maps events to **MITRE ATT&CK** techniques (used by attackers).
- Makes threat detection and alerting easier in tools like **Splunk** or **SIEMs**.

![](https://miro.medium.com/v2/resize:fit:650/1*yauiDIorPJhChe97csXqhg.png)

Click on sysmonconfig.xml file

![](https://miro.medium.com/v2/resize:fit:646/1*xTrsZhYX5v99ufP-Sn4C0w.png)

clcik on raw

![](https://miro.medium.com/v2/resize:fit:645/1*Mq9fwMn5ADXNs0HQfgPpxw.png)

save as sysmonconfig

![](https://miro.medium.com/v2/resize:fit:700/1*knXcsUoKwNKypF1KultiCQ.png)

here I save in this directory

![](https://miro.medium.com/v2/resize:fit:700/1*ae6RT93S6Rv2PFRTT19FYw.png)

I downloaded and installed Sysmon using PowerShell and the olaf config file found on Github.

Sysmon using PowerShell and the olaf config file found on Github.

run this command

```
.\Sysmon64.exe -i ..\sysmonconfig.xml
```

![](https://miro.medium.com/v2/resize:fit:700/0*S7buEJcCvcPwewpG.png)

Here my sysmon is succesfully installed

![](https://miro.medium.com/v2/resize:fit:266/1*wVuphulVowp-XxQXKWs8DA.png)

After My splunk forwarder Installed follow this path means go to this directory

```
C:\Program Files\SplunkForwarder\etc\system\default

#Right click on Iputs.conf and copy it
```

![](https://miro.medium.com/v2/resize:fit:686/1*33pvrCyjeulbj4mHvQRfmw.png)

Then Run notepad as a administrator

![](https://miro.medium.com/v2/resize:fit:259/1*VHaFKjI3rqbjH_HKNNMgTQ.png)

and paste it from here inputs.conf file https://github.com/MyDFIR/Active-Directory-Project save it this directory

```
C:\Program Files\SplunkForwarder\etc\system\local
```

![](https://miro.medium.com/v2/resize:fit:502/1*YuKdw3bQdBdcIWJcp_PFjg.png)

This configuration is used in **Windows 10** to collect important **Windows Event Logs** and send them to a **SIEM** like **Splunk**, usually through the **Splunk Universal Forwarder**.

# **🔹 Explanation:**

- `[WinEventLog://Application]` – Collects application-related logs (e.g., crashes, errors).
- `[WinEventLog://Security]` – Collects security logs (e.g., login attempts, user changes).
- `[WinEventLog://System]` – Collects system logs (e.g., shutdowns, service issues).
- `[WinEventLog://Microsoft-Windows-Sysmon/Operational]` – Collects **Sysmon logs**, which are critical for detecting attacker behavior (e.g., process creation, network activity).

All logs are sent to the **`endpoint` index** in Splunk.

`renderXml = true` ensures logs are collected in **XML format** for better detail and MITRE ATT&CK mapping.

![](https://miro.medium.com/v2/resize:fit:670/1*RqvSD9WaWm7LWuXQTvuSIw.png)

I changed the service logon account from **`NT SERVICE\SYSTEM`** to **`Local Service`** while testing permission restrictions. I wanted to see how the service behaves with **limited privileges** and whether it can still access event logs like **Security** and **Sysmon**. This change helped me understand the importance of using **proper service accounts** for log collection and detection in tools like Splunk.

![](https://miro.medium.com/v2/resize:fit:700/1*yzvEvnk7r7jewGKy5Rcjiw.png)

This is set now NT service

![](https://miro.medium.com/v2/resize:fit:411/1*caEd2iKMvXCF2YX7tZ_wLg.png)

Then You can see this I change in Local system

![](https://miro.medium.com/v2/resize:fit:413/1*X8tyB2ozNrr9362b5tuTYg.png)

Now You can see my changes

![](https://miro.medium.com/v2/resize:fit:494/1*ZGYt36oBxnsbKGpiil-A_g.png)

After restart the service

![](https://miro.medium.com/v2/resize:fit:499/1*aPdItAO2O9Q_f-StpYMXcA.png)

Now we Our Sysmon and Splunk Forwarder Installed our with updated File

**Go to the Splunk server click on settings click on indexes for create endpoints and set port recievings logs**

![](https://miro.medium.com/v2/resize:fit:613/1*opN4_ncoAOugdTs0D7WO_Q.png)

You can see this all indexes click on new indexes

![](https://miro.medium.com/v2/resize:fit:700/1*R3J5YYyVB48JvVe3q_xbzQ.png)

give the name of this endpoint

![](https://miro.medium.com/v2/resize:fit:700/1*P7D2M-ZL_CEWBvIJ1BG6pA.png)

this is my endpoint

![](https://miro.medium.com/v2/resize:fit:667/1*BaXGuCPa9WrN8-zAESiGOA.png)

now we enable our splunk server to recieve our data

click on settings forwarding and recievings

![](https://miro.medium.com/v2/resize:fit:700/1*6YfMb467TKXXYOmD5ZBqqg.png)

This is the default port hit save

![](https://miro.medium.com/v2/resize:fit:700/1*ySmHaBUk5mkQy_CBG57P6w.png)

![](https://miro.medium.com/v2/resize:fit:700/1*HixYThFybXIlTVxrTVLwUg.png)

Go the top select search and reporting

![](https://miro.medium.com/v2/resize:fit:346/1*VqUytTj1fMfP0MUVsHGo9g.png)

If u search index = endpoint

![](https://miro.medium.com/v2/resize:fit:594/0*0aUujin6P9IdO5Lj.png)

The sources defined on our inputs.conf file are also shown here under source.

![](https://miro.medium.com/v2/resize:fit:700/0*f2ePnRgMmsuji0Tx.png)

Installing/Configuring Sysmon and Splunk on the Windows 10 Target VM & Windows Server AD VM: The sources defined on our inputs.conf file are also shown here under source.

## **Active directory setup**

**install and configure windows server 2022**

**Active Directory Promote Domain Controller**

**Our Target Machine (Windows Pc) join Our newely created Domain**

First set our static ip on click network in bottom

![](https://miro.medium.com/v2/resize:fit:333/1*yJQfRHyJpSiqYZbh8yTKYQ.png)

click on change adapter settings

![](https://miro.medium.com/v2/resize:fit:559/1*-uimz3-NlOaX5S34IMytmw.png)

change the name

![](https://miro.medium.com/v2/resize:fit:267/1*1rCxbz-dRjQQJGJKRLASKg.png)

set static ip

![](https://miro.medium.com/v2/resize:fit:392/1*x7DHbkBPDTWRIc9DcximgQ.png)

see the ip of machine

![](https://miro.medium.com/v2/resize:fit:550/1*j7UiWGm0INqjqJPzQgdogg.png)

click on add role

![](https://miro.medium.com/v2/resize:fit:700/1*JxuQVJwxPp5-cgzlwK-0Sg.png)

select accordings to the diagram click on next, next

![](https://miro.medium.com/v2/resize:fit:700/1*On42Cdz-5IRhekb8sPa0qA.png)

After end of install you can see this in yellow line

![](https://miro.medium.com/v2/resize:fit:582/1*_deQUIIYaYQEtb77zzARbg.png)

Then click on triangle means danger sign and click on yellow painted

![](https://miro.medium.com/v2/resize:fit:700/1*TxPbRpwBC_OSpKeFjbMezw.png)

Set our new domain **mydfir.local**

![](https://miro.medium.com/v2/resize:fit:700/1*wnI4M6DDwuXXFmDe2dpCSg.png)

set our password

![](https://miro.medium.com/v2/resize:fit:700/1*MKrRK_V55sobCm-Bzumfaw.png)

after click on next,next,next and install it then restart system

you can see my domain name

![](https://miro.medium.com/v2/resize:fit:700/1*PApuubX-_dFkuZaNJDkaqQ.png)

click on yellow painted to add user nad group

![](https://miro.medium.com/v2/resize:fit:700/1*XwFG-TYvOAZVKk2uKZboJw.png)

Right click on domain click on new then organizatonal unit

![](https://miro.medium.com/v2/resize:fit:694/1*Q4Ad6gyqi6X1cjULR32LtA.png)

Give the name IT

![](https://miro.medium.com/v2/resize:fit:434/1*SyiV5lMk2es1j_MXEeZm4w.png)

![](https://miro.medium.com/v2/resize:fit:582/1*kWIHwxVoVC0SQv7iNfrgwA.png)

Right click on IT

![](https://miro.medium.com/v2/resize:fit:513/1*0JmGl2dQsZe1noky-tjs8Q.png)

![](https://miro.medium.com/v2/resize:fit:428/1*T5WmY6ncmJ-pSby_kmN1jA.png)

Installing and configuring Active Directory on Windows Server 2022: I created two new Organizational Units and 1 new user for each unit

![](https://miro.medium.com/v2/resize:fit:437/1*ma-8Sjdfs9FqZu1dzlwyMA.png)

![](https://miro.medium.com/v2/resize:fit:363/1*WpDl_5A06PxJudKDl1Ahrw.png)

**: I created two new Organizational Units and 1 new user for each unit.**

![](https://miro.medium.com/v2/resize:fit:700/0*aURWF1aOOcC88Hmw.png)

## **Now we move the target Windows machine to join our newly Domain created mydfir.local**

Go the Pc — About_advance System settings

clicl on computer name

![](https://miro.medium.com/v2/resize:fit:674/1*vfDmMmr9a8YjDGUCokaqog.png)

but hre one problem is my dns configuration is wrong

![](https://miro.medium.com/v2/resize:fit:700/1*TbY0COQQf5g29wNpxHZ3ag.png)

On the **Windows target VM,** I configured the preferred DNS server to domain controller IP address so it could resolve the domain address MYDFIR.LOCAL.

![](https://miro.medium.com/v2/resize:fit:700/1*ixkeTHuDsdNnX9Pqow9mfg.png)

change the yellow painted

![](https://miro.medium.com/v2/resize:fit:687/1*-c9W1oTb9FqL62Tmtl3-rw.png)

Set Accordings to this

![](https://miro.medium.com/v2/resize:fit:366/1*RN-QGBr6yWgd51z1yy5oPg.png)

Now You can see this my IP here

![](https://miro.medium.com/v2/resize:fit:667/1*S9ccMpRLmNr2072bmRrq5g.png)

after this doing same process in about PC this time give your useranme and password (we created user before on Server) this time connect you PC with Domain **MYDFIR.LOCAL** Here I Joined newly created domain

![](https://miro.medium.com/v2/resize:fit:700/1*AvnDNdBIPWHJN416xpQJEA.png)

**Then Restart Your PC(Target Machine)**

Here I authenticated Terry Smith’s account to log in the Windows target VM

![](https://miro.medium.com/v2/resize:fit:700/0*VKafVXhxBpbNLp9F.png)

# **MITRE ATT&CK T1110.001: Attack**

# **🔐 MITRE ATT&CK T1110.001 — Brute Force: Password Guessing**

This technique involves an attacker **repeatedly guessing usernames and passwords** to gain access to accounts. The attacker may use **common or leaked credentials** in tools or scripts to try logging into services like:

- SSH
- RDP
- FTP
- Web logins

Once successful, they can **gain access to the system** or move laterally.

**Go the Kali Linux After Active Directory Setup**

**Brute Force Attack**

**View Telemetry via splunk**

**setup & Install ART**

Right click on network to setup our static IP on kali network

![](https://miro.medium.com/v2/resize:fit:304/1*Z0_vS4BXlXgWaP5E7GBh5w.png)

click on painted yellowsettings

![](https://miro.medium.com/v2/resize:fit:649/1*OnyuS9drZ0wtspQxKNU4Gw.png)

change DHCP To static IP

![](https://miro.medium.com/v2/resize:fit:700/1*uz4RuyozkA2HZ1i84Eqe1w.png)

Save Dns server

![](https://miro.medium.com/v2/resize:fit:693/1*u1eIZYrmJFJsI38VX1FG3Q.png)

but ip was not change the click on disconnect

![](https://miro.medium.com/v2/resize:fit:700/1*-VFbsAYni3hhqRS6sIZF6w.png)

Again Click on Wired Connection 1

![](https://miro.medium.com/v2/resize:fit:198/1*YiG1OZtSwH5F_f8Zpih4Nw.png)

Now IP is successfully set

![](https://miro.medium.com/v2/resize:fit:636/1*zVNtFWMFEHRjbeDBGJ33cw.png)

make A project

![](https://miro.medium.com/v2/resize:fit:313/1*Yf-ksA9pSdCgrLDBGfN2UQ.png)

Follow this step

![](https://miro.medium.com/v2/resize:fit:554/1*YUR3LZNaCehjGLPcza4i3A.png)

I took the first 20 passwords from the rockyou.txt file and created a passwords.txt file for the brute force attack. I also added the passwords used for the target machine, the active directory machine, and the two users created in active directory.

![](https://miro.medium.com/v2/resize:fit:351/1*A_YunZ7QGTVxjeeXyV14oA.png)

![](https://miro.medium.com/v2/resize:fit:391/1*4YB9BRRGwATSSeQX7bHxwA.png)

set your Original Passwords in Last

![](https://miro.medium.com/v2/resize:fit:123/1*TTB0DOAriR50IjKklNXTeA.png)

then I enabled remote desktop for both active directory users on the target machine.

![](https://miro.medium.com/v2/resize:fit:700/0*VbFEcKo6MlW6uZuG.png)

I ran crowbar using the rdp function, password.txt file, and the target IP address. The brute force attempt on user tsmith was successful as you can see it shared the correct password

![](https://miro.medium.com/v2/resize:fit:700/0*3MaSQWc9Pz-Z3zq8.png)

then I logged into Splunk and searched for event codes related to the user tsmith. We see that Splunk recorded 20 instances of event code 4625 otherwise known as unsuccessful login attempts and 1 instance of event code 4624 otherwise known as successful login.

![](https://miro.medium.com/v2/resize:fit:700/0*qM-NXkee6VNqBimK.png)

Here we see that there were multiple instances of event code 4625 at the same time, that should grab your attention

Event ID 4625 indicates a failed logon attempt on a Windows system. It logs the details of unsuccessful login attempts, including the reason for failure (e.g., incorrect username or password, disabled account)

![](https://miro.medium.com/v2/resize:fit:700/0*YInUyjm6PW9T7Szm.png)

If we look at an instance of 4624, we see our attacker machine name and IP address listed

Event ID 4624 indicates a successful logon to a Windows system. It logs details like the username, domain, logon type, and source IP, providing a record of who logged on and when. This event is a common occurrence and usually signifies normal user activity.

![](https://miro.medium.com/v2/resize:fit:700/0*C2FYxPjR9Jhpj7PW.png)

## **Now We Istalled Our Atomic Red Teams (ART)**

## **🆔 MITRE ATT&CK T1136 — Create Account**

**Definition:**

Attackers create **new user accounts** on a system to maintain **access**, **escalate privileges**, or **blend in** with normal users. These accounts can be **local**, **domain**, or **cloud** accounts.

## **🔗 How T1136 is Related to Atomic Red Team (ART) and Windows**

## **🔸 What is Atomic Red Team (ART)?**

**Atomic Red Team** is a project that lets you **simulate real-world ATT&CK techniques** (like T1136) on your system — **safely and in a controlled way**.

# **🧪 Why run this on Windows?**

Running this atomic test helps you:

**1.Simulate a real attack** safely.

**2.Generate logs** in:

- Security Event Log (Event ID 4720 — User Account Created)
- Sysmon (if configured)

**3.Test your detections** in tools like:

- **Splunk**
- **Elastic**
- **SIEMs**

**4.Verify if alerts trigger properly** when such behavior happens

Running PowerShell as an administrator on the target machine, I updated the execution policy. I also created an exclusion rule on Windows Defender before installing Atomic Red Team.

**Using PowerShell to install Atomic Red Team.**

First Run

```
Set-ExecutionPolicy Bypass CurrentUser   #then go to the below click on threats
```

![](https://miro.medium.com/v2/resize:fit:616/1*q2e82f0Vm4Ji82Wl-dk3-Q.png)

Then go the below click on threats

![](https://miro.medium.com/v2/resize:fit:179/1*IB9yqa5V1sfxAiG4ymiz9g.png)

click on virus and threat

![](https://miro.medium.com/v2/resize:fit:393/1*uJsWI4b6BpwhjvtMXH_CtA.png)

Then click on manage settings

![](https://miro.medium.com/v2/resize:fit:333/1*pbmn6TxO89MKtBw2ImhdeQ.png)

Go down under exclusion click on add

![](https://miro.medium.com/v2/resize:fit:344/1*1rzJlY4fUxsdXb9bwAW08g.png)

Then click on select Folder simply

![](https://miro.medium.com/v2/resize:fit:373/1*VJiiBd1Aou7_Q7G7A2JWcg.png)

select C: drive

![](https://miro.medium.com/v2/resize:fit:420/1*EuJw7kXC_36cdjevwNQFCw.png)

Then we login Again as a administrator

![](https://miro.medium.com/v2/resize:fit:254/1*ZShCUeNTd6F2uMGIFvoamg.png)

Now You can see my C: drive

![](https://miro.medium.com/v2/resize:fit:276/1*aZ_mupbBd7rVdxjgYyJ7Zw.png)

Now we installing our red team

![](https://miro.medium.com/v2/resize:fit:576/1*Ph_UOOkg-15eDLYGxX_5Qw.png)

after installing under C:\ drive

![](https://miro.medium.com/v2/resize:fit:512/1*e1RSNMs6b3g0KbSRPbIrcQ.png)

under Atomics

![](https://miro.medium.com/v2/resize:fit:488/1*JDZi8sb5G89hadh1DOhIsw.png)

You can see all mapping rules

![](https://miro.medium.com/v2/resize:fit:538/1*pG1uwRJmCUWK_VA7r9ldgw.png)

If You go the Mitre-Attack framework this highlight our technique id

![](https://miro.medium.com/v2/resize:fit:695/1*TR2JrjXQtsU3uns_owODeg.png)

then we create account **T1136**

![](https://miro.medium.com/v2/resize:fit:661/1*Bfh3BwD4df1e228rGJauaQ.png)

If u go In C:\ under technique id might be something about this id

![](https://miro.medium.com/v2/resize:fit:499/1*z5ODvpdA2U6AVW--E8Sxog.png)

**Lets go on MITRE- FRAMEWORK**

You can see this here

![](https://miro.medium.com/v2/resize:fit:700/1*rXj3piW-QmIL4gWmNBYJXw.png)

If u Run this command automatically create user

```
Invoke-AtomicTest T1136.001
```

![](https://miro.medium.com/v2/resize:fit:578/1*PjIA7d1tr03yTwTXfq3WmQ.png)

: I used Atomic Red Team to create telemetry by using the MITRE T1136 technique to create a new local user.

![](https://miro.medium.com/v2/resize:fit:700/0*JomMUlT1OtRxCovG.png)

But If u Go the splunk server endpoint not detect thistime after wait You can see this for more se this two videos mydfir https://youtu.be/orq-OPIdV9M?si=R4eCHSuhVZxwFBMS

# **MITRE ATT&CK T1136: Splunk**

![](https://miro.medium.com/v2/resize:fit:700/0*7LaNoSgOCKfdKkfm.png)

Run Atomic Tests w/ Atomic Red Team: I used Atomic Red Team to create telemetry by using the MITRE T1136 technique to create a new local user. Here Splunk detected the new user being created under event code 4720.

# **Conclusion & Lessons Learned**

This project involved generating simulated attacks and analyzing telemetry in Splunk to detect anomalies and potential threats. Using Splunk dashboards, I correlated events like logins and user creation activities with MITRE ATT&CK techniques, reinforcing my ability to map telemetry to TTPs and transform raw data into actionable threat intelligence.

Ultimately, this project bridged theoretical knowledge with real-world application, allowing me to approach cybersecurity challenges from both attacker and defender perspectives. By combining offensive and defensive security practices, I developed a strong foundation in Active Directory, SIEM tools, and incident detection. This experience highlights the value of practical labs in building industry-relevant cybersecurity expertise, preparing me to address complex challenges in a professional environment.
