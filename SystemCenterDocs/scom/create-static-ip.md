---
ms.assetid: 
title: Create a static IP for Azure Monitor SCOM Managed Instance
description: This article describes how to create a static IP for load balancer in a dedicated subnet of SCOM Managed Instance.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 11/01/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Create a static IP for Azure Monitor SCOM Managed Instance

This article describes how to create a static IP for a load balancer in a dedicated subnet of Azure Monitor SCOM Managed Instance. Additionally, insert an entry into the Domain Name System (DNS) server, and ensure that the DNS name resolves to the DNS name (`DNSHostName`) of the group managed service account (gMSA). Get the DNS host name of the gMSA account from [step 6](create-gmsa-account.md).

>[!NOTE]
> To learn about the SCOM Managed Instance architecture, see [Azure Monitor SCOM Managed Instance](operations-manager-managed-instance-overview.md).

## Create a static IP and configure the DNS name

For all the System Center Operations Manager components to communicate with the load balancer that the SCOM Managed Instance service creates, you need a static IP and DNS name for the load balancer's front-end configuration.

Ensure that the static IP is in the subnet that you created for SCOM Managed Instance. Create a DNS name (according to your organization's policy) for the static IP. The DNS name must resolve to the gMSA account DNS Host name. For the DNS Host name of the gMSA account, run the following command:

```powershell
Get-ADServiceAccount -Identity <gMSA Account Name> -Properties DNSHostName,Enabled,PrincipalsAllowedToRetrieveManagedPassword,SamAccountName,ServicePrincipalNames -Credential <DomainUserCredentials> 
```

Replace the gMSA account name and domain credentials with the right values in the preceding command.

Create the forward lookup entry in DNS by creating an association between the IP and the DNS name.

- If you use the DNS infrastructure of an Active Directory domain, open the DNS manager, connect to the DNS server, and create an association between the IP and the DNS name (forward lookup).
- If you use a different DNS software, create the forward lookup entry in the DNS server to create an association between the IP and the DNS name (forward lookup).

:::image type="DNS manager" source="media/create-static-ip/dns-manager.png" alt-text="Screenshot that shows host information in DNS Manager.":::

> [!IMPORTANT]
> To minimize the need for extensive communication with both your Active Directory admin and the network admin, see [Self-verification](scom-managed-instance-self-verification-of-steps.md). The article outlines the procedures that the Active Directory admin and the network admin use to validate their configuration changes and ensure their successful implementation. This process reduces unnecessary back-and-forth interactions from the Operations Manager admin to the Active Directory admin and the network admin. This configuration saves time for the admins.

## Next steps

- [Configure the network firewall](configure-network-firewall.md)

To provide feedback on SCOM Managed Instance, use [this online form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).