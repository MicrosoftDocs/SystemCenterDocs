---
title: Orchestrator Integration Toolkit Overview
description: The Orchestrator Integration Toolkit is used to create new integrations for Orchestrator.
author: rayne-wiselman
manager: carmonm
ms.date: 02/02/2018
ms.prod: system-center
ms.technology: orchestrator
ms.topic: reference
ms.author: raynew
---

# Orchestrator Integration Toolkit overview

System Center Orchestrator enables integration, efficiency, and business alignment of your IT environment. Using System Center Orchestrator, you can automate your IT operations and standardize on best practices to improve operational efficiency. Orchestrator allows you to connect different systems from different vendors without any knowledge of scripting or programming languages.

 This overview describes the functionality available in Orchestrator Integration Toolkit.  

## Toolkit Components  
 The installation of the Orchestrator Integration Toolkit consists of the following:  

|||  
|-|-|  
|Component|Description|  
|Command-Line Activity Wizard|A utility that allows users to define activities that contain commands that run via Windows command shell, PowerShell, or SSH, and package them into an assembly (.DLL) that can be used with the .NET IP or packaged into a new Integration Pack.|  
|Integration Pack Wizard|A utility designed to package Orchestrator-compatible activity assemblies and dependent files into a deployable Integration Pack file.|  
|Integration Toolkit .NET IP|An Integration Pack for running .NET-based Orchestrator-compatible activity assemblies directly. Contains the Invoke .NET and Monitor .NET activities.|  
|Integration Toolkit SDK Library|A set of files that are used by developers utilizing the Orchestrator SDK to write custom activities.|  

## What’s New in the Integration Toolkit  
 This section describes the changes in the product, including bug fixes, new and enhanced features, and new information about the Orchestrator Integration Toolkit.  

### Major Changes  

#### Installation  

