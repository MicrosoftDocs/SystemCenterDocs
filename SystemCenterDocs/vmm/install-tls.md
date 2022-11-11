---
ms.assetid: 857ab713-df3e-4744-aac9-e057efc0fce7
title: Set up TLS for VMM
description: This article provides instructions for setting up TLS with VMM
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 05/12/2022
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
---

# Set up TLS for VMM

::: moniker range=">= sc-vmm-1801 <= sc-vmm-1807"

[!INCLUDE [eos-notes-virtual-machine-manager.md](../includes/eos-notes-virtual-machine-manager.md)]

::: moniker-end

This article describes how to set up Transport Security Layer (TLS) protocol version 1.2 with System Center - Virtual Machine Manager (VMM) server.

>[!NOTE]
> Virtual Machine Manager will use the protocol configured at the Operating System Level. For example, if TLS 1.0, TLS 1.1, and TLS 1.2 are enabled at the Operating System Level, then Virtual Machine Manager will select one of the three protocols in the following order of preference:
> 1.	TLS version 1.2
> 2.	TLS version 1.1
> 3.	TLS version 1.0
>
> The [Schannel SSP](/windows-server/security/tls/tls-ssl-schannel-ssp-overview) then selects the most preferred authentication protocol that the client and server can support.

## Before you start

::: moniker range="sc-vmm-2016"
- VMM should be running VMM 2016 with [Update Rollup 4](https://support.microsoft.com/help/4041074), or later.
::: moniker-end
- Security fixes should be up-to-date on the VMM server, and the server running the VMM database.
- The VMM server should be running . NET version 4.6. Follow [these instructions](/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed) to determine which version of .NET is installed.
- To work with TLS 1.2, System Center components generate SHA1 or SHA2 self-signed certificates. If SSL certificates from a certificate authority (CA) certificates are used, they should use SHA1 or SHA2.

## Install a SQL Server update for TLS 1.2 support

1. Open [KB 3135244](https://support.microsoft.com/help/3135244).
2. [Download and install](https://support.microsoft.com/help/3135244) the update for your SQL Server version.
    - You don't need this update if you're running SQL Server 2016.
    - SQL Server 2008 R2 doesn't support TLS 1.2.


## Configure the VMM server to use TLS 1.2

Disable all SCHANNEL protocols except for TLS 1.2.

### Manually modify the registry

1. Open the Registry Editor, and navigate to HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols.
2. Right-click **Protocol**, select **New** > **Key**. Type in the key and press Enter. Perform this procedure to create the following keys:
    - **SSL3**
    - **TLS 1.0**
    - **TLS 1.1**
    - **TLS 1.2**
3. After you've created these keys, you need to create the **Client** and **Server** keys under them.
    - For **SSL3**, select **New** > **Key**. Type in **Client** and press enter.  Again, for **SSL3**, select **New** > **Key** again. Then type in **Server** and press Enter.
    - Repeat the action to create the **Client** and **Server** keys under **TLS 1.0**, **TLS 1.1**, and **TLS 1.2**.
4. After you've created the **Client** and **Server** keys,  you need to create DWORD values under them, in order to enable and disable protocols. Do this as follows:
    - Enable the TLS 1.2 protocol. To do this, in **TLS 1.2**, under the **Client** key, create the DWORD value **DisabledByDefault**, and set the value to 0. Now create a DWORD value **Enabled**, and set the value to 1. Create the same DWORD values under the **Server** key.
    - Now disable the other protocols. To do this, in **SSL3**, **TLS 1.0** and **TLS 1.1**, under the **Client** key, create the DWORD value **DisabledByDefault**, and set the value to 1. Now create a DWORD value **Enabled**, and set the value to 0. Create the same DWORD values under the **Server** key.

### Modify the registry with a PowerShell script  

Instead of modifying the registry values manually, you can use the following PowerShell script.

```
$ProtocolList       = @("SSL 2.0", "SSL 3.0", "TLS 1.0", "TLS 1.1", "TLS 1.2")
$ProtocolSubKeyList = @("Client", "Server")
$DisabledByDefault  = "DisabledByDefault"
$registryPath       = "HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\"

foreach ($Protocol in $ProtocolList)
{
	foreach ($key in $ProtocolSubKeyList)
	{
		$currentRegPath = $registryPath + $Protocol + "\" + $key
		Write-Output "Current Registry Path: `"$currentRegPath`""

		if (!(Test-Path $currentRegPath))
		{
			Write-Output " `'$key`' not found: Creating new Registry Key"
			New-Item -Path $currentRegPath -Force | out-Null
		}
		if ($Protocol -eq "TLS 1.2")
		{
			Write-Output " Enabling - TLS 1.2"
			New-ItemProperty -Path $currentRegPath -Name $DisabledByDefault -Value "0" -PropertyType DWORD -Force | Out-Null
			New-ItemProperty -Path $currentRegPath -Name 'Enabled' -Value "1" -PropertyType DWORD -Force | Out-Null
		}
		else
		{
			Write-Output " Disabling - $Protocol"
			New-ItemProperty -Path $currentRegPath -Name $DisabledByDefault -Value "1" -PropertyType DWORD -Force | Out-Null
			New-ItemProperty -Path $currentRegPath -Name 'Enabled' -Value "0" -PropertyType DWORD -Force | Out-Null
		}
		Write-Output " "
	}
}

Exit 0
```

## Configure VMM to use TLS 1.2

1. Open the registry editor on the VMM server. Navigate to **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ .NetFramework\v4.0.30319**.
2. Create the DWORD value **SchUseStrongCrypto**, and set the value to 1.
3. Now navigate to
   <strong>HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\
   .NetFramework\v4.0.30319</strong>.
4. Under this location, create the same DWORD value **SchUseStrongCrypto**, and set the value to 1.
5. Restart the server for the settings to take effect.

### Modify the registry with a PowerShell script

You can modify the registry settings using the following PowerShell script.

```
# Tighten up the .NET Framework
$NetRegistryPath = "HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319"
New-ItemProperty -Path $NetRegistryPath -Name "SchUseStrongCrypto" -Value "1" -PropertyType DWORD -Force | Out-Null

$NetRegistryPath = "HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319"
New-ItemProperty -Path $NetRegistryPath -Name "SchUseStrongCrypto" -Value "1" -PropertyType DWORD -Force | Out-Null
```

## Next steps

[Learn more](https://tools.ietf.org/html/rfc5246) about the TLS 1.2 protocol.
