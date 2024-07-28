---
title: Internet-based client management
titleSuffix: Configuration Manager
description: Create a plan to manage internet-based clients in Configuration Manager.
ms.date: 03/29/2022
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: conceptual
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Plan for internet-based client management in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use internet-based client management (IBCM) to manage Configuration Manager clients when they aren't connected to your internal network. Advantages of using IBCM:

- Full control of servers and roles providing the service
- No cloud service dependency
- May not require a virtual private network (VPN)
- All costs are associated with the on-premises service

Because of the higher security requirements of managing client computers on a public network, IBCM requires the use of PKI certificates. This configuration makes sure that connections are authenticated by an independent authority. When IBCM clients and site servers send data, it's encrypted and secure.  

## Client communications

The following site system roles at primary sites support connections from clients that are in untrusted locations:

> [!NOTE]
> While IBCM primarily focuses on the internet-based scenario, the same behaviors apply to clients in an untrusted Active Directory forest. Secondary sites don't support client connections from untrusted locations.

- Certificate registration point for the Configuration Manager policy module (NDES)

    > [!WARNING]
    > Starting in version 2203, the certificate registration point is no longer supported.<!--13951253--> For more information, see [Frequently asked questions about resource access deprecation](../../../protect/plan-design/resource-access-deprecation-faq.yml).

- Distribution point

- Content-enabled cloud management gateway (CMG)

- Enrollment proxy point

- Fallback status point

- Management point

- Software update point

### About internet facing site systems

There's no requirement to have a trust between a client's forest and that of the site system server. However, when the forest that contains an internet-facing site system trusts the forest that contains the user accounts, this configuration supports user-based policies for devices on the internet when you enable the **Client Policy** client setting **Enable user policy requests from internet clients**.

For example, the following configurations illustrate when IBCM supports user policies for devices on the internet:

- The internet-based management point is in the perimeter network. That network also has a read-only domain controller to authenticate the user. A firewall between the perimeter and internal networks allows Active Directory packets.

- The user account is in the intranet-based forest. The internet-based management point is in the perimeter-based forest. The perimeter forest trusts the internal forest. A firewall between the perimeter and internal networks allows the authentication packets.

- The user account and the internet-based management point are both in the intranet-based forest. You publish the management point to the internet with a web proxy server.

### Use a web proxy server

You can place internet-based site systems in the intranet when you publish them to the internet with a web proxy server. Configure these site systems for client connections from the internet only, or client connections from the internet and intranet. When you use a web proxy server, you can configure it for Secure Sockets Layer (SSL) bridging to SSL or SSL tunneling.

#### SSL bridging to SSL

SSL bridging to SSL is the recommended and more secure configuration, because it uses SSL termination with authentication. It authenticates client computers with computer authentication. Mobile devices that you enroll with Configuration Manager don't support SSL bridging.

With SSL termination at the proxy, it inspects packets from the internet before it forwards them to the internal network. The proxy authenticates the connection from the client, terminates it, and then opens a new authenticated connection to the internet-based site systems. When Configuration Manager clients use a proxy, the client securely contains its identity (GUID) in the packet payload. The management point doesn't consider the proxy to be the client. Configuration Manager doesn't support bridging with HTTP to HTTPS, or from HTTPS to HTTP.

> [!NOTE]
> Configuration Manager doesn't support setting third-party SSL bridging configurations. For example, Citrix Netscaler or F5 BIG-IP. Please work with your device vendor to configure it for use with Configuration Manager.

#### Tunneling

If your proxy web server can't support the requirements for SSL bridging, Configuration Manager also supports SSL tunneling. You can also use SSL tunneling to support mobile devices that you enroll with Configuration Manager. It's a less secure option because the proxy forwards the SSL packets from the internet to the site systems without SSL termination. The proxy doesn't inspect the packets for malicious content. When you use SSL tunneling, there are no certificate requirements for the proxy web server.

## Plan for internet-based clients

Decide whether to configure your internet-based clients for management on both the intranet and the internet, or for internet-only client management. You can only configure this management option during client installation. To change it later, reinstall the client.

> [!NOTE]
> If you configure a management point to support internet-based clients, clients that connect to this management point will become internet-capable when they next refresh their list of available management points.
>
> You don't have to restrict the configuration of internet-only client management to the internet. You can also use it on the intranet.

Clients that you configure for internet-only management only communicate with the site systems that you configure for client connections from the internet. Use this configuration in the following scenarios:

