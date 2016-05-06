---
title: Sealed Management Pack Files
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ca985c60-b854-41ff-8d40-19891d07d6ef
---
# Sealed Management Pack Files
When a management pack file is sealed, it is converted to a binary file that has an .mp extension. Either the sealed or the unsealed version of a management pack file can be installed to a management group, but both cannot be installed at the same time.

> [!IMPORTANT]
> Sealing a management pack is not a valid strategy for hiding information from users. You can export any sealed management pack from the management group by giving you full access to its XML code. A management pack should never contain sensitive information such as passwords.

## Characteristics of Sealed Management Pack Files
Sealed management pack files have the following characteristics:

### The contents of the management pack file cannot be modified
Sealed management pack files cannot be changed. Changes must be made to the .xml file which is then sealed again with the same certificate. Such an update can only be installed in the same management group if the updated management pack is backward compatible.

### Enforce version control
Only sealed management pack files enforce version control when an updated version of the management pack is installed. If the management pack is unsealed, the new version is always installed regardless of its backward compatibility.

### Enable the management pack to be referenced by other management packs
Management packs can only reference an element in another management pack if the management pack that is referenced is sealed. This requirement ensures that a modification to a management pack cannot break other management packs that reference it. Because sealed management packs maintain version control, any referencing management packs ensures that updates to the sealed management pack are backward compatible.

## When to Seal a Management Pack File
Management pack files do not all have to be sealed. You can install the unsealed version of a management pack file in a management group, and it behaves exactly as the sealed version of the same management pack file. The following criteria list when a management pack file must be sealed:

-   Management pack files that are referenced by other management pack files must be sealed. You might want to create common elements such as groups or modules that are used by other management packs for different applications. The application management packs do not have to be sealed, but the management pack files that contain the shared elements must be.

-   Any management packs that are sent to external customers must be sealed. In addition to ensuring that the customer cannot modify the contents of the management pack, it ensures that any modifications they make are made through overrides in a different management pack file. This lets you provide updates to the management pack without affecting the customer’s modifications.

-   Management pack files that are shared by multiple business units in your organization should be sealed. This ensures that each business unit makes any modifications through overrides in their own management pack files. Each business unit cannot make modifications that affect the other group.

## Sealing a Management Pack File
Management pack files are sealed by using the MPSeal tool that is located in the SupportTools folder of the Operations Manager 2007 R2 distribution media. Sealing requires a client certificate to validate the identity of the author.

You can use the Strong Name tool \(Sn.exe\) included with the Microsoft .NET Framework SDK to create a certificate sufficient for sealing management packs for testing. For production, use a client certificate from the correct certification authority \(CA\) appropriate for signing code for sealing management packs.

For information about the process for sealing a management pack file, see [How to Seal a Management Pack File](./How-to-Seal-a-Management-Pack-File.md).

## See Also
[How to Seal a Management Pack File](./How-to-Seal-a-Management-Pack-File.md)
[Structure of a Management Pack](./Structure-of-a-Management-Pack.md)


