---
title: "SMS_Processor Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 7f338a23-33c5-44c0-adc2-a8d44ceaa179
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_Processor Client WMI Class
The `SMS_Processor` class is a client Windows Management Instrumentation (WMI) class, in Configuration Manager, that represents a device that can interpret a sequence of instructions on a computer that is running a Windows operating system. On a multiprocessor computer, one `SMS_Processor` object exists for each processor.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Processor   
{  
      UInt16 AddressWidth;  
      UInt16 Architecture;  
      UInt16 Availability;  
      UInt16 BrandID;  
      String Caption;  
      UInt32 ConfigManagerErrorCode;  
      Boolean ConfigManagerUserConfig;  
      String CPUHash;  
      String CPUKey;  
      UInt16 CpuStatus;  
      UInt16 CreationClassName;  
      UInt32 CurrentClockSpeed;  
      UInt16 CurrentVoltage;  
      UInt16 DataWidth;  
      String Description;  
      String DeviceID;  
      Boolean ErrorCleared;  
      String ErrorDescription;  
      UInt32 ExtClock;  
      UInt16 Family;  
      DateTime InstallDate;  
      Boolean Is64Bit;  
      Boolean IsHyperthreadCapable;  
      Boolean IsHyperthreadEnabled;  
      Boolean IsMobile;  
      Boolean IsMulticore;  
      UInt32 L2CacheSize;  
      UInt32 L2CacheSpeed;  
      UInt32 LastErrorCode;  
      UInt16 Level;  
      UInt16 LoadPercentage;  
      String Manufacturer;  
      UInt32 MaxClockSpeed;  
      String Name;  
      UInt32 NormSpeed;  
      String OtherFamilyDescription;  
      UInt32 PCache;  
      String PNPDeviceID;  
      UInt16 PowerManagementCapabilities[];  
      Boolean PowerManagementSupported;  
      String ProcessorId;  
      UInt16 ProcessorType;  
      UInt16 Revision;  
      String Role;  
      String SocketDesignation;  
      String Status;  
      UInt16 StatusInfo;  
      String Stepping;  
      String SystemName;  
      String UniqueId;  
      UInt16 UpgradeMethod;  
      String Version;  
      UInt32 VoltageCaps;  
};  
```  

## Methods  
 The `SMS_Processor` class does not define any methods.  

## Properties  
 `AddressWidth`  
 Data type: `UInt16`  

 Access type: Read-only  

 Qualifiers: None  

 Processor address width, in bits, that represents the size of a pointer type on the processor. On a 32-bit processor, the value is 32. On a 64-bit processor, the value is 64.  

 `Architecture`  
 Data type: `UInt16`  

 Access type: Read-only  

 Qualifiers: None  

 Processor architecture used by the platform. Possible values are:  

|||  
|-|-|  
|0 (0x0)|x86|  
|1 (0x1)|MIPS|  
|2 (0x2)|Alpha|  
|3 (0x3)|PowerPC|  
|6 (0x6)|Intel Itanium Processor Family (IPF)|  
|9 (0x9)|x64|  

 `Availability`  
 Data type: `UInt16`  

 Access type: Read-only  

 Qualifiers: None  

 Availability and status of the device. Possible values are:  

|||  
|-|-|  
|1 (0x1)|Other|  
|2 (0x2)|Unknown|  
|3 (0x3)|Running or Full Power|  
|4 (0x4)|Warning|  
|5 (0x5)|In Test|  
|6 (0x6)|Not Applicable|  
|7 (0x7)|Power Off|  
|8 (0x8)|Off Line|  
|9 (0x9)|Off Duty|  
|10 (0xA)|Degraded|  
|11 (0xB)|Not Installed|  
|12 (0xC)|Install Error|  
|13 (0xD)|Power Save - Unknown. The device is known to be in a power save state, but its exact status is unknown.|  
|14 (0xE)|Power Save - Low Power Mode. The device is in a power save state, but it is still functioning, and might exhibit decreased performance.|  
|15 (0xF)|Power Save - Standby. The device is not functioning, but it can be brought to full power quickly.|  
|16 (0x10)|Power Cycle|  
|17 (0x11)|Power Save - Warning. The device is in a warning state, though also in a power save state.|  

 `BrandID`  
 Data type: `UInt16`  

 Access type: Read-only  

 Qualifiers: None  

 Processor architecture-specific brand identification information.  

 `Caption`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Short description of an object. The caption consists of a one-line string.  

 `ConfigManagerErrorCode`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Windows API Configuration Manager error code. Possible values are:  

|||  
|-|-|  
|0 (0x0)|Device is working properly.|  
|1 (0x1)|Device is not configured correctly.|  
|2 (0x2)|Windows cannot load the driver for this device.|  
|3 (0x3)|Driver for this device might be corrupted or the system might be low on memory or other resources.|  
|4 (0x4)|Device is not working properly. One of its drivers or the registry might be corrupted.|  
|5 (0x5)|Driver for the device requires a resource that Windows cannot manage.|  
|6 (0x6)|Boot configuration for the device conflicts with other devices.|  
|7 (0x7)|Cannot filter.|  
|8 (0x8)|Driver loader for the device is missing.|  
|9 (0x9)|Device is not working properly. The controlling firmware is incorrectly reporting the resources for the device.|  
|10 (0xA)|Device cannot start.|  
|11 (0xB)|Device failed.|  
|12 (0xC)|Device cannot find enough free resources to use.|  
|13 (0xD)|Windows cannot verify the device resources.|  
|14 (0xE)|Device cannot work properly until the computer is restarted.|  
|15 (0xF)|Device is not working properly due to a possible re-enumeration problem.|  
|16 (0x10)|Windows cannot identify all of the resources that the device uses.|  
|17 (0x11)|Device is requesting an unknown resource type.|  
|18 (0x12)|Device drivers must be reinstalled.|  
|19 (0x13)|Failure using the VxD loader.|  
|20 (0x14)|Registry might be corrupted.|  
|21 (0x15)|System failure. If changing the device driver is ineffective, see the hardware documentation. Windows is removing the device.|  
|22 (0x16)|Device is disabled.|  
|23 (0x17)|System failure. If changing the device driver is ineffective, see the hardware documentation.|  
|24 (0x18)|Device is not present, not working properly, or does not have all of its drivers installed.|  
|25 (0x19)|Windows is still setting up the device.|  
|26 (0x1A)|Windows is still setting up the device.|  
|27 (0x1B)|Device does not have valid log configuration.|  
|28 (0x1C)|Device drivers are not installed.|  
|29 (0x1D)|Device is disabled. The device firmware did not provide the required resources.|  
|30 (0x1E)|Device is using an IRQ resource that another device is using.|  
|31 (0x1F)|Device is not working properly. Windows cannot load the required device drivers.|  

 `ConfigManagerUserConfig`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: None  

 `true` if the device is using a configuration that the user defines.  

 `CPUHash`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 A unique 128-bit signature that is derived from a combination of the `Manufacturer`, `BrandID`, `PCache`, `NormSpeed`, `IsMobile`, and `Name` properties.  

 `CPUKey`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Key for the CPU associated with the processor.  

 `CpuStatus`  
 Data type: `UInt16`  

 Access type: Read-only  

 Qualifiers: None  

 Current status of the processor. Possible values are listed below. Status changes indicate processor usage, but not the physical condition of the processor.  

|||  
|-|-|  
|0 (0x0)|Unknown|  
|1 (0x1)|CPU Enabled|  
|2 (0x2)|CPU Disabled by User via BIOS Setup|  
|3 (0x3)|CPU Disabled by BIOS (POST Error)|  
|4 (0x4)|CPU Is Idle|  
|5 (0x5)|Reserved|  
|6 (0x6)|Reserved|  
|7 (0x7)|Other|  

 `CreationClassName`  
 Data type: `UInt16`  

 Access type: Read-only  

 Qualifiers: None  

 The creation class name.  

 `CurrentClockSpeed`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Current speed of the processor, in megahertz.  

 `CurrentVoltage`  
 Data type: `UInt16`  

 Access type: Read-only  

 Qualifiers: None  

 Voltage of the processor. If the eighth bit is set, bits 0-6 contain the voltage multiplied by 10. If the eighth bit is not set, the bit setting in the `VoltageCaps` property represents the voltage value. The `CurrentVoltage` property is only set when SMBIOS designates a voltage value.  

 Example: Value for a processor voltage of 1.8 volts is 0x12 (1.8 x 10).  

 `DataWidth`  
 Data type: `UInt16`  

 Access type: Read-only  

 Qualifiers: None  

 Processor data width, in bits.  

 `Description`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Description of the processor.  

 `DeviceID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key]  

 Unique ID of the processor.  

 `ErrorCleared`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: None  

 `true` if the error reported in the `LastErrorCode` property is cleared.  

 `ErrorDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Additional information about the error that is recorded in the `LastErrorCode` property and information about corrective actions that can be taken.  

 `ExtClock`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 External clock frequency, in megahertz. If the frequency is unknown, set this property to `null`.  

 `Family`  
 Data type: `UInt16`  

 Access type: Read-only  

 Qualifiers: None  

 Processor family type. Possible values are:  

|||  
|-|-|  
|1 (0x1)|Other|  
|2 (0x2)|Unknown|  
|3 (0x3)|8086|  
|4 (0x4)|80286|  
|5 (0x5)|Intel386 Processor|  
|6 (0x6)|Intel486 Processor|  
|7 (0x7)|8087|  
|8 (0x8)|80287|  
|9 (0x9)|80387|  
|10 (0xA)|80487|  
|11 (0xB)|Pentium Brand|  
|12 (0xC)|Pentium Pro|  
|13 (0xD)|Pentium II|  
|14 (0xE)|Pentium Processor with MMX Technology|  
|15 (0xF)|Celeron|  
|16 (0x10)|Pentium II Xeon|  
|17 (0x11)|Pentium III|  
|18 (0x12)|M1 Family|  
|19 (0x13)|M2 Family|  
|20 (0x14)|AMD Duron Processor Family|  
|21 (0x15)|K5 Family|  
|22 (0x16)|K6 Family|  
|23 (0x17)|K6-2|  
|24 (0x18)|K6-3|  
|25 (0x19)|AMD Athlon Processor Family|  
|26 (0x1A)|AMD2900 Family|  
|27 (0x1B)|K6-2+|  
|32 (0x20)|Power PC Family|  
|33 (0x21)|Power PC 601|  
|34 (0x22)|Power PC 603|  
|35 (0x23)|Power PC 603+|  
|36 (0x24)|Power PC 604|  
|37 (0x25)|Power PC 620|  
|38 (0x26)|Power PC X704|  
|39 (0x27)|Power PC 750|  
|48 (0x30)|Alpha Family|  
|49 (0x31)|Alpha 21064|  
|50 (0x32)|Alpha 21066|  
|51 (0x33)|Alpha 21164|  
|52 (0x34)|Alpha 21164PC|  
|53 (0x35)|Alpha 21164a|  
|54 (0x36)|Alpha 21264|  
|55 (0x37)|Alpha 21364|  
|64 (0x40)|MIPS Family|  
|65 (0x41)|MIPS R4000|  
|66 (0x42)|MIPS R4200|  
|67 (0x43)|MIPS R4400|  
|68 (0x44)|MIPS R4600|  
|69 (0x45)|MIPS R10000|  
|80 (0x50)|SPARC Family|  
|81 (0x51)|SuperSPARC|  
|82 (0x52)|microSPARC II|  
|83 (0x53)|microSPARC IIep|  
|84 (0x54)|UltraSPARC|  
|85 (0x55)|UltraSPARC II|  
|86 (0x56)|UltraSPARC IIi|  
|87 (0x57)|UltraSPARC III|  
|88 (0x58)|UltraSPARC IIIi|  
|96 (0x60)|68040|  
|97 (0x61)|68xxx Family|  
|98 (0x62)|68000|  
|99 (0x63)|68010|  
|100 (0x64)|68020|  
|101 (0x65)|68030|  
|112 (0x70)|Hobbit Family|  
|120 (0x78)|Crusoe TM5000 Family|  
|121 (0x79)|Crusoe TM3000 Family|  
|122 (0x7A)|Efficeon TM8000 Family|  
|128 (0x80)|Weitek|  
|130 (0x82)|Itanium Processor|  
|131 (0x83)|AMD Athlon 64 Processor Family|  
|132 (0x84)|AMD Opteron Processor Family|  
|144 (0x90)|PA-RISC Family|  
|145 (0x91)|PA-RISC 8500|  
|146 (0x92)|PA-RISC 8000|  
|147 (0x93)|PA-RISC 7300LC|  
|148 (0x94)|PA-RISC 7200|  
|149 (0x95)|PA-RISC 7100LC|  
|150 (0x96)|PA-RISC 7100|  
|160 (0xA0)|V30 Family|  
|176 (0xB0)|Pentium III Xeon Processor|  
|177 (0xB1)|Pentium III Processor with Intel SpeedStep Technology|  
|178 (0xB2)|Pentium 4|  
|179 (0xB3)|Intel Xeon|  
|180 (0xB4)|AS400 Family|  
|181 (0xB5)|Intel Xeon Processor MP|  
|182 (0xB6)|AMD Athlon XP Family|  
|183 (0xB7)|AMD Athlon MP Family|  
|184 (0xB8)|Intel Itanium 2|  
|185 (0xB9)|Intel Pentium M Processor|  
|190 (0xBE)|K7|  
|200 (0xC8)|IBM390 Family|  
|201 (0xC9)|G4|  
|202 (0xCA)|G5|  
|203 (0xCB)|G6|  
|204 (0xCC)|z/Architecture Base|  
|250 (0xFA)|i860|  
|251 (0xFB)|i960|  
|260 (0x104)|SH-3|  
|261 (0x105)|SH-4|  
|280 (0x118)|ARM|  
|281 (0x119)|StrongARM|  
|300 (0x12C)|6x86|  
|301 (0x12D)|MediaGX|  
|302 (0x12E)|MII|  
|320 (0x140)|WinChip|  
|350 (0x15E)|DSP|  
|500 (0x1F4)|Video Processor|  

 `InstallDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: None  

 Date and time when the processor was installed. A value for this property is not required.  

 `Is64Bit`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: None  

 A non-zero value if the CPU is 64-bit. Otherwise, this property is set to zero.  

 `IsHyperthreadCapable`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: None  

 A non-zero value if processor supports hyperthreading. Otherwise, this property is set to zero.  

 `IsHyperthreadEnabled`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: None  

 A non-zero value if hyperthreading is enabled. Otherwise, this property is set to zero.  

 `IsMobile`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: None  

 `true` if the computer is a mobile device.  

 `IsMulticore`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: None  

 `true` if the computer has more than one core.  

 `L2CacheSize`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Size of the level 2 processor cache. A level 2 cache is an external memory area that has a faster access time than the main RAM.  

 `L2CacheSpeed`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Clock speed of the level 2 processor cache.  

 `LastErrorCode`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Last error code reported by the logical device.  

 `Level`  
 Data type: `UInt16`  

 Access type: Read-only  

 Qualifiers: None  

 Level definition for the processor. The value depends on processor architecture.  

 `LoadPercentage`  
 Data type: `UInt16`  

 Access type: Read-only  

 Qualifiers: None  

 Load capacity for the processor, averaged to the last second. Processor loading refers to the total computing burden for a processor at one time.  

 `Manufacturer`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Name of the processor manufacturer, for example, "A. Datum Corporation".  

 `MaxClockSpeed`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Maximum speed of the processor, in megahertz.  

 `Name`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Label by which the processor is known. When this name indicates a subclass, it can be overridden to be a key property.  

 `NormSpeed`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 The normalized processor speed, in megahertz.  

 `OtherFamilyDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Processor family type. This property is used when the `Family` property is set to "Other". For other settings of the `Family` property, set this string to `null`.  

 `PCache`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Processor cache.  

 `PNPDeviceID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Windows Plug and Play device ID of the logical device.  

 `PowerManagementCapabilities`  
 Data type: `UInt16` Array  

 Access type: Read-only  

 Qualifiers: None  

 Specific power-related capabilities of a logical device. Possible values are:  

