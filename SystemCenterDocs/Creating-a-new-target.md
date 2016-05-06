---
title: Creating a new target
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 22b0f17b-5dba-4ccf-9a6c-307b161b5570
---
# Creating a new target
There are multiple methods that you can use to create a new class that can be used as a target for monitors and rules in [!INCLUDE[om12long](../Token/om12long_md.md)]. You can use a separate tool such as [MP Author](http://www.mpauthor.com)that will allow you to directly create targets. Advanced authors can refer to the [Service Model](http://aka.ms/mpauthor#Service_Model) section of the [System Center Management Pack Authoring Guide](http://aka.ms/mpauthor) for detailed information on creating a complex class model for their application. This advanced information is not required though to create a basic class that can act as a target for monitors and rules specific to a particular application.

## Management Pack Templates
The following management pack templates in the Operations console create a class that can be used as a target for monitors and rules:

### Windows Service Template
If your application has service a Windows installed on each server, then you should use the [Windows Service Template](../Topic/Windows-Service-Template.md). This will create a new class and discover an instance on all agent computers with the service installed. If any monitors or rules use this class as a target, then they will run on those same agents.

### Process Monitoring Template
If your application does not have a Windows service but does have a process that is running on the agent computer, then you should use the [Process Monitoring Template](../Topic/Process-Monitoring-Template.md). This will create a new class and discover an instance on all computers in a specified group. If any monitors or rules use this class as a target, then they will run on those same agents.

### Unix\/Linux Service
If your application has a service on a Unix or Linux server, then you should use the [UNIX or Linux Process](../Topic/UNIX-or-Linux-Process.md) template. This will create a new class and discover an instance on all agent computers with the service installed.

## Simple class using Authoring Console
The [System Center Operations Manager 2007 R2 Authoring Console](../Topic/Authoring-Tools.md#AuthoringConsole) is typically used by advanced users for custom management packs. It can be used though to create a simple class and discovery that you can then install in your management group and perform further authoring using the Operations console.

In addition to the class, you must create a discovery so that instances of the class can be created on agents where the application is installed. The Authoring Console provides a wizard that creates a discovery based on the Windows registry. This will allow you to specify criteria such as the name of a registry key. If the key is present, then the application is installed, and an instance of the class should be created.

#### To create a class and discovery in the Authoring Console

1.  Open the Authoring Console.

2.  Select **File** and then **New**.

3.  On the **Management Pack Template** page, do the following:

    1.  In the **Select a Management Pack Template** pane, select **Windows Application \(Registry\)**.

    2.  For the **Management Pack Identity**, type a name such as **Contoso.MyApplication**.

        > [!NOTE]
        > This name may not contain spaces and should start with the name of the management pack.

    3.  Click **Next**.

4.  On the **Name and Description** page, type a **Display Name** such as **Contoso My Application** for the management pack and click **Next**.

5.  On the **Windows Application** page, do the following:

    1.  In the **ID** box, type a unique ID for the new class such as *Contoso.MyApplication.MyTarget*.

        > [!NOTE]
        > This name may not contain spaces and should start with the name of the management pack.

    2.  In the **Display Name** box, type a display name for the new class such as *My Application Target*

    3.  Click **Next**.

6.  On the **Discovery Schedule** page, set the schedule to 1 hour or more and click **Next**.

    > [!NOTE]
    > This is the frequency that registry criteria on the agent computer will be evaluated to determine if an instance of the class should be created.

7.  On the **Registry Probe Configuration** page, do the following:

    > [!NOTE]
    > On this page, you specify the registry keys and values that your criteria will use.

    1.  Click **Add**.

    2.  Leave the **Object Type** set to **Key**.

    3.  In the **Name** box, type a name such as **KeyExists**.

        > [!NOTE]
        > You can use any name that is descriptive. The name is not displayed to the user and is only used on the next page of the wizard.

    4.  In the **Path** box, type the path of the registry key to check such as **SOFTWARE\\MyApplication**.

    5.  In the **Attribute Type** box, select **Check if exists**.

    6.  Click **Next**.

8.  On the **Expression Filter** page, do the following:

    > [!NOTE]
    > On this page, you specify the criteria for evaluating the registry data collected on the previous page.

    1.  Click **Insert**.

    2.  Click the ellipse button next to **Parameter Name** and select **KeyExists**.

    3.  In the **Operator** box, select **Equals**.

    4.  In the **Value** box, type **True**.

    5.  Click **Create**.

#### To install the management pack from the Authoring Console

1.  Select **Tools** and then **Export MP to Management Group**.

2.  Select or type in the name of a management server for your management group.

3.  Click **Connect**.

## See Also
[Understanding Classes and Objects](../Topic/Understanding-Classes-and-Objects.md)
[Selecting a target](../Topic/Selecting-a-target.md)
[Management Pack Templates](../Topic/Management-Pack-Templates.md)

