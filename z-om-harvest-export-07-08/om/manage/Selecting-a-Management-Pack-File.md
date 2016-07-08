---
title: Selecting a Management Pack File
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e8c3975-e6d5-42c3-aa3f-1f666986688c
author:markgalioto
---
# Selecting a Management Pack File
When you create any monitoring in the Operations console, you have to specify a management pack file for the elements that you are creating. This topic describes a basic strategy that you can follow and provides additional details to help you understand the logic of the recommended strategy.  
  
## General Strategy  
For applications that already have a sealed management pack installed, typically management packs installed from the Management Pack Catalog:  
  
-   Create a separate management pack file to store overrides and new monitoring for that application.  
  
For applications that do not have a sealed management pack installed, typically management packs that you created yourself:  
  
-   Create a separate management pack file for each application. Use this file to store overrides and any new monitoring for that application.  
  
For common elements that are used by other management pack files, such as groups:  
  
-   Create a separate management pack file for each logical set of elements. Seal this management pack file before installing it.  
  
    > [!NOTE]  
    > If you created the management pack file in the Operations console, you must export it to an .xml file, and then seal it. You must then uninstall the unsealed management pack file from the management group before you install the sealed management pack file.  
  
## Default Management Pack  
The **Default Management Pack** file contains common elements such as views at the top level of the **Monitoring** workspace. This is an unsealed management pack file so that you can create views and folders at this level. It should not be used for any other purpose. For creating elements such as monitors and rules, create a new management pack file.  
  
## Logically Grouping Elements  
Although you could simply create a single management pack file to store all custom elements that you create, it is not a best practice. While management pack elements are treated individually by the agents that run them, the management group works with the management pack file. When a management pack file is installed in the management group or removed from it, it includes all of its management pack elements.  
  
When you determine how to group different elements, take the following considerations into account:  
  
-   Management pack files are delivered to any agent computer that requires at least one element in the file. If you use a single management pack file for different applications, elements might be delivered to agents that do not require them. The agent only actually loads the elements for the applications that it has installed, but the entire management pack file is delivered. Breaking up management pack files according to the elements that are relevant to a single application ensures the most efficient delivery of the files to agents.  
  
-   You can remove an application from your environment and no longer require its management pack. Or you can obtain a new management pack for an application and want to remove custom monitoring that you implemented. In cases like these, you can uninstall all of the elements for a particular application by removing any of its management pack files. If you combine elements for multiple applications, you limit your ability to manage the monitoring logic for a single application.  
  
-   You can develop and test some monitoring logic in a lab environment before moving it into a production management group. Combining elements for a particular application into a single management pack lets you manage that file through the different environments without affecting the monitoring for other applications.  
  
By following the recommend strategy for logically grouping management pack elements, you can ensure that your management group runs as efficiently as possible and can most effectively handle future changes.  
  
## Sealed and Unsealed Management Pack Files  
When selecting a management pack file, you must consider the implications of sealed and unsealed management packs. An element in one management pack file cannot refer to an element in another file if the file being referenced is not sealed. For this reason, you might have to group\-related elements in a single management pack file or seal management pack files meant for general use. For more information about the effects of sealing a management pack, see [Sealed Management Pack Files](../../om/manage/Sealed-Management-Pack-Files.md).  
  
Because a sealed management pack file cannot be modified, you can only store new management pack elements in unsealed files. Any management pack created in the Operations console is unsealed, and any dialog box prompting you for a management pack only includes unsealed files.  
  
For example, you might create a set of groups that represent different aspects of your computing environment such as the data center that certain computers reside in, the support personnel that manage particular computers, or the applications that different computers support. You want to use those groups to override monitors and rules that you created in different management pack files.  
  
If you used the Operations console to create the groups in this example in an unsealed management pack file, you could not use them with other management pack files. You have to use one of the following two strategies to implement this solution:  
  
-   Create groups in each management pack file with the overrides. This has the advantage of being easy to implement without any requirement to seal a management pack file, but it has the disadvantage of requiring you to potentially create multiple copies of the same group.  
  
-   Create a separate management pack file for the groups. After you create the groups in the Operations console, export the management pack to an .xml file, and then  seal the .xml file by using the process described in [Selecting a Management Pack File](../../om/manage/Selecting-a-Management-Pack-File.md). You can then install the sealed version of the management pack file so that the groups are available to any other management pack.  
  
## See Also  
[Management Pack Templates](../../om/manage/Management-Pack-Templates.md)  
[Monitors and Rules](../../om/manage/Monitors-and-Rules.md)  
  