|||  
|-|-|  
|0 (0x0)|Unknown|  
|1 (0x1)|Not Supported|  
|2 (0x2)|Disabled|  
|3 (0x3)|Enabled. The power management features are currently enabled, but the exact feature set is unknown or the information is unavailable.|  
|4 (0x4)|Power Saving Modes Entered Automatically. The device can change its power state based on usage or other criteria.|  
|5 (0x5)|Power State Settable. The `SetPowerState` method is supported. This method is found on the parent `CIM_LogicalDevice` class and can be implemented.|  
|6 (0x6)|Power Cycling Supported. The `SetPowerState` method can be invoked with the `PowerState` parameter set to 5 (Power Cycle).|  
|7 (0x7)|Timed Power-On Supported. The `SetPowerState` method can be invoked with the `PowerState` parameter set to 5 (Power Cycle) and the `Time` parameter set to a specific date and time, or interval, for power-on.|  

 `PowerManagementSupported`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: None  

 `true` if the power of the logical device can be managed, indicating that it can be put into suspend mode, and so on. This property does not indicate that power management features are enabled.  

 `ProcessorId`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Processor ID. For an x86 class CPU, the field format depends on the processor support of the CPUID instruction. If the instruction is supported, the property contains two DWORD formatted values. The first is an offset of 08h-0Bh, which is the EAX value that a CPUID instruction returns with input EAX set to 1. The second is an offset of 0Ch-0Fh, which is the EDX value that the instruction returns. Only the first two bytes of the property are significant and contain the contents of the DX register at CPU reset. All other bytes are set to 0 (zero), and the contents are in DWORD format.  

 `ProcessorType`  
 Data type: `UInt16`  

 Access type: Read-only  

 Qualifiers: None  

 Primary function of the processor. Possible values are:  

