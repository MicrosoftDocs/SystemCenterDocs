---
ms.assetid: 
title: Create a static IP
description: This article describes how to create a static IP for load balancer in a dedicated subnet of SCOM Managed Instance.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 08/25/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Create a static IP

This article describes how to create a static IP for load balancer in a dedicated subnet of SCOM Managed Instance. Additionally, insert an entry into the DNS server, ensure that DNS name resolves to DNS name (DNSHostName) of the gMSA; Get DNSHostName of gMSA account from [step6](create-gmsa-account.md).

>[!Note]
> To know about the SCOM Managed Instance (preview) Architecture, see [Azure Monitor SCOM Managed Instance (preview)](operations-manager-managed-instance-overview.md).

## Create a static IP and configure the DNS name

For all the System Center Operations Manager components to communicate with the load balancer that the SCOM Managed Instance (preview) service creates, you need a static IP and DNS name for the load balancer's front-end configuration.

Ensure that the static IP is in the subnet that you created for SCOM Managed Instance. Create a DNS name (according to your organization's policy) for the static IP and the DNS name must resolves to gMSA account DNS Host name. For DNS Host name of gMSA account, run the following command:

     ```powershell
     Get-ADServiceAccount -Identity <gMSA Account Name> -Properties DNSHostName,Enabled,PrincipalsAllowedToRetrieveManagedPassword,SamAccountName,ServicePrincipalNames -Credential <DomainUserCredentials> 
     ```    

Relpace the gMSA account name and domain credentials with the right values in the above command.

:::image type="DNS manager" source="media/create-static-ip/dns-manager.png" alt-text="Screenshot of host information in DNS Manager.":::

>[!Important]
>To minimize the need for extensive communication with both your Active Directory admin and Network Admin, review  [**Self-verification**](/system-center/scom/scom-mi-self-verification-of-steps?view=sc-om-2022). The outlines the procedures through which the AD admin and network admin validate their configuration changes and ensure their successful implementation; thus, reducing unnecessary back-and-forth interactions from Operations Manager admin to AD Admin and network admin. This saves time of AD admin, Network admin and System Center Operations Manager admin.

## Next steps

- [Configure the network firewall](configure-network-firewall.md)

To provide feedback on SCOM Managed Instance (preview), use [this online form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
