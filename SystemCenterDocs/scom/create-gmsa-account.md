---
ms.assetid: 
title: Create a computer group and gMSA account
description: This article describes how to create a gMSA account and computer group, domine user account in on-premises Active directory.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 09/05/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Create a computer group and gMSA account

This article describes how to create a gMSA account, computer group and domain user account in on-premises Active directory.

>[!Note]
> To know about the SCOM Managed Instance (preview) Architecture, see [Azure Monitor SCOM Managed Instance (preview)](operations-manager-managed-instance-overview.md).

## Active directory prerequisites

>[!Note]
>- To perform Active Directory operations, install the **RSAT: Active Directory Domain Services and Lightweight Directory Tools** feature. Then install the **Active Directory Users and Computers** tool. You can install this tool on any machine that has domain connectivity. You must sign in to this tool with admin permissions to perform all Active Directory operations.


### Configure a domain account in Active Directory

Create a domain account in your Active Directory instance. The domain account is a typical Active Directory account. (It can be a nonadmin account.) You'll use this account to add the System Center Operations Manager management servers to your existing domain.

:::image type="Active directory users" source="media/create-gmsa-account/active-directory-users.png" alt-text="Screenshot of Active Directory users.":::

Ensure that this account has the [permissions](/windows/security/threat-protection/security-policy-settings/add-workstations-to-domain) to join other servers to your domain. You can use an existing domain account if it has these permissions.

You'll use the configured domain account in later steps for creating a SCOM Managed Instance and subsequent steps.

### Create and configure a computer group

Create a computer group in your Active Directory instance. For more information, see [Create a group account in Active Directory](/windows/security/threat-protection/windows-firewall/create-a-group-account-in-active-directory). All the management servers that you create will be a part of this group so that all the members of the group can retrieve group managed service account (gMSA) credentials. (You'll create these credentials in later steps.) The group name can't contain spaces and must have alphabet characters only.

:::image type="Active directory computers" source="media/create-gmsa-account/active-directory-computers.png" alt-text="Screenshot of Active Directory computers.":::

To manage this computer group, provide permissions to the domain account that you created. Follow these steps to provide permissions:

1. Select the group properties, and then select **Managed By**.
1. For **Name**, enter the name of the domain account.
1. Select the **Manager can update membership list** checkbox.

     :::image type="Server group properties" source="media/create-gmsa-account/server-group-properties.png" alt-text="Screenshot of server group properties.":::

### Create and configure a gMSA account

Create a gMSA to run the management server services and to authenticate the services. Use the following PowerShell command to create a gMSA service account. DNS host name provided will also be used to configure the static IP and associate the same DNS name to static IP in [step8](create-static-ip.md).

```powershell
New-ADServiceAccount ContosogMSA -DNSHostName "ContosoLB.aquiladom.com" -PrincipalsAllowedToRetrieveManagedPassword "ContosoServerGroup" -KerberosEncryptionType AES128, AES256 -ServicePrincipalNames MSOMHSvc/ContosoLB.aquiladom.com, MSOMHSvc/ContosoLB, MSOMSdkSvc/ContosoLB.aquiladom.com, MSOMSdkSvc/ContosoLB 
```

In that command:
- `ContosogMSA` is the gMSA name. 
- `ContosoLB.aquiladom.com` is the DNS name for the load balancer (specified previously). Use the same DNS name to create the static IP and associate the same DNS name to static IP in [step8](create-static-ip.md).
- `ContosoServerGroup` is the computer group created above in Active Directory (specified previously).
- `MSOMHSvc/ContosoLB.aquiladom.com`, `SMSOMHSvc/ContosoLB`, `MSOMSdkSvc/ContosoLB.aquiladom.com`, and `MSOMSdkSvc/ContosoLB` are service principal names.

>[!Note]
>If the gMSA name is longer than 14 characters, ensure that you set the `SamAccountName` less than 15 characters including the `$` sign.

Use the following command if the root key isn't effective:

```powershell
Add-KdsRootKey -EffectiveTime ((get-date).addhours(-10)) 
```

Ensure that the created gMSA account is a local admin account. If there are any GPO policies on the local admins at the Active Directory level, ensure that they have the gMSA account as the local admin.

>[!Important]
>To minimize the need for extensive communication with both your Active Directory admin and Network Admin, review  [**Self-verification**](scom-managed-instance-self-verification-of-steps.md). The outlines the procedures through which the AD admin and network admin validate their configuration changes and ensure their successful implementation; thus, reducing unnecessary back-and-forth interactions from Operations Manager admin to AD Admin and network admin. This saves time of AD admin, Network admin and System Center Operations Manager admin.

## Next steps

[Store domain credentials in Key vault](store-domain-credentials-in-key-vault.md)

To provide feedback on SCOM Managed Instance (preview), use [this online form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).