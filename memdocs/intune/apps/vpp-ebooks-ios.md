---
# required metadata

title: Manage volume-purchased iOS/iPadOS eBooks
titleSuffix: Microsoft Intune
description: Learn about how you can sync books you purchased in volume from the iOS store into Intune and then manage and track their usage.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/27/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: f5617074-2384-4812-b913-dc94f64c0818

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: bryanke
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- iOS/iPadOS
---

# How to manage iOS/iPadOS eBooks you purchased through a volume-purchase program with Microsoft Intune


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

The Apple Volume Purchase Program (VPP) lets you purchase multiple licenses for a book that you want to distribute to users in your company. You can distribute books from the Business, or Education stores.

Microsoft Intune helps you synchronize, manage, and assign books that you purchased through this program. You can import license information from the store and track how many of the licenses you have used.

The procedures to manage books are similar to [managing VPP apps](vpp-apps-ios.md).

## Manage volume-purchased books for iOS devices
You acquire multiple licenses for iOS/iPadOS books through the [Apple Business Manager](https://business.apple.com/) or the [Apple School Manager](https://school.apple.com/). This process involves setting up an Apple Business Manager account from the Apple website and uploading the location token to Intune.  You can then synchronize your volume purchase information with Intune and track your volume-purchased book use.

## Before you start
Before you start, get a VPP token from Apple and upload it to your Intune account. Additionally:

* If you previously used a VPP token with a different product, you must generate a new one to use with Intune.
* Each token is valid for one year.
* By default, Intune syncs with the Apple Business Manager service twice a day. You can start a manual sync at any time.
* After you have imported the VPP token to Intune, don't import the same token to any other device management solution. Doing so might result in the loss of license assignment and user records.
* Before you start to use iOS/iPadOS books with Intune, remove any existing VPP user accounts created with other mobile device management (MDM) vendors. Intune doesn't synchronize those user accounts into Intune as a security measure. Intune synchronizes only data from the Apple Business Manager service that Intune created.
* When you assign a book to a device, that device must have the built-in iBooks app installed. If it isn't, the end user must reinstall the app before they can read the book. You can't currently use Intune to restore removed built-in apps.
* You can only assign books from the Apple Volume Purchase Program site. You can't upload, then assign books you created in-house.
* You can't currently assign books to end-user categories in the same way as you do apps.
* You can't reclaim a license once the book is assigned.
* When a user with an eligible device first tries to install a VPP book, they must join the Apple Volume Purchase program before they can install a book. You can also assign licenses to security groups with managed Apple IDs. If you do this, then users aren't prompted for their Apple ID when a book is installed.
* Devices must be enrolled with user affinity as e-books can only be assigned to user groups.   


## To get and upload an Apple Business Manager location token

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Tenant administration** > **Connectors and tokens** > **Apple VPP tokens**.
3. On the list of VPP tokens pane, click **Create**.
5. On the **New VPP Token** pane, specify the following information:
    - **VPP token file** - Ensure you have signed in to [Apple Business Manager](https://business.apple.com/) or [Apple School Manager](https://school.apple.com/). Note these services were previously known as Apple's volume purchase program for business or the Apple volume purchase program for education. Then, download the Apple location/VPP token for your account and select it in Intune.
    - **Apple ID** - Enter the Apple ID of the account associated with the volume-purchase program.
    - **Type of VPP account** - Choose from **Business** or **Education**.
5. When you're done, click **Create**.

The token is displayed in the list of tokens pane.


You can synchronize the data held by Apple with Intune at any time by choosing **Sync now**.

## To assign a volume-purchased app

1. Select **Apps** > **eBooks** > **All eBooks**.
2. On the list of books pane, choose the book you want to assign, and then choose '**...**' > **Assign Groups**.
3. On the <*book name*> - **Groups Assigned** pane, choose **Manage** > **Groups Assigned**.
4. Choose **Assign Groups** then, on the **Select groups** pane, choose the Microsoft Entra user groups to which you want to assign the book. Device groups are currently not supported.
Choose an assignment action of **Available**, or **Required**. 
5. Once you're done, choose **Save**.

## Next steps

See [How to monitor apps](apps-monitor.md) for information to help you monitor book assignments.