- For computers that you know will never connect to your intranet. For example, point of sale computers in remote locations.
- To restrict client communication to HTTPS only. For example, to support firewall and restricted security policies.
- When you install internet-based site systems in a perimeter network, and you want to manage these servers as Configuration Manager clients.

> [!NOTE]
> When you want to manage workgroup clients on the internet, install them as internet-only.
>
> When you configure a mobile device to use an internet-based management point, it automatically configures as internet-only.

You can configure other clients for both internet and intranet client management. When they detect a change of network, they automatically switch between IBCM and intranet client management. If these clients can find and connect to a management point that supports client connections on the intranet, these clients are managed as intranet clients. Intranet clients have full Configuration Manager functionality. If the clients can't find or connect to a management point that supports client connections on the intranet, they attempt to connect to an internet-based management point. If this action succeeds, these clients are then managed by the internet-based site systems in their assigned site.

The benefit in automatic switching is that clients can use all features when they connect to the intranet, and receive essential management when they're on the internet. Content download that begins on the internet can seamlessly resume on the intranet, and the other way around.

## Prerequisites

IBCM in Configuration Manager has the following dependencies:

- Clients require an internet connection. Configuration Manager uses the device's existing internet connection. Mobile devices must have a direct internet connection. Full client computers can have either a direct internet connection or connect by using a proxy web server.

- Site systems that support IBCM require an internet connection, and must be in an Active Directory domain. The internet-based site systems don't require a trust relationship with the Active Directory forest of the site server. However, when the internet-based management point can authenticate the user by using Windows authentication, it supports user policies. If Windows authentication fails, it only supports device policies.

    > [!NOTE]
    > To support user policies, also enable the following client settings in the **Client Policy** group:
    >
    > - **Enable user policy polling on clients**
    > - **Enable user policy requests from Internet clients**  

- A public key infrastructure (PKI) to deploy and manage the required certificates for internet-based clients and site system servers. For more information, see [PKI certificate requirements](../../plan-design/network/pki-certificate-requirements.md).

- Register public DNS host entries for the internet fully qualified domain names (FQDN) of site systems that support IBCM.

- Enable the option to **Use PKI client certificate (client authentication capability) when available** on the **Communication Security** tab of the site properties. This option is required.<!-- MEMDocs#1010 -->

### Client communication requirements

Intervening firewalls or proxy servers must allow the client communication for internet-based site systems:

- Support HTTP 1.1  

- Allow HTTP content type of multipart MIME attachment (multipart/mixed and application/octet-stream)  

#### Verbs

Allow the following verbs for the internet-based site system server roles:

| Role | Verbs |
|------|-------|
| Management point | - HEAD<br>- CCM_POST<br>- BITS_POST<br>- GET<br>- PROPFIND |
| Distribution point | - HEAD<br>- GET<br>- PROPFIND |
| Fallback status point | POST |

#### HTTP headers

Allow the following HTTP headers for the internet-based site system server roles:

| Role | HTTP headers |
|------|--------------|
| Management point | - Range:<br>- CCMClientID:<br>- CCMClientIDSignature:<br>- CCMClientTimestamp:<br>- CCMClientTimestampsSignature: |
| Distribution point | Range: |

For similar communication requirements when you use the software update point for client connections from the internet, see the documentation for Windows Server Update Services (WSUS).

## Unsupported features

Not all client management functionality is appropriate for the internet. Configuration Manager doesn't support some features for clients on the internet. These unsupported features typically rely on Active Directory Domain Services or aren't appropriate for a public network.

The following features aren't supported when you manage clients on the internet with IBCM:

- Client deployment over the internet, such as client push and software update-based client deployment. Use manual client installation.

- Automatic site assignment

- Wake-on-LAN

- OS deployment. However, you can deploy task sequences that don't deploy an OS.

- Remote control

- Software deployment to users. This feature relied upon the application catalog, which is no longer supported.

- Client roaming. Roaming enables clients to always find the closest distribution points to download content. Clients non-deterministically select one of the internet-based site systems, whatever the bandwidth or physical location.

When you configure a software update point to accept connections from the internet, internet-based clients always scan against this software update point to determine which software updates are required. When these clients are on the internet, they first try to download the software updates from Microsoft Update, rather than from an internet-based distribution point. If this behavior fails, they then try to download the required software updates from an internet-based distribution point.

> [!TIP]
> The Configuration Manager client automatically determines whether it's on the intranet or the internet. If the client can contact a domain controller or an on-premises management point, it sets its connection type to "Currently *intranet*". Otherwise, it switches to "Currently *internet*", and communicates with the site systems assigned to its site.
