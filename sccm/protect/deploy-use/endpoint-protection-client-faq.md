---
title: "Endpoint Protection client frequently asked questions"
description: "Get answers to frequently asked questions about Windows Defender and Endpoint Protection."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3aaa9d2-a40e-42b1-ad75-5a115351729e
caps.latest.revision: 15
author: NathBarnms.author: nathbarnmanager: angrobe

---
# Endpoint Protection client frequently asked questions*Applies to: System Center Configuration Manager (Current Branch)*

This FAQ is for computer users whose IT administrator has deployed Windows Defender or Endpoint Protection to their managed computer. The content here might not apply to other antimalware software. Microsoft System Center Endpoint Protection manages Windows Defender on Windows 10. It can also deploy and manage the Endpoint Protection client to computers before Windows 10. While Windows Defender is described in this article, its information also applies to Endpoint Protection.  

-   [Why do I need antivirus and antispyware software?](#why-do-i-need-antivirus-and-antispyware-software)  
-   [How can I tell if my computer is infected with malicious software?](#how-can-i-tell-if-my-computer-is-infected-with-malicious-software)
-   [How can I find the version of Windows Defender?](#how-can-i-find-the-version-of-windows-defender)
-   [What should I do if Windows Defender or Endpoint Protection detects malicious software on my computer?](#what-should-i-do-if-windows-defender-or-endpoint-protection-detects-software-on-my-computer)  
-   [What is a virus?](#what-is-a-virus)  
-   [What is a spyware?](#what-is-spyware)  
-   [What's the difference between viruses, spyware, and other potentially harmful software?](#hat-s-the-difference-between-viruses-spyware-and-other-potentially-harmful-software)  
-   [Where do viruses, spyware, and other potentially unwanted software come from?](#where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from)  
-   [Can I get malicious software without knowing it?](#can-i-get-malicious-software-without-knowing-it)  
-   [Why is it important to review license agreements before installing software?](#why-is-it-important-to-review-license-agreements-before-installing-software)  
-   [What's the difference between Endpoint Protection and Windows Defender?](#what-s-the-difference-between-endpoint-protection-and-windows-defender)  
-   [Why doesn't Windows Defender detect cookies?](#why-doesn-t-windows-defender-detect-cookies)  
-   [How can I prevent malware?](#how-can-i-prevent-malware)  
-   [What are virus and spyware definitions?](#what-are-virus-and-spyware-definitions)  
-   [How do I keep virus and spyware definitions up to date?](#how-do-i-keep-virus-and-spyware-definitions-up-to-date)  
-   [How do I remove or restore items quarantined by Windows Defender or Endpoint Protection?](#how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection)  
-   [What is real-time protection?](#what-is-real-time-protection)  
-   [How do I know that Windows Defender or Endpoint Protection is running on my computer?](#how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer)
-   [How to set up Windows Defender or Endpoint Protection alerts?](#how-to-set-up-windows-defender-or-endpoint-protection-alerts)  

##  Why do I need antivirus and antispyware software?  

 It is critical to make sure that your computer is running software that protects against malicious software. Malicious software, which includes viruses, spyware, or other potentially unwanted software can try to install itself on your computer any time you connect to the Internet. It can also infect your computer when you install a program using a CD, DVD, or other removable media. Malicious software, can also be programmed to run at unexpected times, not just when it is installed.  

 Windows Defender or Endpoint Protection offers three ways to help keep malicious software from infecting your computer:  

-   **Using real-time protection** - Real-time protection enables Windows Defender to monitor your computer all the time and alert you when malicious software, including viruses, spyware, or other potentially unwanted software attempts to install itself or run on your computer. Windows Defender then suspends the software and enables you to you to follow its recommendation on the software or take an alternative action.  

    |**Real-time protection option** |**Purpose** |

    |-|-|  
    |Scan all downloads|This option monitors files and programs that are downloaded, including files that are automatically downloaded via Windows Internet Explorer and Microsoft Outlook® Express, such as ActiveX® controls and software installation programs. These files can be downloaded, installed, or run by the browser itself. Malicious software, including viruses, spyware, and other potentially unwanted software, can be included with these files and installed without your knowledge.<br /><br /> Using the real-time protection option, Windows Defender monitors your computer all the time and checks for any malicious files or programs that you may have downloaded. This monitoring feature means that Windows Defender doesn't need to slow down your browsing or e-mail experience by requiring a check of any files or programs you may want to download.|  
    |Monitor file and program activity on your computer|This option monitors when files and programs start running on your computer, and then it alerts you about any actions they perform and actions taken on them. This is important, because malicious software can use vulnerabilities in programs that you have installed to run malicious or unwanted software without your knowledge. For example, spyware can run itself in the background when you start a program that you frequently use. Windows Defender monitors your programs and alerts you if it detects suspicious activity.|  
    |Enable behavior monitoring|This option monitors collections of behavior for suspicious patterns that might not be detected by traditional antivirus detection methods.|  

    |Enable Network Inspection System|This option helps protect your computer against "zero day" exploits of known vulnerabilities, decreasing the window of time between the moment a vulnerability is discovered and an update is applied.|  

-   **Scanning options** - You can use Windows Defender to scan for potential threats, such as viruses, spyware, and other malicious software that might put your computer at risk. You can also use it to schedule scans on a regular basis and to remove malicious software that is detected during a scan.  

-   **Microsoft Active Protection Service community** - The online Microsoft Active Protection Service community helps you see how other people respond to software that has not yet been classified for risks. You can use this information to help you choose whether to allow this software on your computer. In turn, if you participate, your choices are added to the community ratings to help other people decide what to do.  

##  How can I tell if my computer is infected with malicious software?  

 You might have some form of malicious software, including viruses, spyware, or other potentially unwanted software, on your computer if:  

-   You notice new toolbars, links, or favorites that you did not intentionally add to your Web browser.  

-   Your home page, mouse pointer, or search program changes unexpectedly.  

-   You type the address for a specific site, such as a search engine, but you are taken to a different Web site without notice.  

-   Files are automatically deleted from your computer.  

-   Your computer is used to attack other computers.  

-   You see pop-up ads, even if you're not on the Internet.  

-   Your computer suddenly starts running more slowly than it usually does. Not all computer performance problems are caused by malicious software, but malicious software, especially spyware, can cause a noticeable change.  

There might be malicious software on your computer even if you don't see any symptoms. This type of software can collect information about you and your computer without your knowledge or consent. To help protect your privacy and your computer, you should run Windows Defender or Endpoint Protection at all times.  

## How can I find the version of Windows Defender?
 To view the version of Windows Defender running on your computer, open Windows Defender (click **Start** and then search for **Windows Defender**), click **Settings**, and scroll to the bottom of the Windows Defender settings to find **Version info**.

##  What should I do if Windows Defender or Endpoint Protection detects malicious software on my computer?  

 If Windows Defender detects malicious software or potentially unwanted software on your computer (either when monitoring your computer using real-time protection or after running a scan), it notifies you about the detected item by displaying a notification message in the bottom right-hand corner of your screen.  

 The notification message includes a **Clean computer** button and a **Show details** link that lets you view additional information about the detected item. Click the **Show details** link to open the **Potential threat details** window to get additional information about the detected item. You can now choose which action to apply to the item, or click **Clean computer**. If you need help determining which action to apply to the detected item, use the alert level that Windows Defender assigned to the item as your guide (for more information see, Understanding alert levels).  

 Alert levels help you choose how to respond to viruses, spyware, and other potentially unwanted software. While Windows Defender will recommend that you remove all viruses and spyware, not all software that is flagged is malicious or unwanted. The following information can help you decide what to do if Windows Defender detects potentially unwanted software on your computer.  

 Depending on the alert level, you can choose one of the following actions to apply to the detected item:  

-   **Remove** - This action permanently deletes the software from your computer.  

-   **Quarantine** - This action quarantines the software so that it can't run. When Windows Defender quarantines software, it moves it to another location on your computer, and then prevents the software from running until you choose to restore it or remove it from your computer.  

-   **Allow** - This action adds the software to the Windows Defender allowed list and allows it to run on your computer. Windows Defender will stop alerting you to risks that the software might pose to your privacy or to your computer.  

 If you choose **Allow** for an item, such as software, Windows Defender will stop alerting you to risks that the software might pose to your privacy or to your computer. Therefore, add software to the allowed list only if you trust the software and the software publisher.  

### How to remove potentially harmful software

To remove all unwanted or potentially harmful items that Windows Defender detects quickly and easily, use the **Clean computer** option.  

1.  When you see the notification message that  displays in the Notification area after it detects potential threats, click **Clean computer**.  

2.  Windows Defender removes the potential threat (or threats), and then notifies you when it's finished cleaning your computer.  

3.  To learn more about the detected threats, click the **History** tab, and then select **All detected items**.  

4.  If you don't see all the detected items, click **View details**. If you're prompted for an administrator password or confirmation, type the password or confirm the action. On systems running Windows XP, you may need to log on as an administrator on this computer.  

> [!NOTE]  
>  During computer cleanup, whenever possible, Windows Defender removes only the infected part of a file, not the entire file.  

##  What is a virus?  
 Computer viruses are software programs deliberately designed to interfere with computer operation, to record, corrupt, or delete data, or to infect other computers throughout the Internet. Viruses often slow things down and cause other problems in the process.  

##  What is spyware?  
 Spyware is software that can install itself or run on your computer without getting your consent or providing you with adequate notice or control. Spyware might not display symptoms after it infects your computer, but many malicious or unwanted programs can affect how your computer runs. For example, spyware can monitor your online behavior or collect information about you (including information that can identify you or other sensitive information), change settings on your computer, or cause your computer to run slowly.  

##  What's the difference between viruses, spyware, and other potentially harmful software?  
 Both viruses and spyware are installed on your computer without your knowledge and both have the potential to be intrusive and destructive. They also have the ability to capture information on your computer and damage or delete that information. They both can negatively affect your computer's performance.  

 The main differences between viruses and spyware is how they behave on your computer. Viruses, like living organisms, want to infect a computer, replicate, and then spread to as many other computers as possible. Spyware, however, is more like a mole - it wants to "move into" your computer and stay there as long as possible, sending valuable information about your computer to an outside source while it is there.  

##  Where do viruses, spyware, and other potentially unwanted software come from?  
 Unwanted software, such as viruses, can be installed by Web sites or by programs that you download or that you install using a CD, DVD, external hard disk, or a device. Spyware is most commonly installed through free software, such as file sharing, screen savers, or search toolbars.  

##  Can I get malicious software without knowing it?  
 Yes, some malicious software can be installed from a website through an embedded script or program in a webpage. Some malicious software requires your help to install it. This software uses Web pop-ups or free software that requires you to accept a downloadable file. However, if you keep Microsoft Windows® up to date and don't reduce your security settings, you can minimize the chances of an infection.  

##  Why is it important to review license agreements before installing software?  
 When you visit websites, do not automatically agree to download anything the site offers. If you download free software, such as file sharing programs or screen savers, read the license agreement carefully. Look for clauses that say that you must accept advertising and pop-ups from the company, or that the software will send certain information back to the software publisher.  

##  What's the difference between Endpoint Protection and Windows Defender?  
 Endpoint Protection is antimalware software, which means that it's designed to detect and help protect your computer against a wide range of malicious software, including viruses, spyware, and other potentially unwanted software. Windows Defender, which is automatically installed with your Windows operating system, is software that detects and stops spyware.  

##  Why doesn't Windows Defender detect cookies?  
 Cookies are small text files that websites put on your computer to store information about you and your preferences. Websites use cookies to offer you a personalized experience and to gather information about website use. Windows Defender doesn't detect cookies because it doesn't consider them a threat to your privacy or to the security of your computer. Most internet browser programs allow you to block cookies.  

##  How can I prevent malware?  
 Two of the biggest concerns for computer users today are viruses and spyware. In both cases, while these can be a problem, you can defend yourself against them easily enough with just a little bit of planning:  

-   Keep your computer's software current and remember to install all patches. Remember to update your operating system on a regular basis.  

-   Make sure your antivirus and antispyware software, Windows Defender, is using the latest updates again potential threats (see How do I keep virus and spyware definitions up to date?). Also make sure you're always using the latest version of Windows Defender.  

-   Only download updates from reputable sources. For Windows operating systems, always go to [Microsoft Update](http://go.microsoft.com/fwlink/?LinkID=96304) (http://go.microsoft.com/fwlink/?LinkID=96304) and for other software always use the legitimate websites of the company or person who produces it.  

-   If you receive an e-mail with an attachment and you're unsure of the source, then you should delete it immediately. Don't download any applications or files from unknown sources, and be careful when trading files with other users.  

-   Install and use a firewall. It is recommended that you enable Windows Firewall.  

##  What are virus and spyware definitions?  
 When you use Windows Defender or Endpoint Protection, it is important to have up-to-date virus and spyware definitions. Definitions are files that act like an ever-growing encyclopedia of potential software threats. Windows Defender or Endpoint Protection uses definitions to determine if software that it detects is a virus, spyware, or other potentially unwanted software, and then to alert you to potential risks. To help keep your definitions up to date, Windows Defender or Endpoint Protection works with Microsoft Update to install new definitions automatically as they are released. You can also set Windows Defender or Endpoint Protection to check online for updated definitions before scanning.  

##  How do I keep virus and spyware definitions up to date?  
 Virus and spyware definitions are files that act like an encyclopedia of known malicious software, including viruses, spyware, and other potentially unwanted software. Because malicious software is continually being developed, Windows Defender or Endpoint Protection relies on up-to-date definitions to determine if software that is trying to install, run, or change settings on your computer is a virus, spyware, or other potentially unwanted software.  

### To automatically check for new definitions before scheduled scans (recommended)  

1.  Open Windows Defender or Endpoint Protection client by clicking the icon in the notification area or launching it from the **Start** menu.  

2.  Click **Settings**, and then click **Scheduled scan**.  

3.  Make sure the **Check for the latest virus and spyware definitions before running a scheduled scan** check box is selected, and then click **Save changes**. If you're prompted for an administrator password or confirmation, type the password or confirm the action.  

### To check for new definitions manually

 Windows Defender or Endpoint Protection updates the virus and spyware definitions on your computer automatically. If the definitions haven't been updated for over seven days (for example, if you didn't turn on your computer for a week), Windows Defender or Endpoint Protection will notify you that the definitions are out of date.  

1.  Open Windows Defender or Endpoint Protection client by clicking the icon in the notification area or launching it from the **Start** menu.  

2.  To check for new definitions manually, click the **Update** tab and then click **Update definitions**.  

##  How do I remove or restore items quarantined by Windows Defender or Endpoint Protection?  

 When Windows Defender or Endpoint Protection quarantines software, it moves the software to another location on your computer, and then it prevents the software from running until you choose to restore it or to remove it from your computer.  

 For all the steps mentioned in this procedure, if you're prompted for an administrator password or confirmation, type the password or provide confirmation.  

###  To remove or restore items quarantined by Windows Defender or Endpoint Protection


1.  Click the **History** tab, select **Quarantined items**, and then select the **Quarantined items** option.  

2.  Click **View details** to see all of the items.  

3.  Review each item, and then for each, click **Remove** or **Restore**. If you want to remove of the all quarantined items from your computer, click **Remove All**.  

##  What is real-time protection?  

 Real-time protection enables Windows Defender to monitor your computer all the time and alert you when potential threats, such as viruses and spyware, are trying to install themselves or run on your computer. Because this feature is an important element of the way that Windows Defender helps protect your computer, you should make sure real-time protection is always turned on. If real-time protection gets turned off, Windows Defender notifies you, and changes your computerâ€™s status to â€œAt riskâ€.  

 Whenever real-time protection detects a threat or potential threat, Windows Defender displays a notification. You can now choose from the following options:  

-   Click **Clean computer** to remove the detected item. Windows Defender will automatically remove the item from your computer.  

-   Click the **Show details** link to display the Potential threat details window, and then choose which action to apply to the detected item.  

 You can choose the software and settings that you want Windows Defender to monitor, but we recommend that you turn on real-time protection and enable all real-time protection options. The following table explains the available options.  

|||  
|-|-|  
|**Real-time protection option**|**Purpose**|  
|Scan all downloads|This option monitors files and programs that are downloaded, including files that are automatically downloaded via Windows Internet Explorer and Microsoft Outlook® Express, such as ActiveX® controls and software installation programs. These files can be downloaded, installed, or run by the browser itself. Malicious software, including viruses, spyware, and other potentially unwanted software, can be included with these files and installed without your knowledge.<br /><br /> Using the real-time protection option, Windows Defender monitors your computer all the time and checks for any malicious files or programs that you may have downloaded. This monitoring feature means that Windows Defender doesn't need to slow down your browsing or e-mail experience by requiring a check of any files or programs you may want to download.|  
|Monitor file and program activity on your computer|This option monitors when files and programs start running on your computer, and then it alerts you about any actions they perform and actions taken on them. This is important, because malicious software can use vulnerabilities in programs that you have installed to run malicious or unwanted software without your knowledge. For example, spyware can run itself in the background when you start a program that you frequently use. Windows Defender monitors your programs and alerts you if it detects suspicious activity.|  
|Enable behavior monitoring|This option monitors collections of behavior for suspicious patterns that might not be detected by traditional antivirus detection methods.|  
|Enable Network Inspection System|This option helps protect your computer against â€œzero dayâ€ exploits of known vulnerabilities, decreasing the window of time between the moment a vulnerability is discovered and an update is applied.|  

### To turn off real-time protection  

1.  Click **Settings**, and then click **Real-time protection.**  

2.  Clear the real-time protection options you want to turn off, and then click **Save changes**. If you're prompted for an administrator password or confirmation, type the password or confirm the action.  

##  How do I know that Windows Defender or Endpoint Protection is running on my computer?  

 After you install Windows Defender on your computer, you can close the main window and let Windows Defender run quietly in the background. Windows Defender will continue running on your computer, monitor it, and help protect it against threats.  

 Of course, you'll know that Windows Defender is running whenever it displays notification messages in the notification area. These notifications alert you to potential threats that Windows Defender has detected.  

 You'll also receive other alert notifications, for example, if for some reason real-time protection has been turned off, if you haven't updated your virus and spyware definitions for a number of days, or when upgrades to the program become available. Windows Defender also briefly displays a notification to let you know that it's scanning your computer.  

> [!TIP]  

>If you don't see the Windows Defender icon in the notification area, click the arrow in the notification area to show hidden icons, including the Windows Defender icon.  


 The icon color depends on your computer's current status:  

-   Green indicates that your computer's status is "protected."  

-   Yellow indicates that your computer's status is "potentially unprotected."  

-   Red indicates that your computer's status is "at risk."  

##  How to set up Windows Defender or Endpoint Protection alerts?  
 When Windows Defender is running on your computer, it automatically alerts you if it detects viruses, spyware, or other potentially unwanted software. You can also set Windows Defender to alert you if you run software that has not yet been analyzed, and you can choose to be alerted when software makes changes to your computer.  

### To set up alerts  

1.  Click **Settings**, and then click **Real-time protection.**  

2.  Make sure the **Turn on real-time protection (recommended)** check box is selected.  

3.  Select the check boxes next to the real-time protections options you want to run, and then click **Save changes**. If you're prompted for an administrator password or confirmation, type the password or confirm the action.  

### See also  
 [Troubleshooting Windows Defender or Endpoint Protection client](troubleshoot-endpoint-client.md)   

 [Endpoint Protection Client Help](endpoint-protection-client-help.md)
