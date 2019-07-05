---
ms.assetid: 958fdc2f-73b1-4648-94d0-b9c45b51b719
title: Set up TLS for Orchestrator
description: This article provides instructions for setting up TLS with Orchestrator
author: JYOTHIRMAISURI
ms.author: v-jysur
manager: carmonm
ms.date: 07/05/2019
ms.topic: article
ms.prod: system-center
ms.technology: Orchestrator
---

# Set up TLS for Orchestrator

This article describes how to set up Transport Security Layer (TLS) protocol version 1.2 with System Center - Orchestrator


## Before you start

Ensure the following:

- Orchestrator should be running version 2016 with Update Rollup 4 or later/1801/1807/2019.
- Security fixes should be up-to-date on the Orchestrator.
- System Center updates are up-to-date.
- SQL Server 2012 Native client 11.0 or later is installed on the Orchestrator management server. To download and install Microsoft SQL Server 2012
  Native Client 11.0, see [this Microsoft Download Center webpage](https://www.microsoft.com/en-us/download/details.aspx?id=50402&751be11f-ede8-5a0c-058c-2ee190a24fa6=True).
- Orchestrator should be runnning .NET version 4.6. Follow [these instructions](https://docs.microsoft.com/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed.md) to determine which version of .NET is installed.
- To work with TLS 1.2, System Center components generate SHA1 or SHA2 self-signed certificates. If SSL certificates from a certificate authority (CA) certificates are used, they should use SHA1 or SHA2.
- Install the SQL server version that supports TLS 1.2. SQL Server 2016 or later supports TLS 1.2.

## Install a SQL Server update for TLS 1.2 support

1. Open [KB 3135244](https://support.microsoft.com/help/3135244).
2. [Download and install](https://support.microsoft.com/help/3135244) the update for your SQL Server version.
    - You don't need this update if you're running SQL Server 2016 or later.
    - SQL Server 2008 R2 doesn't support TLS 1.2.


## Configure Orchestrator to use TLS 1.2
Follow these steps:

1. Set Windows to use only TLS 1.2.

   **Method 1: Manually modify the registry**

   >[!Important]
   >Carefully follow the steps in this section. You could cause serious problems if you modify the registry incorrectly. Before you begin, back up the registry so you can restore it if a problems occurs.

   Use the following steps to enable or disable all SCHANNEL protocols across the system.

   >[!NOTE]
   >We recommend that you enable the TLS 1.2 protocol for incoming communications. Enable the TLS 1.2, TLS 1.1, and TLS 1.0 protocols for all outgoing communications. Registry changes don't affect the use of the Kerberos protocol or NTLM protocol.

   a. Start Registry Editor. To do this, right-click **Start**, type **regedit** in the Run box, and then select **OK**.

   b. Locate the following registry subkey:          
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

   c. Right-click  **Protocol**, and point to **New** > **Key**.

      ![New registry key](./media/integration-pack-for-om/new-registry-key.png)

   d. Enter **SSL 3.0**.

   e. Repeat the previous two steps to create keys for TLS 0, TLS 1.1, and TLS 1.2. These keys resemble directories.

   f. Create a client key and a server key under each of the SSL 3.0, TLS 1.0, TLS 1.1, and TLS 1.2 keys.

   g. To enable a protocol, create the DWORD value under each client and server key, as follows:

   - DisabledByDefault [Value = 0]
   - Enabled [Value = 1]

   h. To disable a protocol, change the DWORD value under each client and server key, as follows:

   - DisabledByDefault [Value = 1]
   - Enabled [Value = 0]

   i. Select **File** > **Exit**.

   **Method 2: Automatically modify the registry**

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

2. Set System Center to use only TLS 1.2.

   Before you change the registry in this step, back up the registry in case you need to restore it later. Then set the following registry key values.

   **Values for 64-bit operating systems**

   | Path | Registry key | Value |
   | --- | --- | --- |
   |HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727 | SystemDefaultTlsVersions | dword:00000001 |
   |HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727 | SystemDefaultTlsVersions | dword:00000001 |
   | HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319 | SystemDefaultTlsVersions | dword:00000001 |
   | HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319 | SystemDefaultTlsVersions | dword:00000001 |

   **Values for 32-bit operating systems**

   | Path   |Registry key  | Value |
   | --- | --- | --- |
   | HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319 | SystemDefaultTlsVersions | dword:00000001 |
   | HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\.NETFramework\ v2.0.50727 | SystemDefaultTlsVersions | dword:00000001 |

3. Install the following updates on all Service Manager roles. Update roles on management servers, Azure Data Warehouse servers, the Self-Service portal, and Analyst consoles (including the Analyst consoles installed on the Orchestrator Runbook servers).

   | Operating system | Required update |
   | --- | --- |
   | Windows 8.1 and Windows Server 2012 R2 | [3154520](https://apac01.safelinks.protection.outlook.com/?url=https%3A%2F%2Fsupport.microsoft.com%2Fen-in%2Fhelp%2F3154520&amp;data=02%7C01%7Cv-anesh%40microsoft.com%7C5311298568114da9a70b08d6ab9d2a60%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636885088873390534&amp;sdata=4zmUO0R60zFAV339V1nYhf32MQRpCoxPEiEmUsNn5LM%3D&amp;reserved=0) Support for TLS System Default Versions included in the .NET Framework 3.5 on Windows 8.1 and Windows Server 2012 R2 |
   | Windows Server 2012 | [3154519](https://apac01.safelinks.protection.outlook.com/?url=https%3A%2F%2Fsupport.microsoft.com%2Fen-in%2Fhelp%2F3154519&amp;data=02%7C01%7Cv-anesh%40microsoft.com%7C5311298568114da9a70b08d6ab9d2a60%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636885088873390534&amp;sdata=Om3y93IekKZdW6%2FTt8Arerz1loDOsW3L6LE%2F5bd69dY%3D&amp;reserved=0) Support for TLS System Default Versions included in the .NET Framework 3.5 on Windows Server 2012 |
   | Windows 7 SP1 and Windows Server 2008 R2 SP1 | [3154518](https://apac01.safelinks.protection.outlook.com/?url=https%3A%2F%2Fsupport.microsoft.com%2Fen-in%2Fhelp%2F3154518&amp;data=02%7C01%7Cv-anesh%40microsoft.com%7C5311298568114da9a70b08d6ab9d2a60%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636885088873400526&amp;sdata=i1drbmxTit4RkFEKTaEKVTytzWpjAs3dg5DXD2DuH8Y%3D&amp;reserved=0) Support for TLS System Default Versions included in the .NET Framework 3.5.1 on Windows 7 SP1 and Server 2008 R2 SP1 |
   | Windows 10 and Windows Server 2016 | [3154521](https://apac01.safelinks.protection.outlook.com/?url=https%3A%2F%2Fsupport.microsoft.com%2Fen-in%2Fhelp%2F3154521&amp;data=02%7C01%7Cv-anesh%40microsoft.com%7C5311298568114da9a70b08d6ab9d2a60%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636885088873400526&amp;sdata=OfqEkrkocQeSqf2MIW9wKQkZI7mKgaIhpKkZI3%2Bptis%3D&amp;reserved=0) Hotfix rollup 3154521 for the .NET Framework 4.5.2 and 4.5.1 on Windows<br><br>[3156421](https://apac01.safelinks.protection.outlook.com/?url=https%3A%2F%2Fsupport.microsoft.com%2Fen-in%2Fhelp%2F3156421&amp;data=02%7C01%7Cv-anesh%40microsoft.com%7C5311298568114da9a70b08d6ab9d2a60%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636885088873410525&amp;sdata=6xGOexADeuoR49tyrMBzxweoVDX2JNkrBqEvpbrdIdw%3D&amp;reserved=0) Cumulative Update for Windows 10 Version 1511 and Windows Server 2016 Technical Preview 4: May 10, 2016 |

4. Restart the computer.

> [IMPORTANT]
>
> After you set Microsoft System Center Orchestrator to use only the TLS 1.2 protocol for connections, the Integration Packs stop working.
To fix this issue, follow these steps:

>1.	Start Registry Editor.
>2.	Locate the following registry subkey:
 *HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319*
>3.	Check whether the SystemDefaultTlsVersions value exists.
    -   If the value exists, make sure that its data is set to 1.
    -   If the value does not exist, create a DWORD (32-bit) value, and specify the following values:
        Name: SystemDefaultTlsVersions
        Value data: 1
>4.	Click **OK**.

For detailed information, see [this KB article](https://support.microsoft.com/en-us/help/4494803/orchestrator-integration-packs-stop-working-with-tls-1-2-connections).


## Next steps

[Learn more](https://tools.ietf.org/html/rfc5246) about the TLS 1.2 protocol.