-   The Integration Toolkit no longer includes the binaries for the Windows Installer XML (WiX) Toolset, used for creating the Windows Installer files within Integration Packs. This set of tools is now a prerequisite installation. The Integration Toolkit supports version 3.5 of the WiX Toolset. The WiX Toolset can be downloaded from [http://wix.codeplex.com](http://wix.codeplex.com).  

#### Orchestrator SDK  

-   There have been significant changes to the SDK namespace, interfaces, and attributes as part of rebranding to Microsoft. For details about these changes, please see the [Orchestrator SDK](https://msdn.microsoft.com/en-us/library/hh855054.aspx).  

-   The full SDK documentation and code examples are no longer included in the installation of the Orchestrator Integration Toolkit. The SDK Documentation is located on MSDN, and the code samples are located on CodePlex at [http://orchestrator.codeplex.com](http://orchestrator.codeplex.com).  

### New and Enhanced Features  

#### General  

-   There is now one primary help file for the utilities in the Toolkit. However, detailed documentation is now located on TechNet to allow for continuous content updates.  

#### Installation  

-   If installing on a computer where Orchestrator is already installed, it will detect the Orchestrator installation path and install there. Otherwise, it installs to a default path of **%ProgramFiles(x86)%\Microsoft System Center <version>\Orchestrator\Integration Toolkit**. On 32-bit Windows 7, the base directory is **%ProgramFiles%**.  

-   The Integration Toolkit no longer includes the binaries for the Windows Installer XML (WiX) Toolset, used for creating the Windows Installer files within Integration Packs. This set of tools is now a prerequisite installation. The Integration Toolkit supports version 3.5 of the WiX Toolset. The WiX Toolset can be downloaded from [http://wix.codeplex.com](http://wix.codeplex.com). Installation of the Integration Toolkit is prevented until WiX is installed.  

-   A license key is longer required to install the product.  

#### Command-Line Activity Wizard  

-   Allows import of assemblies created using the Opalis QIK CLI Wizard or by the Orchestrator Command-Line Activity Wizard and automatically converts assemblies to be compatible with Orchestrator.  

-   Improved field validation to avoid compile-time errors.  

#### Integration Pack Wizard  

-   Allows import of IPs created using the Opalis QIK IP Wizard and automatically converts IPs to be compatible with Orchestrator.  

-   Allows side-by-side installation of multiple versions of the same IP. When using an imported IP file and deselecting **upgrade from previous versions**, the IP and all activities are given new IDs, which allows for multiple versions to exist simultaneously.  

-   Allows installation of IPs and dependent files with identical file names. The installation automatically deploys assemblies and dependent files of an Integration Pack into an IP-specific folder to physically separate files of different IPs and prevent issues such as overwriting existing files.  

-   The wizard now supports upgrade from any version. It is not necessary to provide a previous version number, so the **Upgrade from** version number inputs have been removed from the wizard.  

-   IPs created using the wizard are limited to installation on Orchestrator.  

-   IPs created using the wizard detect the Orchestrator installation path and install there.  

-   Improved field validation to avoid compile-time errors.  

-   All sample icons have been replaced with new *generic* icons which are more *verb-based* rather than being copies of existing activity icons. You can also resize the icon viewer dialog in the wizard to see more icons at the same time.  

-   The **License Key** feature of Integration Packs has been removed.  

-   The Integration Toolkit no longer includes the binaries for the Windows Installer XML (WiX) Toolset, used by the IP Wizard for creating the Windows Installer files within Integration Packs. This set of tools is now a prerequisite installation, required prior to installing the Toolkit. However, if WiX is subsequently uninstalled, the Integration Pack wizard will fail with an error message directing you to download and install WiX. The Integration Toolkit supports version 3.5 of the WiX Toolset. The WiX Toolset can be downloaded from [http://wix.codeplex.com](http://wix.codeplex.com).  

#### Toolkit Integration Packs  

-   Installation limited to Orchestrator systems.  

-   Activities detect usage of assemblies not compatible with Orchestrator and prevents loading.  

-   The Integration Pack for Java-based activities is no longer available.  

### Resolved Issues  

#### Command-Line Activity Wizard  

-   Now accepts double quote characters **(")** in command lines without failing at compile time.  

-   Special characters, such as **"$$"** are no longer removed from command lines.  

-   The **Echo as published data** checkbox has been removed from the wizard. It had errantly been placed there and did not represent an actual feature of the product.  

#### Integration Pack Wizard  

-   Fixed an issue where the files from an IP were not removed when the IP was uninstalled.  

### Known Issues  

#### Integration Pack Wizard  

-   When packaging an IP that contains commands created via the Command-Line Activity Wizard that utilize the SSH Command option, all of the SSH commands must be within a single CLI assembly. If the IP contains more than one assembly that uses SSH commands, only the first assembly’s commands will function.  

## Activity and IP Compatibility with Orchestrator  
 System Center Orchestrator Integration Toolkit has undergone some significant changes in the underlying framework since the previous release as the Opalis Quick Integration Kit. These changes make activities created using the CLI Wizard and activities developed using the Opalis API, as well as Integration Packs packed by the QIK Wizard incompatible with Orchestrator. In order to utilize these activities in Orchestrator, they must be converted to use the new framework. The manner in which these activities were created determines the process required to convert them:  

-   Activities created using the QIK CLI Wizard and used in workflows via the **Invoke .NET** activity need simply to be loaded and regenerated using the new Command-Line Activity Wizard. The required process is defined in the section QIK CLI Activity Migration.  

-   Activities created using the QIK CLI Wizard and then packaged into an Integration Pack using the QIK Wizard require a two-step process. This includes regenerating the assembly or assemblies for the activities using the process defined in QIK CLI Activity Migration, and then repackaging the IP using the new Integration Pack Wizard using the process defined in QIK IP Migration.  

-   Activities developed using the Opalis API and then packaged into an Integration Pack using the QIK Wizard also require a two-step process which involves modifying the source code using the process defined in QIK API Custom Activity Migration, and repackaging the IP using the new Integration Pack Wizard using the process defined in QIK IP Migration.  

## See Also  
 [Orchestrator documentation](../learn-about-orchestrator.md)   
 [Orchestrator Integration Packs](../list-of-orchestrator-integration-packs.md)      
 [Orchestrator SDK](https://msdn.microsoft.com/en-us/library/hh855054.aspx)
