---
# required metadata

title: Configure the Microsoft Managed Home Screen app
titleSuffix: Microsoft Intune
description: Learn how to configure the Microsoft Managed Home Screen app.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/26/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: 865c7f03-f525-4dfa-b3a8-d088a9106502

# optional metadata 

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Configure the Microsoft Managed Home Screen app for Android Enterprise

The Managed Home Screen is the application used for corporate-owned Android Enterprise dedicated devices enrolled via Intune and running in multi-app kiosk mode. For these devices, the Managed Home Screen acts as the launcher for other approved apps to run on top of it. The Managed Home Screen provides IT admins the ability to customize their devices and to restrict the capabilities that the end user can access. 

## When to configure the Microsoft Managed Home Screen app

Typically, if settings are available to you through Device configuration, configure the settings there. Doing so will save you time, minimize errors, and will give you a better Intune-support experience. However, some of the Managed Home Screen settings are currently only available via the **App configuration policies** pane in the Intune console. Use this document to learn how to configure the different settings either using the configuration designer or a JSON script. 

> [!NOTE]
> It is currently possible, and advisable, to set allow-listed applications and pinned web links through **Apps** and **Device configuration**. For the full list of settings available in **Device configuration** that impact Managed Home Screen,  see [Dedicated device settings](../intune/configuration/device-restrictions-android-for-work.md#dedicated-device-settings).  

First, navigate to the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Apps** > **App configuration policies**. Add a configuration policy for **Managed devices** running **Android** and choose **Managed Home Screen** as the associated app. Click on **Configuration settings** to configure the different available Managed Home Screen settings. 

## Choosing a Configuration Settings Format

There are two methods that you can use to define configuration settings for Managed Home Screen:

- **Configuration designer** allows you to configure settings with an easy-to-use UI that lets you toggle features on or off and set values. In this method, there are a few disabled configuration keys with value type `BundleArray`. These configuration keys can only be configured by entering JSON data. 
- **JSON data** allows you to define all possible configuration keys using a JSON script. 

If you add properties with Configuration Designer, you can automatically convert these properties to JSON by selecting **Enter JSON data** from the **Configuration settings format** dropdown.

![Screenshot of Configuration setting format options](./media/app-configuration-managed-home-screen-app/app-configuration-managed-home-screen-app_01.png)

## Using Configuration Designer

Configuration designer allows you to select pre-populated settings and their associated values. 

![Screenshot of added configuration settings](./media/app-configuration-managed-home-screen-app/app-configuration-managed-home-screen-app_02.png)

The following table lists the Managed Home Screen available configuration keys, value types, default values, and descriptions. The description provides the expected device behavior based on the selected values. Configuration keys that are disabled in Configuration Designer are not listed in the table.

| Configuration   Key | Value Type | Default Value | Description |
|---------------------------------------------------------------------------------------------------------------------------|-------------|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Set Grid Size | string | Auto | Allows you to set the grid size for apps to be positioned on   the managed home screen. You can set the number of app rows and columns to define grid size in the following format `columns;rows`. If you define the   grid size, the maximum number of apps that will be shown in a row on the home   screen would be the number of rows you set and the maximum number of apps   that will be shown in a column in the home screen would be the number of   columns you set. |
| Enable notifications badge | bool | FALSE | Enables the notification badge for app icons that shows the number of new notifications on the app. If you enable this setting, end users   will see notification badges on apps that have unread notifications. If you keep this configuration key disabled, the end user will not see any notification badged to apps   that might have unread notifications. |
| Lock Home Screen | bool | TRUE | Removes the ability of the end user to move around app icons   on the home screen. If you enable this configuration key, the app icons on the home screen will   be locked and the end user would not be able to drag and drop to different   grid positions of the home screen. If turned to `false`, end users will be able to move around application and weblink icons on the Managed Home Screen.  |
| Set device wall paper | string | Default | Allows you to set a wallpaper of your choice by entering the   URL of the image that you want to set as a wallpaper. |
| Set app icon size | integer | 2 | Allows you to set the icon size for apps displayed on the home   screen. You can choose the following values in this configuration for   different sizes - 0 (Smallest), 1 (Small), 2 (Regular), 3 (Large) and 4   (Largest). |
| Set app folder icon | integer | 0 | Allows you to define the appearance of app folders on the home   screen. You can choose the appearance from following values: Dark Square(0);   Dark Circle(1); Light Square(2); Light Circle(3). |
| Set screen orientation | integer | 1 | Allows you to set the orientation of the home screen to   portrait mode, landscape mode or allow auto rotate. You can set the   orientation by entering values 1 (for portrait mode), 2 (for Landscape mode),   3 (for Autorotate). |
| Enable device telemetry | bool | FALSE | Enables all the telemetry that is being captured for the   managed home screen. If you enable this, Microsoft will be able to capture device usage telemetry, such as the number of times a particular app is launched on this device. |
| Set allow-listed applications | bundleArray | FALSE | Allows you to define the set of apps visible on the home screen from amongst the apps installed on the device. You can define the apps   by entering the app package name of the apps that you would like to make   visible, for example com.microsoft.emmx would make settings accessible on the home   screen. The apps that you allow-list in this section should already be installed on the device in order to be visible on the home screen. |
| Set pinned web links | bundleArray | FALSE | Allows you to pin websites as quick launch icons on the home   screen. With this configuration, you can define the URL and add it to the home   screen for the end user to launch in the browser with a single tap. |
| Enable screen saver | bool | FALSE | To enable screen saver mode or not. If set to true, you can   configure **screen_saver_image**, **screen_saver_show_time**,   **inactive_time_to_show_screen_saver**, and   **media_detect_screen_saver**. |
| Screen saver image | string |   | Set the URL of the screen saver image. If no URL is set,   devices will show the default screen saver image when screen saver is activated. The default image shows the Managed Home Screen app icon.  |
| Screen saver show time | integer | 0 | Gives option to set the amount of time in seconds the device   will display the screen saver during screen saver mode. If set to 0, the   screen saver will show on screen saver mode indefinitely until the device   becomes active.  |
| Inactive time to enable   screen saver | integer | 30 | The number of seconds the device is inactive before triggering   the screen saver. If set to 0, the device will never go into screen saver mode. |
| Media detect before showing screen saver | bool | TRUE | Choose whether the device screen should show   screen saver if audio/video is playing on device. If set to true, the   device will not play audio/video, regardless of the value in **inactive_time_to_show_scree_saver**. If set to false, device  screen will show screen saver according to value set in   **inactive_time_to_show_screen_saver**.   |
| Enable virtual home button | bool | FALSE | Turn this setting to `True` to allow the end user to have access to a Managed Home Screen home button that will return the user to the Managed Home Screen from the current task they are in.  |
| Type of virtual home button | string | swipe_up | Use **swipe_up** to access home button with a swipe up gesture. Use **float** to access a sticky, persistent  home button that can be moved around the screen by the end user. |
| Battery and Signal Strength   indicator bar | bool | True  | Turning this setting to `True` shows the battery and signal strength indicator bar. |
| Exit lock task mode password | string |   | Enter a 4-6-digit code to use to temporarily drop out of lock-task mode for troubleshooting. |
| Show Wi-Fi setting | bool | FALSE | Turning this setting to `True` allows the end user to turn on or off Wi-Fi, or to connect to different Wi-Fi networks.  |
| Show Bluetooth setting | bool | FALSE | Turning this setting to `True` allows the end user to turn on or off Bluetooth and to connect to different Bluetooth-capable devices.   |
| Applications in folder are ordered by name | bool | TRUE | Turning this setting to `False` allows items in a folder to appear in the order in which they are specified. Otherwise, they will appear in the folder alphabetically.   |
| Application order enabled | bool | FALSE | Turning this setting to `True` allows enables the ability to set the order of applications, weblinks, and folders on the Managed Home Screen. Once enabled, set the ordering with **app_order**.the end user to turn on or off Bluetooth and to connect to different Bluetooth-capable devices.   |
| Application order | bundleArray | FALSE | Allows you to specify the order of applications, weblinks and folders on the Managed Home Screen. To use this setting, **Lock Home Screen** must be enabled, **Set grid size** must be defined and **Application order enabled** must be set to `True`.   |

## Enter JSON Data

Enter JSON data to configure all available settings for Managed Home Screen, as well as the settings disabled in **Configuration Designer**.

![Screenshot of added JSON data](./media/app-configuration-managed-home-screen-app/app-configuration-managed-home-screen-app_03.png)

In addition to the list of configurable settings listed in the **Configuration Designer** table (above), the following table provides the configuration keys you can only configure via JSON data.

|    Configuration   Key    |    Value   Type    |    Default   Value    |    Description    |
|-------------------------------------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Set allow-listed applications    |    bundleArray    | <img alt="JSON - Example 1" src="./media/app-configuration-managed-home-screen-app/defaultvaluejson01.png" width="300"> |    Allows you to define the set of   apps visible on the home screen from amongst the apps installed on the   device. You can define the apps by entering the app package name of the apps   that you would like to make visible, for example, com.android.settings would make settings accessible on the home screen. The apps that you allow-list in this section   should already be installed on the device in order to be visible on the home   screen.    |
|    Set pinned web links    |    bundleArray    | <img alt="JSON - Example 2" src="./media/app-configuration-managed-home-screen-app/defaultvaluejson02.png" width="300"> |    Allows you to pin websites as   quick launch icons on the home screen. With this configuration, you can define   the URL and add it to the home screen for the end user to launch in the   browser with a single tap.    |
|    Create Managed Folder for grouping   apps    |    bundleArray    | <img alt="JSON - Example 3" src="./media/app-configuration-managed-home-screen-app/defaultvaluejson03.png" width="300"> |    Allows you to create and name   folders and group apps within these folders. End users will not be able to   move folders, rename the folders, or move the apps within the folders.   Folders will appear in the order created, and apps within the folders will   appear alphabetically.         Note: all apps that you want to   group into folders must be assigned as required to the device and must have   been added to the Managed Home Screen.     |

The following is an example JSON script with all the available configuration keys included:

```json
{
    "kind": "androidenterprise#managedConfiguration",
    "productId": "com.microsoft.launcher.enterprise",
    "managedProperty": [
        {
            "key": "lock_home_screen",
            "valueBool": true
        },
        {
            "key": "wallpaper",
            "valueString": "default"
        },
        {
            "key": "icon_size",
            "valueInteger": 2
        },
        {
            "key": "app_folder_icon",
            "valueInteger": 0
        },
        {
            "key": "screen_orientation",
            "valueInteger": 1
        },
        {
            "key": "enable_telemetry",
            "valueBool": false
        },
        {
            "key": "applications",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "package",
                            "valueString": “app package name here”
                        }
                    ]
                }
            ]
        },
        {
            "key": "weblinks",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "link",
                            "valueString": “link here”
                        },
                        {
                            "key": "label",
                            "valueString": “weblink label here”
                        }
                    ]
                }
            ]
        },
        {
            "key": "show_virtual_home",
            "valueBool": false
        },
        {
            "key": "virtual_home_type",
            "valueString": "swipe_up"
        },
        {
            "key": "show_virtual_status_bar",
            "valueBool": true
        },
        {
            "key": "exit_lock_task_mode_code",
            "valueString": ""
        },
        {
            "key": "show_wifi_setting",
            "valueBool": false
        },
        {
            "key": "show_bluetooth_setting",
            "valueBool": false
        },
        {
            "key": "grid_size",
            "valueString": "4;5"
        },
        {
            "key": "app_order_enabled",
            "valueBool": true
        },
        {
            "key": "apps_in_folder_ordered_by_name",
            "valueBool": true
        },
        {
            "key": "app_orders",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "package",
                            "valueString": "com.Microsoft.emmx"
                        },
                        {
                            "key": "type",
                            "valueString": "application"
                        },
                        {
                            "key": "container",
                            "valueInteger": 1
                        },
                        {
                            "key": "position",
                            "valueInteger": 1
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "folder_name",
                            "valueString": "Work"
                        },
                        {
                            "key": "type",
                            "valueString": "managed_folder"
                        },
                        {
                            "key": "container",
                            "valueInteger": 1
                        },
                        {
                            "key": "position",
                            "valueInteger": 2
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "package",
                            "valueString": "com.microsoft.launcher.enterprise"
                        },
                        {
                            "key": "type",
                            "valueString": "application"
                        },
                        {
                            "key": "class",
                            "valueString": "com.microsoft.launcher.launcher"
                        },
                        {
                            "key": "container",
                            "valueInteger": 1
                        },
                        {
                            "key": "position",
                            "valueInteger": 3
                        }
                    ]
                }
            ]
        },
        {
            "key": "managed_folders",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "folder_name",
                            "valueString": "Folder name here"
                        },
                        {
                            "key": "applications",
                            "valueBundleArray": [
                                {
                                    "managedProperty": [
                                        {
                                            "key": "package",
                                            "valueString": "com.microsoft.emmx"
                                        }
                                    ]
                                },
                                {
                                    "managedProperty": [
                                        {
                                            "key": "package",
                                            "valueString": "com.microsoft.bing"
                                        }
                                    ]
                                },
                                {
                                    "managedProperty": [
                                        {
                                            "key": "link",
                                            "valueString": "https://microsoft.com/"
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "folder_name",
                            "valueString": "Example folder name 2"
                        },
                        {
                            "key": "applications",
                            "valueBundleArray": [
                                {
                                    "managedProperty": [
                                        {
                                            "key": "package",
                                            "valueString": "com.microsoft.office.word"
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                }
            ]
        }
    ]
}
```

## Google's Android Device Policy app
The Managed Home Screen app now provides access to Google's Android Device Policy app. The Managed Home Screen app is a custom launcher used for devices enrolled in Intune as Android Enterprise (AE) dedicated devices using multi-app kiosk mode. You can access the Android Device Policy app, or guide users to the Android Device Policy app, for support and debug purposes. This launching capability is available at the time the device enrolls and locks into Managed Home Screen. No additional installations are needed to use this functionality.

## Managed Home Screen debug screen
You can access the Managed Home Screen's debug screen by clicking the **back** button until the debug screen is displayed (click the **back** button 15 times or more). From this debug screen, you are able to launch the Android Device Policy application, view and upload logs, or temporarily pause kiosk mode to update the device. For more information about pausing kiosk mode, see the **Leave kiosk mode** item in the Android Enterprise [dedicated device settings](../intune/configuration/device-restrictions-android-for-work.md#dedicated-device-settings).

## Next steps

- For more information about Android Enterprise dedicated devices, see [Set up Intune enrollment of Android Enterprise dedicated devices](../intune/enrollment/android-kiosk-enroll.md).
