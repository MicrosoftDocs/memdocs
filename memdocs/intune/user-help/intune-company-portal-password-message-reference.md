---
# required metadata

title: Intune Company Portal device password messages | Microsoft Docs
description: This article lists the Company Portal device password messages for devices running Windows, Android, macOS, and iOS/iPadOS, with information about how to resolve them.    
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/08/2024 
ms.topic: end-user-help
ms.localizationpriority: high
ms.service: microsoft-intune
ms.subservice: end-user
searchScope:
 - User help


# optional metadata

ROBOTS:  
#audience:

ms.reviewer: anuragjain 
#ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser 
ms.collection:
- tier3
---
 
# Device password messages in Company Portal   

 **Applies to**:  
 * Windows 10  
 * Windows 11  
 * Android  
 * iOS/iPadOS  
 * macOS    

This article lists the password-related messages you could receive from Intune Company Portal. These messages appear on devices during and after device enrollment, and enforce your organization's device password requirements. If you receive one or more of these messages, you may be blocked from accessing your org's network until you change your password settings. This article gives a brief description on how to fix your settings to meet each requirement. For more specific information about your organization's policies, contact your IT support person. Sign into the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980) or app to find your organization's helpdesk information.  

Messages in this article are organized by operating system.  

## Windows password messages  
These password-related messages are sent to devices running Windows 10 or later.  

| Message | How to fix |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Password is required. | Set a password. Your organization requires that you enter a password to unlock your device. |
| Password is too simple. |  Make sure that your password doesn't contain sequential or repeating numbers, such as 1234 or 1111. |
| Password is too short.| Update or set a password with more characters. Your organization requires that your password is a certain length. The minimum length they can require is 4 characters, and the maximum is 16. |
| Password must only contain numbers. | Set a password that only contains numbers.|
| Password must only contain alphanumeric characters. | Set a password that contains a mix of numbers and letters.|
| Password must contain complex characters. | Add complex characters such as numbers, capital letters, and symbols like `$`, `%`, and `#`. Your organization requires a mix of letters, numbers, and nonalphanumeric characters to make it harder for others to guess the password.|  
| Password has expired. | Set a new password. Your organization requires you to change your password from time-to-time to ensure your device stays secure. |
| Your password was used too recently. | Create a brand new password. Your organization requires a certain amount of time to pass before you can reuse a password. |

## iOS passcode messages   

These password-related messages are sent to iOS/iPadOS devices.  

| Message | How to fix |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Passcode is required.| Set a passcode. Your organization requires that you enter a passcode to unlock your device. |
| Passcode is too simple. |  Make sure that your passcode doesn't contain sequential or repeating numbers, such as 1234 or 1111. |
| Passcode is too short. | Update or set a passcode with more characters. Your organization requires that your passcode is a certain length. The minimum length they can require is 4 characters, and the maximum is 14. When you change your passcode, you might see a prompt from Apple telling you to enter 6 or more characters; this message is only an Apple system recommendation. If your organization only requires a passcode that's 4 or 5 characters, you don't have to enter a 6-digit passcode.|  
| Passcode must only contain numbers. | Set a passcode that only contains numbers.|
| Passcode must only contain alphanumeric characters.| Set a passcode that contains a mix of numbers and letters.|
| Passcode must contain nonalphanumeric characters. | Add special characters such as `&`, `!`, `$`, `%`, and `#`. Your organization requires a mix of letters, numbers, and nonalphanumeric characters to make it harder for others to guess the passcode.|
| Passcode has expired. | Set a new password. Your organization requires you to change your password from time-to-time to keep your device secure.  |
| Your passcode was used too recently.| Create a brand new passcode. Your organization requires a certain amount of time to pass before you can reuse a passcode. |
|Touch ID or Face ID authentication required. | Set up Touch ID or Face ID. Your organization requires you to authenticate with one of these methods before using autofill for passwords or credit card information. | 

## macOS password messages   
These password-related messages are sent to Mac devices.  

| Message | How to fix |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Password is required. | Set a password. Your organization requires that you enter a password to unlock your device. |
| Password is too simple.|  Make sure that your password doesn't contain sequential or repeating numbers, such as 1234 or 1111. |
| Password is too short. | Update or set a password with more characters. Your organization requires that your password is a certain length.|
| Password must only contain numbers. | Set a password that only contains numbers.|
| Password must only contain alphanumeric characters. | Set a password that contains a mix of numbers and letters.|
| Password must contain non-alphanumeric characters. | Add special characters such as `&`, `!`, `$`, `%`, and `#`. Your organization requires a mix of letters, numbers, and nonalphanumeric characters to make it harder for others to guess the password.|
| Password has expired. | Set a new password. Your organization requires you to change your password from time-to-time to keep your device secure. |
| Your password was used too recently. | Create a brand new password. Your organization requires a certain amount of time to pass before you can reuse a password. |

## Android password messages  
These password-related messages are sent to Android devices.   

### Android work profile 
| Message | How to fix |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Set a work profile password. | Create a work profile password or pattern. Your organization requires that you enter a password to unlock your work profile. |
| Set a stronger work profile password. | Create a work profile PIN or password with at least four characters and no repeating (4444) or ordered (1234, 4321, 2468) sequences. |
| Set a more complex work profile password. | Create a work profile PIN or password that's at least eight digits long with no repeating or ordered sequences, or create an alphabetic or alphanumeric password with at least six characters. |
| Set a longer work profile password. | Update or set a password with more characters. Your organization requires that your password is a certain length.|
| Work profile password requires numbers. | Set a password or PIN that contains numbers.|
| Work profile password can't have repeating numbers. |  Make sure that your password or PIN doesn't contain sequential or repeating numbers, such as 1234 or 1111. |
| Work profile password requires a letter. | Set a password that contains letters from the alphabet.|
| Work profile password must have letters and numbers. | Set a password that contains a mix of numbers and letters.|
| Work profile password must include symbols. | Set a password that contains a mix of letters, numbers, and special characters such as `&`, `!`, `$`, `%`, and `#`. |
| Work profile password must use biometrics. | Set up your work profile to use biometric authentication, such as fingerprint or facial recognition. |
| Work profile password expired. | Set a new password. Your organization requires you to change your password after a certain number of days. |
| Work profile password was recently used. | Create a brand new password. Your organization requires a certain amount of time to pass before you can reuse a password. | 

### Android (no work profile)  

| Message | How to fix |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Password is required. | Set a password or PIN. Your organization requires that you enter a password to unlock your device. |
| Password is too simple. |  Make sure that your password or PIN doesn't contain sequential or repeating numbers, such as 1234 or 1111. |
| Password is too short. | Update or set a password with more characters. Your organization requires a longer device password. |
| Password must contain numbers. | Set a password or PIN that contains numbers.|
| Password must contain letters. | Set a password that contains letters from the alphabet.|
| Password must contain alphanumeric characters. | Set a password that contains a mix of numbers and letters.|
| Password must contain alphanumeric characters and symbols. | Set a password that contains a mix of letters, numbers, and special characters such as `&`, `!`, `$`, `%`, and `#`. |
| Password must use biometric technology.| Set up your device to use biometric authentication, such as fingerprint or facial recognition.
| Password has expired. | Set a new password. Your organization requires you to change your password from time-to-time to keep your device secure. |
| Your password was used too recently. | Create a brand new password. Your organization requires a certain amount of time to pass before you can reuse a password. |  

## Next steps  
For more information about password requirements, including how to change the password or screen lock on your device, see [Secure device with lock screen or password](password-does-not-meet-it-administrator-requirements.md).  

