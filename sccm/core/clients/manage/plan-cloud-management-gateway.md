---
title: "Plan for cloud management gateway | Microsoft Docs"
description: ""
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology:
  - configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: Mtillman
ms.author: mtillman
manager: angrobe
---

# Plan for cloud management gateway in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Beginning in version 1610, cloud management gateway provides a simple way to manage Configuration Manager clients on the Internet. The cloud management gateway service, which is deployed to Microsoft Azure and requires an Azure subscription, connects to your on-premises Configuration Manager infrastructure using a new role called the cloud management gateway connector point. Once it's completely deployed and configured, clients will be able to access on-premises Configuration Manager site system roles regardless of whether they're connected to the internal private network or on the Internet.

You use the Configuration Manager console to deploy the service to Azure, add the cloud management gateway connector point role, and configure site system roles to allow cloud management gateway traffic. Cloud management gateway currently only supports the management pointand software update point roles.

Client certificates and Secure Socket Layer (SSL) certificates are required to authenticate computers and encrypt communications between the different layers of the service. Client computers typically receive a client certificate through group policy enforcement. To encrypt the traffic between clients and site system server hosting the roles, you need to create a custom SSL certificate from the CA. In addition to these two types of certificates, you also need set up a management certificate on Azure that allows Configuration Manager to deploy the cloud management gateway service.

## Requirements for cloud management gateway

-   Client computers and the site system server running the cloud management gateway connector point.

-   Custom SSL certificates from the internal CA - used to encrypt communication from the client computers and authenticate the identity of the cloud management gateway service.

-   Azure subscription for cloud services.

-   Azure management certificate - used to authenticate Configuration Manager with Azure.

## Limitations of cloud management gateway

-   Cloud management gateway only supports the management point and software update point roles.

-   The following features in Configuration Manager are currently unsupported for cloud management gateway:

    -   Client deployment and upgrade using client push

    -   Automatic site assignment

    -   User policies

    -   Application catalog (including software approval requests)

    -   Full operating system deployment (OSD)

    -   Configuration Manager console

    -   Remote tools

    -   Reporting website

    -   Wake on LAN

    -   Mac, Linux, and UNIX clients

    -   Azure Resource Manager

    -   Peer cache

    -   On-premises Mobile Device Management

## Cost of cloud management gateway

>[!IMPORTANT]
>The cost information provided below is for estimating purposes only. Your environment may have other variables that affect the overall cost of using cloud management gateway.

Cloud management gateway uses the following Microsoft Azure functionality, which incurs charges to the Azure subscription account:

-   Virtual machine

    -   Cloud management gateway currently requires a Standard\_A2 virtual machine. When creating the service, you can select how many VMs to support the service (one is the default).

    -   For estimating purposes only, expect that a single Azure Standard\_A2 virtual machine can support approximately 2,000 simultaneous Internet-based clients.

    -   See the [Azure pricing calculator](https://azure.microsoft.com/en-us/pricing/calculator/) to help determine potential costs.

      >[!NOTE]
      >Virtual machine costs vary by region.

-   Outbound data transfer

    -   Charges are incurred for data flowing out of the service.. See the [Azure bandwidth pricing details](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) to help determine potential costs.

    -   For estimating purposes only, expect approximately 100 MB per client per month for Internet-based clients doing policy refreshes every hour.

    >[!NOTE]
    > Performing other actions supported via the cloud management gateway (for example, deploying software updates or applications) will increase the amount of outbound data transfer from Azure.

-   Content storage

    -   Internet-based clients managed with cloud management gateway will get software update content from Windows Update at no charge.

    -   Any other necessary content (for example, applications) must be distributed to a cloud-based distribution point. Currently, cloud management gateway does not support using a standard distribution point site system role for sending content to clients.

    - See the cost of using a [cloud-based distribution](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution) for more details.

## Next steps

[Set up cloud management gateway](setup-cloud-management-gateway.md)