|||  
|-|-|  
|1 (0x1)|Other|  
|2 (0x2)|Unknown|  
|3 (0x3)|Central Processor|  
|4 (0x4)|Math Processor|  
|5 (0x5)|DSP Processor|  
|6 (0x6)|Video Processor|  

 `Revision`  
 Data type: `UInt16`  

 Access type: Read-only  

 Qualifiers: None  

 System revision level that depends on the processor architecture. The system revision level contains the same values as the `Version` property, but in a numerical format.  

 `Role`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Role of the processor, for example, "Central Processor" or "Math Processor".  

 `SocketDesignation`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Type of chip socket used on the circuit, for example, "J202".  

 `Status`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Current status of the processor. Possible values are:  

- OK  

- Error  

- Degraded  

- Unknown  

- Pred Fail  

- Starting  

- Stopping  

- Service  

- Stressed  

- NonRecover  

- NoContact  

- LostComm  

  `StatusInfo`  
  Data type: `UInt16`  

  Access type: Read-only  

  Qualifiers: None  

  State of the logical device. Possible values are listed below. If this property does not apply to the logical device, the property is set to "Not Applicable".  

|||  
|-|-|  
|1 (0x1)|Other|  
|2 (0x2)|Unknown|  
|3 (0x3)|Enabled|  
|4 (0x4)|Disabled|  
|5 (0x5)|Not Applicable|  

 `Stepping`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Revision level of the processor in the processor family.  

 `SystemName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Name of the scoping system.  

 `UniqueId`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 GUID for the processor. This identifier can be unique only within a processor family.  

 `UpgradeMethod`  
 Data type: `UInt16`  

 Access type: Read-only  

 Qualifiers: None  

 CPU socket information, including the method by which the processor can be upgraded, if upgrades are supported. Possible values are:  

|||  
|-|-|  
|1 (0x1)|Other|  
|2 (0x2)|Unknown|  
|3 (0x3)|Daughter Board|  
|4 (0x4)|ZIF Socket|  
|5 (0x5)|Replacement or Piggy Back|  
|6 (0x6)|None|  
|7 (0x7)|LIF Socket|  
|8 (0x8)|Slot 1|  
|9 (0x9)|Slot 2|  
|10 (0xA)|370 Pin Socket|  
|11 (0xB)|Slot A|  
|12 (0xC)|Slot M|  
|13 (0xD)|Socket 423|  
|14 (0xE)|Socket A (Socket 462)|  
|15 (0xF)|Socket 478|  
|16 (0x10)|Socket 754|  
|17 (0x11)|Socket 940|  
|18 (0x12)|Socket 939|  

 `Version`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Processor revision number that depends on the architecture.  

 `VoltageCaps`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Voltage capabilities of the processor. Possible values are listed below. If the property is set to `null`, the voltage capabilities are unknown.  

|||  
|-|-|  
|1 (0x1)|5 volts|  
|2 (0x2)|3.3 volts|  
|4 (0x4)|2.9 volts|  

 Bits 0-3 of the property represent specific voltages that the processor socket can accept. All other bits should be set to 0 (zero). The socket is configurable if multiple bits are set. For more information about the actual voltage at which the processor is running, see the `CurrentVoltage` property.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Asset Intelligence Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/asset-intelligence-client-wmi-classes.md)   
 [SMS_AutoStartSoftware Class](../../../../../develop/reference/core/clients/client-classes/sms_autostartsoftware-client-wmi-class.md)   
 [SMS_BrowserHelperObject Class](../../../../../develop/reference/core/clients/client-classes/sms_browserhelperobject-client-wmi-class.md)   
 [SMS_InstalledExecutable Class](../../../../../develop/reference/core/clients/client-classes/sms_installedexecutable-client-wmi-class.md)   
 [SMS_InstalledSoftware Class](../../../../../develop/reference/core/clients/client-classes/sms_installedsoftware-client-wmi-class.md)   
 [SMS_InstalledSoftwareMS Class](../../../../../develop/reference/core/clients/client-classes/sms_installedsoftwarems-client-wmi-class.md)   
 [SMS_SoftwareShortcut Class](../../../../../develop/reference/core/clients/client-classes/sms_softwareshortcut-client-wmi-class.md)   
 [SMS_SystemConsoleUsage Class](../../../../../develop/reference/core/clients/client-classes/sms_systemconsoleusage-client-wmi-class.md)   
 [SMS_SystemConsoleUser Class](../../../../../develop/reference/core/clients/client-classes/sms_systemconsoleuser-client-wmi-class.md)
