---
title: System Center - The Orchestrator integration pack for System Center Operations Manager
description: Learn about the integration pack for Operations Manager, an add-in provided by System Center Orchestrator.
ms.date: 04/04/2019
ms.prod: system-center
ms.technology: orchestrator
ms.topic: reference
author: rayne-wiselman
ms.author: raynew
manager: carmonm
---

# The integration pack for System Center Operations Manager

The integration pack for Operations Manager is an add-in provided by System Center Orchestrator. Use the integration pack to connect an Orchestrator Runbook server to an Operations Manager management server so you can automate various actions.

For more information about integration packs, see the [System Center integration guide](https://go.microsoft.com/fwlink/?LinkID=275796).

## Set up your system

Before you deploy the Operations Manager integration pack, install and configure the following software:

- Orchestrator.
- Operations Manager. The integration pack version should match the System Center version.

    >[!NOTE]
    > If you use the Orchestrator 2016, version 1801, integration pack for Operations Manager 2016 UR4 or later, you'll need to [change the registry](#enable-sco-ip-for-operations-manager-2016-ur4-and-later) if you've configured Operations Manager to accept only TLS 1.1 or 1.2 connections.

    On each computer where an Orchestrator Runbook server or Runbook Designer needs to interact with Operations Manager, install the Operations Manager console.

The Create Alert object requires the Orchestrator integration library management pack. The Create Alert object automatically installs this management pack in Operations Manager the first time it runs. If you want to uninstall the integration pack, remove the Orchestrator integration library management pack from Operations Manager.


## Download the integration pack

Download an integration pack for your software version: 

- [The pack for 2019](https://www.microsoft.com/download/details.aspx?id=58111&WT.mc_id=rss_alldownloads_all)
- [The pack for 1801](https://www.microsoft.com/download/details.aspx?id=56605)
- [The pack for 2016](https://www.microsoft.com/download/details.aspx?id=54098)

## Register and deploy the pack

After you download the integration pack file, register it with the Orchestrator management server. Then deploy it to Runbook servers and Runbook Designer computers. For more information, see [Add an integration pack](how-to-add-an-integration-pack.md).

## Configure the connections

A connection establishes a reusable link between Orchestrator and an Operations Manager management server. Create as many connections as you need to specify links to multiple Operations Manager management servers. You can also create multiple connections to the same server to allow for differences in security permissions for user accounts.

To configure a connection:

1.  In Runbook Designer, select **Options** > **Operations Manager**.
2.  On the **Connections** tab, select **Add**.
3.  In **Connection Entry**, in the  **Name** box, type the name or IP address of the server that runs Operations Manager.
4.  In the **Domain** box, type the domain name of the Operations Manager server. Or select the ellipsis button (...) to browse for the domain, select it, and then select **Add**.
5.  In the **User name** and **Password** boxes, type the credentials that the Orchestrator server will use to connect to the Operations Manager server.
6. In **Monitoring Intervals\\Polling** and **Monitoring Intervals\\Reconnect**, accept the default value of 10 seconds, or change the value. The property **(default value: 10 seconds)** is configurable.
7.  Select **Test Connection**. When the confirmation message appears, select **OK**.
8.  Add more connections if necessary. 
1. Select **OK** > **Finish**.

## Enable SCO IP for Operations Manager 2016 UR4 or later

Enable SCO IP for Operations Manager 2016 (UR4 or later) when your Operations Manager configuration accepts only TLS 1.1 or TLS 1.2.

Follow these steps:

1. Set Windows to use only TLS 1.2.
1. Set System Center to use only TLS 1.2.
1. Install updates.
1. Restart the computer.

Find details about these steps in the next sections.

### Set Windows to use only TLS 1.2

#### Method 1: Manually modify the registry**

    > [!Important]
    > Carefully follow the steps in this section. You could cause serious problems if you modify the registry incorrectly. Before you begin, back up the registry so you can restore it if a problems occurs.

Use the following steps to enable or disable all SCHANNEL protocols across the system.

    >[!NOTE]
    > We recommend that you enable the TLS 1.2 protocol for incoming communications. Enable the TLS 1.2, TLS 1.1, and TLS 1.0 protocols for all outgoing communications. 

    > Registry changes don't affect the use of the Kerberos protocol or NTLM protocol.

1. Start Registry Editor. To do this, right-click **Start**, type **regedit** in the Run box, and then select **OK**.

1. Locate the following registry subkey:   HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

1. Right-click  **Protocol**, and point to **New** > **Key**.

    ![Screenshot of Registry Editor, showing how to create a new registry key](./media/integration-pack-for-om/new-registry-key.png)

1. Enter **SSL 3.0**.

1. Repeat the previous two steps to create keys for TLS 0, TLS 1.1, and TLS 1.2. These keys resemble directories.

1. Create a client key and a server key under each of the SSL 3.0, TLS 1.0, TLS 1.1, and TLS 1.2 keys.

1. To enable a protocol, create the DWORD value under each client and server key, as follows:

    - DisabledByDefault [Value = 0]
    - Enabled [Value = 1]

1. To disable a protocol, change the DWORD value under each client and server key, as follows:

    - DisabledByDefault [Value = 1]
    - Enabled [Value = 0]

1. Select **File** > **Exit**.

#### Method 2: Automatically modify the registry

Run the following Windows PowerShell script in administrator mode to automatically configure Windows to use only the TLS 1.2 protocol:

    ```    
        $ProtocolList       = @("SSL 2.0","SSL 3.0","TLS 1.0", "TLS 1.1", "TLS 1.2")
        $ProtocolSubKeyList = @("Client", "Server")
        $DisabledByDefault = "DisabledByDefault"
        $Enabled = "Enabled"
        $registryPath = "HKLM:\\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\"

        foreach($Protocol in $ProtocolList)
        {
          Write-Host " In 1st For loop"
          foreach($key in $ProtocolSubKeyList)
          {		
              $currentRegPath = $registryPath + $Protocol + "\" + $key
              Write-Host " Current Registry Path $currentRegPath"

              if(!(Test-Path $currentRegPath))
              {
                  Write-Host "creating the registry"
                  New-Item -Path $currentRegPath -Force | out-Null			
              }
              if($Protocol -eq "TLS 1.2")
              {
                  Write-Host "Working for TLS 1.2"
                  New-ItemProperty -Path $currentRegPath -Name $DisabledByDefault -Value "0" -PropertyType DWORD -Force | Out-Null
                  New-ItemProperty -Path $currentRegPath -Name $Enabled -Value "1" -PropertyType DWORD -Force | Out-Null

              }
              else
              {
                  Write-Host "Working for other protocol"
                  New-ItemProperty -Path $currentRegPath -Name $DisabledByDefault -Value "1" -PropertyType DWORD -Force | Out-Null
                  New-ItemProperty -Path $currentRegPath -Name $Enabled -Value "0" -PropertyType DWORD -Force | Out-Null
              }
          }
        }

        Exit 0
    ```

### Set System Center to use only TLS 1.2

Before you change the registry in this step, back up the registry in case you need to restore it later. Then set the following registry key values. 

#### Values for 64-bit operating systems

    | Path | Registry key | Value |
    | --- | --- | --- |
    |HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727 | SystemDefaultTlsVersions | dword:00000001 |
    |HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727 | SystemDefaultTlsVersions | dword:00000001 |
    | HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319 | SystemDefaultTlsVersions | dword:00000001 |
    | HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319 | SystemDefaultTlsVersions | dword:00000001 |

#### Values for 32-bit operating systems

    | Path   |Registry key  | Value |
    | --- | --- | --- |
    | HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319 | SystemDefaultTlsVersions | dword:00000001 |
    | HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\.NETFramework\ v2.0.50727 | SystemDefaultTlsVersions | dword:00000001 |

### Install updates 

Install the following updates on all Service Manager roles. Update roles on management servers, Azure Data Warehouse servers, the Self-Service portal, and Analyst consoles (including the Analyst consoles installed on the Orchestrator Runbook servers).


    | Operating system | Required update |
    | --- | --- |
    | Windows 8.1 and Windows Server 2012 R2 | [3154520](https://apac01.safelinks.protection.outlook.com/?url=https%3A%2F%2Fsupport.microsoft.com%2Fen-in%2Fhelp%2F3154520&amp;data=02%7C01%7Cv-anesh%40microsoft.com%7C5311298568114da9a70b08d6ab9d2a60%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636885088873390534&amp;sdata=4zmUO0R60zFAV339V1nYhf32MQRpCoxPEiEmUsNn5LM%3D&amp;reserved=0) Support for TLS System Default Versions included in the .NET Framework 3.5 on Windows 8.1 and Windows Server 2012 R2 |
    | Windows Server 2012 | [3154519](https://apac01.safelinks.protection.outlook.com/?url=https%3A%2F%2Fsupport.microsoft.com%2Fen-in%2Fhelp%2F3154519&amp;data=02%7C01%7Cv-anesh%40microsoft.com%7C5311298568114da9a70b08d6ab9d2a60%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636885088873390534&amp;sdata=Om3y93IekKZdW6%2FTt8Arerz1loDOsW3L6LE%2F5bd69dY%3D&amp;reserved=0) Support for TLS System Default Versions included in the .NET Framework 3.5 on Windows Server 2012 |
    | Windows 7 SP1 and Windows Server 2008 R2 SP1 | [3154518](https://apac01.safelinks.protection.outlook.com/?url=https%3A%2F%2Fsupport.microsoft.com%2Fen-in%2Fhelp%2F3154518&amp;data=02%7C01%7Cv-anesh%40microsoft.com%7C5311298568114da9a70b08d6ab9d2a60%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636885088873400526&amp;sdata=i1drbmxTit4RkFEKTaEKVTytzWpjAs3dg5DXD2DuH8Y%3D&amp;reserved=0) Support for TLS System Default Versions included in the .NET Framework 3.5.1 on Windows 7 SP1 and Server 2008 R2 SP1 |
    | Windows 10 and Windows Server 2016 | [3154521](https://apac01.safelinks.protection.outlook.com/?url=https%3A%2F%2Fsupport.microsoft.com%2Fen-in%2Fhelp%2F3154521&amp;data=02%7C01%7Cv-anesh%40microsoft.com%7C5311298568114da9a70b08d6ab9d2a60%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636885088873400526&amp;sdata=OfqEkrkocQeSqf2MIW9wKQkZI7mKgaIhpKkZI3%2Bptis%3D&amp;reserved=0) Hotfix rollup 3154521 for the .NET Framework 4.5.2 and 4.5.1 on Windows<br><br>[3156421](https://apac01.safelinks.protection.outlook.com/?url=https%3A%2F%2Fsupport.microsoft.com%2Fen-in%2Fhelp%2F3156421&amp;data=02%7C01%7Cv-anesh%40microsoft.com%7C5311298568114da9a70b08d6ab9d2a60%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636885088873410525&amp;sdata=6xGOexADeuoR49tyrMBzxweoVDX2JNkrBqEvpbrdIdw%3D&amp;reserved=0) Cumulative Update for Windows 10 Version 1511 and Windows Server 2016 Technical Preview 4: May 10, 2016 |

After you install the updates, restart the computer.
