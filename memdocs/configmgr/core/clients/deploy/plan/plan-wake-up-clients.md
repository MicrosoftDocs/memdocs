---
title: Waking up clients
titleSuffix: Configuration Manager
description: Plan how to wake up clients in Configuration Manager using Wake On LAN (WOL).
ms.date: 04/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---
# Plan how to wake up clients in Configuration Manager

*Applies to: Configuration Manager (current branch)*

 Configuration Manager supports traditional wake-up packets to wake up computers in sleep mode when you want to install required software, such as software updates and applications.

> [!NOTE]
> This article describes how an older version of Wake on LAN functions. This functionality still exists in Configuration Manager version 1810, which also includes a newer version of Wake on LAN too. Both versions of Wake on LAN can, and in many cases will, be enabled simultaneously. For more information about how the new version of Wake on LAN functions starting in 1810 and enabling either or both versions, see [How to configure Wake on LAN](../configure-wake-on-lan.md).  

## How to wake up clients in Configuration Manager

 Configuration Manager supports traditional wake-up packets to wake up computers in sleep mode when you want to install required software, such as software updates and applications.  

You can supplement the traditional wake-up packet method by using the wake-up proxy client settings. Wake-up proxy uses a peer-to-peer protocol and elected computers to check whether other computers on the subnet are awake, and to wake them if necessary. When the site is configured for Wake On LAN and clients are configured for wake-up proxy, the process works as follows:  

1. Computers with the Configuration Manager client installed and that aren't asleep on the subnet check whether other computers on the subnet are awake. They do this check by sending each other a TCP/IP ping command every five seconds.  

