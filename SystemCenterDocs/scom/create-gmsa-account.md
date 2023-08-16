---
ms.assetid: 
title: Create an instance of Azure Monitor SCOM Managed Instance (preview)
description: This article describes how to create a SCOM managed instance to monitor workloads by using System Center Operations Manager functionality on Azure.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 08/16/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Create gMSA account

This article describes how to create an instance of the service (a SCOM managed instance) with System Center Operations Manager functionality in Azure.

In on-premises Active directory, create gMSA account and Computer Group, domain user account.

## Active directory prerequisites

>[!Note]
>- To perform Active Directory operations, install the **RSAT: Active Directory Domain Services and Lightweight Directory Tools** feature. Then install the **Active Directory Users and Computers** tool. You can install this tool on any machine that has domain connectivity. You must sign in to this tool with admin permissions to perform all Active Directory operations.
>- To perform operations on the DNS server, you need to sign in to the DNS server and run the **DNS Manager** tool.

### Configure a domain account in Active Directory

Create a domain account in your Active Directory instance. The domain account is a typical Active Directory account. (It can be a non-admin account.) You'll use this account to add the System Center Operations Manager management servers to your existing domain.

:::image type="Active directory users" source="media/create-gmsa-account/active-directory-users.png" alt-text="Screenshot of Active Directory users.":::

Ensure that this account has the [permissions](/windows/security/threat-protection/security-policy-settings/add-workstations-to-domain) to join other servers to your domain. You can use an existing domain account if it has these permissions.

You'll use the configured domain account in later steps for creating a SCOM managed instance.

### Create and configure a computer group

Create a computer group in your Active Directory instance. For more information, see [Create a group account in Active Directory](/windows/security/threat-protection/windows-firewall/create-a-group-account-in-active-directory). All the management servers that you create will be a part of this group so that all the members of the group can retrieve group managed service account (gMSA) credentials. (You'll create these credentials in later steps.) The group name can't contain spaces and must have alphabet characters only.

:::image type="Active directory computers" source="media/create-gmsa-account/active-directory-computers.png" alt-text="Screenshot of Active Directory computers.":::

To manage this computer group, provide permissions to the domain account that you created. Follow these steps to provide permissions:

1. Select the group properties, and then select **Managed By**.
1. For **Name**, enter the name of the domain account.
1. Select the **Manager can update membership list** checkbox.

:::image type="Server group properties" source="media/create-gmsa-account/server-group-properties.png" alt-text="Screenshot of server group properties.":::

### Create a static IP and configure the DNS name

For all the System Center Operations Manager components to communicate with the load balancer that the SCOM Managed Instance (preview) service will create, you need a static IP and DNS name for the load balancer's front-end configuration.

Ensure that the static IP is in the subnet that you created during virtual network creation. Create a DNS name (according to your organization's policy) for the static IP.

:::image type="DNS manager" source="media/create-gmsa-account/dns-manager.png" alt-text="Screenshot of host information in DNS Manager.":::

### Create and configure a gMSA account

Create a gMSA to run the management server services and to authenticate the services. Use the following PowerShell command to create a gMSA service account:

```powershell
New-ADServiceAccount ContosogMSA -DNSHostName "ContosoLB.aquiladom.com" -PrincipalsAllowedToRetrieveManagedPassword "ContosoServerGroup" -KerberosEncryptionType AES128, AES256 -ServicePrincipalNames MSOMHSvc/ContosoLB.aquiladom.com, MSOMHSvc/ContosoLB, MSOMSdkSvc/ContosoLB.aquiladom.com, MSOMSdkSvc/ContosoLB 
```

In that command:
- `ContosogMSA` is the gMSA name. 
- `ContosoLB.aquiladom.com` is the DNS name for the load balancer (specified previously).
- `ContosoServerGroup` is the computer group in Active Directory (specified previously).
- `MSOMHSvc/ContosoLB.aquiladom.com`, `SMSOMHSvc/ContosoLB`, `MSOMSdkSvc/ContosoLB.aquiladom.com`, and `MSOMSdkSvc/ContosoLB` are service principal names.

>[!Note]
>If the gMSA name is longer than 14 characters, ensure that you set the `SamAccountName` less than 15 characters including the `$` sign.

Use the following command if the root key isn't effective:

```powershell
Add-KdsRootKey -EffectiveTime ((get-date).addhours(-10)) 
```

Ensure that the created gMSA account is a local admin account. If there are any GPO policies on the local admins at the Active Directory level, ensure that they have the gMSA account as the local admin.

>[!Important]
>To minimize the need for extensive communication with both your Active Directory admin and Network Admin, review  [**Self-verification**](/system-center/scom/scom-mi-self-verification-of-steps?view=sc-om-2022). The outlines the procedures through which the AD admin and network admin validate their configuration changes and ensure their successful implementation; thus, reducing unnecessary back-and-forth interactions with Operations Manager admin time.

## Next steps

- [Create a static IP](create-static-ip.md)

To provide feedback on SCOM Managed Instance (preview), use [this online form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
