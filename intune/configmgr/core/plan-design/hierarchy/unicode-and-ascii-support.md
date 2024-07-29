---
title: Unicode and ASCII support
titleSuffix: Configuration Manager
description: Learn about support for Unicode and ASCII characters in Configuration Manager objects.
ms.date: 12/01/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: reference
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Unicode and ASCII support in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration Manager creates most objects by using Unicode characters. However, several objects only support ASCII characters, or they have other limitations.

## Objects that use ASCII characters

When you create the following objects, Configuration Manager only supports the ASCII character set:

- Site code

- All site system server computer names

- The following Configuration Manager accounts:

    > [!NOTE]
    > These accounts support ASCII characters, and RUS characters on a site that runs in Russian.

  - Client push installation account

  - Management point database connect account

  - Network access account

  - Package access account

  - Standard sender account

  - Site system installation account

  - Software update point connection account

  - Software update point proxy server account

    > [!NOTE]
    > The accounts that you specify for role-based administration support Unicode.
    >
    > The reporting services point account supports Unicode, with the exception of RUS characters.

- Fully qualified domain name (FQDN) for site servers and site systems

- Installation path for Configuration Manager

- SQL Server instance name

- The path for the following site system roles:

  - Enrollment point

  - Enrollment proxy point

  - Reporting services point

  - State migration point

- The path for the following folders:

  - The folder that stores client state migration data

  - The folder that contains the Configuration Manager reports

  - The folder that stores the Configuration Manager backup

  - The folder that stores the installation source files for site setup

  - The folder that stores the prerequisite downloads for use by setup

- The path for the following objects:

  - IIS website

  - Virtual application installation path

  - Virtual application name

- Boot media ISO file names

- [Custom property](../../../develop/adminservice/custom-properties.md) _names_<!-- 12377169 -->

## Other limitations

The following limitations are for supported character sets and language versions:

- Configuration Manager doesn't support changing the locale of the site server computer.

- An enterprise certificate authority (CA) doesn't support client computer names that use double-byte character sets (DBCS). The client computer names that you can use are restricted by the PKI limitation of the IA5 character set. Configuration Manager doesn't support CA names or subject name values that use DBCS.

## Objects that aren't localized

The Configuration Manager database supports Unicode for most objects that it stores. When possible, it displays this information in the OS language that matches the locale of a computer. For the client interface or Configuration Manager console to display information in the computer's OS language, the computer's locale must match a client or server language that you install at a site.

Several Configuration Manager objects don't support Unicode. They're stored in the database by using ASCII, or they have other language limitations. This information is always displayed by using the ASCII character set, or in the language that was in use when you created the object.

## Next steps

[Language packs in Configuration Manager](../../servers/deploy/install/language-packs.md)