2. If there's no response from other computers, they're assumed to be asleep. The computers that are awake become *manager computer* for the subnet.  

    Because it's possible that a computer might not respond because of a reason other than it's asleep (for example, it's turned off, removed from the network, or the proxy wake-up client setting is no longer applied), the computers are sent a wake-up packet every day at 2 P.M. local time. Computers that don't respond will no longer be assumed to be asleep and will not be woken up by wake-up proxy.  

    To support wake-up proxy, at least three computers must be awake for each subnet. To achieve this requirement, three computers are non-deterministically chosen to be *guardian computers* for the subnet. This state means that they stay awake, despite any configured power policy to sleep or hibernate after a period of inactivity. Guardian computers honor shutdown or restart commands, for example, as a result of maintenance tasks. If this action happens, the remaining guardian computers wake up another computer on the subnet so that the subnet continues to have three guardian computers.  

3. Manager computers ask the network switch to redirect network traffic for the sleeping computers to themselves.  

    The redirection is achieved by the manager computer broadcasting an Ethernet frame that uses the sleeping computer's MAC address as the source address. This behavior makes the network switch behave as if the sleeping computer has moved to the same port that the manager computer is on. The manager computer also sends ARP packets for the sleeping computers to keep the entry fresh in the ARP cache. The manager computer also responds to ARP requests on behalf of the sleeping computer and replies with the MAC address of the sleeping computer.  

   > [!WARNING]  
   >  During this process, the IP-to-MAC mapping for the sleeping computer remains the same. Wake-up proxy works by informing the network switch that a different network adapter is using the port that was registered by another network adapter. However, this behavior is known as a MAC flap and is unusual for standard network operation. Some network monitoring tools look for this behavior and can assume that something is wrong. Consequently, these monitoring tools can generate alerts or shut down ports when you use wake-up proxy.  
   >   
   >  Do not use wake-up proxy if your network monitoring tools and services do not allow MAC flaps.  

4. When a manager computer sees a new TCP connection request for a sleeping computer and the request is to a port that the sleeping computer was listening on before it went to sleep, the manager computer sends a wake-up packet to the sleeping computer, and then stops redirecting traffic for this computer.  

5. The sleeping computer receives the wake-up packet and wakes up. The sending computer automatically retries the connection and this time, the computer is awake and can respond.  

   Wake-up proxy has the following prerequisites and limitations:  

> [!IMPORTANT]  
>  If you have a separate team that is responsible for the network infrastructure and network services, notify and include this team during your evaluation and testing period. For example, on a network that uses 802.1X network access control, wake-up proxy will not work and can disrupt the network service. In addition, wake-up proxy could cause some network monitoring tools to generate alerts when the tools detect the traffic to wake-up other computers.  

-   All Windows operating systems listed as supported clients in [Supported operating systems for clients and devices](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md) are supported for Wake On LAN.  

-   Guest operating systems that run on a virtual machine are not supported.  

-   Clients must be enabled for wake-up proxy by using client settings. Although wake-up proxy operation does not depend on hardware inventory, clients do not report the installation of the wake-up proxy service unless they are enabled for hardware inventory and submitted at least one hardware inventory.  

-   Network adapters (and possibly the BIOS) must be enabled and configured for wake-up packets. If the network adapter is not configured for wake-up packets or this setting is disabled, Configuration Manager will automatically configure and enable it for a computer when it receives the client setting to enable wake-up proxy.  

-   If a computer has more than one network adapter, you cannot configure which adapter to use for wake-up proxy; the choice is non-deterministic. However, the adapter chosen is recorded in the SleepAgent_<DOMAIN\>@SYSTEM_0.log file.  

-   The network must allow ICMP echo requests (at least within the subnet). You cannot configure the five-second interval that is used to send the ICMP ping commands.  

-   Communication is unencrypted and unauthenticated, and IPsec is not supported.  

-   The following network configurations are not supported:  

    -   802.1X with port authentication  

    -   Wireless networks  

    -   Network switches that bind MAC addresses to specific ports  

    -   IPv6-only networks  

    -   DHCP lease durations less than 24 hours  

If you want to wake up computers for scheduled software installation, you must configure each primary site to use wake-up packets.  

 To use wake-up proxy, you must deploy Power Management wake-up proxy client settings in addition to configuring the primary site.  

Decide whether to use subnet-directed broadcast packets, or unicast packets, and what UDP port number to use. By default, traditional wake-up packets are transmitted by using UDP port 9, but to help increase security, you can select an alternative port for the site if this alternative port is supported by intervening routers and firewalls.  

## Choose Between Unicast and Subnet-Directed Broadcast for Wake-on-LAN  
 If you chose to wake up computers by sending traditional wake-up packets, you must decide whether to transmit unicast packets or subnet-direct broadcast packets. If you use wake-up proxy, you must use unicast packets. Otherwise, use the following table to help you determine which transmission method to choose.  

|Transmission method|Advantage|Disadvantage|  
|-------------------------|---------------|------------------|  
|Unicast|More secure solution than subnet-directed broadcasts because the packet is sent directly to a computer instead of to all computers on a subnet.<br /><br /> Might not require reconfiguration of routers (you might have to configure the ARP cache).<br /><br /> Consumes less network bandwidth than subnet-directed broadcast transmissions.<br /><br /> Supported with IPv4 and IPv6.|Wake-up packets do not find destination computers that have changed their subnet address after the last hardware inventory schedule.<br /><br /> Switches might have to be configured to forward UDP packets.<br /><br /> Some network adapters might not respond to wake-up packets in all sleep states when they use unicast as the transmission method.|  
|Subnet-Directed Broadcast|Higher success rate than unicast if you have computers that frequently change their IP address in the same subnet.<br /><br /> No switch reconfiguration is required.<br /><br /> High compatibility rate with computer adapters for all sleep states, because subnet-directed broadcasts were the original transmission method for sending wake-up packets.|Less secure solution than using unicast because an attacker could send continuous streams of ICMP echo requests from a falsified source address to the directed broadcast address. This causes all of the hosts to reply to that source address. If routers are configured to allow subnet-directed broadcasts, the additional configuration is recommended for security reasons:<br /><br /> -   Configure routers to allow only IP-directed broadcasts from the Configuration Manager site server, by using a specified UDP port number.<br />-   Configure Configuration Manager to use the specified non-default port number.<br /><br /> Might require reconfiguration of all intervening routers to enable subnet-directed broadcasts.<br /><br /> Consumes more network bandwidth than unicast transmissions.<br /><br /> Supported with IPv4 only; IPv6 is not supported.|  

> [!WARNING]  
>  There are security risks associated with subnet-directed broadcasts: An attacker could send continuous streams of Internet Control Message Protocol (ICMP) echo requests from a falsified source address to the directed broadcast address, which cause all the hosts to reply to that source address. This type of denial of service attack is commonly called a smurf attack and is typically mitigated by not enabling subnet-directed broadcasts.
