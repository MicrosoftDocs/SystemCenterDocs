---
title: Set up client auto deployment
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce00b745-c1fe-449b-9d8e-47507ce20b96
---
# Set up client auto deployment
In large environments  with many client computers you can automate the deployment and protection of laptop computers using the client auto\-deployment management pack

## Prerequisites
You’ll need the following:

1.  One or more DPM servers

2.  An Operations Manager server

3.  A Configuration Manager server

4.  The [ClientAD.msi](http://go.microsoft.com/fwlink/?LinkId=207880) file to set up the management pack.

## Deployment steps
Set up DPM client auto deployment as follows:

1.  **Install the**[ClientAD.msi](http://go.microsoft.com/fwlink/?LinkId=207880) on the Operations Manager server

2.  **[Configure settings on the Operation Manager server](#BKMK_OM)**—Specify the domains that contain client computers you want to protect with DPM, and configure exclusions for client computers that you don’t want to protect in these domains. Then configure protection groups.

3.  **Import the management pack on the Operations Manager server**—After configuring settings you’ll need to import the management pack in order to use it. For more information see [How to import a management pack](http://go.microsoft.com/fwlink/?LinkId=207699).

4.  **Set up the DPM server**—On the DPM server, install the Operations Manager agent. In addition you might need also need to add more disks and storage for the protection groups. For more information see [Process Manual Agent Installations](http://go.microsoft.com/fwlink/?LinkID=207703) and [Configure disk storage and storage pools](assetId:///a9b893b9-bf55-4eab-b03a-4abcf7923a93).

5.  **[Add the DPM server on the Operations Manager server](#BKMK_AddDPM)**—On the Operations Manager server, include the DPM server for auto\-deployment.

6.  **[Set up Configuration Manager](#BKMK_SetCM)**—Set up Configuration Manager so that it installs the DPM protection agent on client computers.

### <a name="BKMK_OM"></a>Configure the Operations Manager server

#### <a name="BKMK_ConfigureDomains"></a>Specify the domains

1.  Open the file **DomainsForAutoDeployment.txt** from \\Program Files\\Microsoft Data Protection Manager\\Auto Deployment\\Config on the System Center Operations Manager server.

2.  Add new line separated entries for the domains from which you want to protect laptop computers.

    Wildcard characters are supported. For example. client\*.corp.contoso.com includes protection of all clients whose name starts with word ‘client’ in the domain corp.contoso.com

#### <a name="BKMK_ConfigureExclusions"></a>Configure exclusions

1.  Open the file **Exclusions.txt** from \\Program Files\\Microsoft Data Protection Manager\\Auto Deployment\\Config on the System Center Operations Manager server.

2.  Add new line separated client system FQDNs for clients which you don’t want to perform auto protection.

    Wildcard characters are supported. For example. client\*.corp.contoso.com excludes protection of all clients whose name starts with word ‘client’ in the domain corp.contoso.com

#### <a name="BKMK_ConfigurePG"></a>Configure protection groups

1.  Open the file **ClientPGSettings.xml** from \\Program Files\\Microsoft Data Protection Manager\\Auto Deployment\\Config on the System Center Operations Manager server. This file has the default settings with which a protection group is created.

2.  Edit the details here such as per laptop size, and so on, to set new settings.

    All protection groups created for all [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] servers involved in auto protection will use these configuration settings.

### <a name="BKMK_AddDPM"></a>Add the DPM server

1.  On the System Center Operations Manager console, go to the **Monitoring** view, expand **DPM Client Auto Deployment**, and then select **Auto deployment DPM server state**.

2.  On the main pane, select the DPM server you want to include. On the **Actions** pane, click **Include DPM for auto deployment**.

    You can also select **Exclude DPM for auto deployment** to remove a DPM server.

### <a name="BKMK_SetCM"></a>Set up Configuration Manager

1.  Download the System Center Configuration Manager integration program.

2.  Open an elevated command prompt and run the following command: SCCMClientAD.exe –s <Time of daily run><Day of global run><Share path><Configuration Manager site code>.

