---
title: How to Seal a Management Pack File_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce160976-e945-4d37-bb75-5bb0c5624426
---
# How to Seal a Management Pack File_1
Management packs are sealed by using the MPSeal tool that is located in the SupportTools folder of the Operations Manager 2007 R2 distribution media. This is a command\-line tool that creates a sealed .mp file from an unsealed .xml file. After performing the sealing process, you can install the sealed management pack in your management group.

> [!NOTE]
> If you created the management pack in the Operations console, you must export it to an .xml file before performing the sealing process. You must then uninstall the management pack before installing the sealed version.

## <a name="MPSeal"></a>MPSeal Syntax
MPSeal.exe uses the following syntax:

**MPseal.exe***Management Pack File Name* \[**\/I***Include Path*\]\* **\/Keyfile***Key File Path***\/Company***Company Name* \[**\/Outdir***Output Directory*\] \[**\/DelaySign**\] \[**\/Copyright***Copyright text*\]

Each of the command\-line options are described in the following table.

|Option|Description|
|----------|---------------|
|Management Pack File Name|The full name of the .xml file to seal. If the file is not in the current directory, you must include the full path to the file. If the path includes a space, you must enclose it in quotes.|
|Include Path|The path to a directory containing .mp files that are referenced by the management pack that you are sealing. For more information, see [Management Pack References](./How-to-Seal-a-Management-Pack-File.md#MPReferences).|
|Key File Path|The file containing the private and public key. For more information, see [Key File](./How-to-Seal-a-Management-Pack-File.md#KeyFile).|
|Company Name|The name of your company. If it includes a space, you must enclose it in quotes.|
|Output Directory|The directory to store the output file. If not specified, the current directory is used.|
|DelaySign|If this option is used, only the public key is used. For more information, see [Delayed Signing](./How-to-Seal-a-Management-Pack-File.md#DelayedSigning).|
|Copyright text|Text to include for copyright information. While this option is functional, the text is not currently accessible from Operations Manager.|

## Example
The following example seals a management pack file named Contoso.MyApp.xml. It creates a file called Contoso.MyApp.mp in the current directory.

```
mpseal Contoso.MyApp.xml /I c:\mp /Keyfile contoso.snk /Company "Contoso"
```

## <a name="MPReferences"></a>Management Pack References
In addition to sealing the management pack, MPSeal verifies the management pack file and reports any errors that prevents it from installing. All of these errors must be corrected before the sealing finishes successfully. The MPVerify tool performs the same verification . To perform this function, MPSeal requires access to any management packs referenced by the management pack that is in the process of being sealed. These must be the sealed versions of the files with an .mp extension and must be at least the version specified by the management pack that is being sealed.

You specify a directory to search .mp files with the **\/I** command\-line option. You can use multiple **\/I** options if the required files are in multiple directories. You can obtain the standard library management pack files included with Operations Manager 2007 R2 from the installation directory on the management server. You must obtain other management pack files separately. If you import a management pack directly into your management group from the management pack catalog, you have to download it separately to obtain the .mp file.

> [!NOTE]
> If you are unsure of the management packs referenced by the management pack that you are sealing, you can run MPSeal by using any directory. A list of the required management packs are returned.

For more information about management pack references, see the [Management Pack References &#91;OM2007\_AuthConsole&#93;](assetId:///2a17c71d-8cab-45a1-9b01-63e8ec4dbd4c) section of this guide.

## <a name="KeyFile"></a>Key File
Sealing requires a key file that contains a private and public key. The key pair validates the identity of the signing party and ensures that a malicious user cannot provide a sealed management pack by impersonating someone else. This is the same key pair used for signing .NET assemblies and can be created with the Strong Name tool \(sn.exe\) included with the [Microsoft Windows SDK](http://go.microsoft.com/fwlink/?LinkID=231265).

> [!IMPORTANT]
> You should protect any key file that is used to seal a management pack. If someone else were to obtain this key file, they could seal a management pack by impersonating the original author.

For information about the complete use of the Strong Name tool, see [Sn.exe \(String Name Tool\)](http://go.microsoft.com/fwlink/?LinkID=231266). The following example is sufficient for most management packs and creates a key file called contoso.snk in the local directory.

```
sn –k contoso.snk
```

## <a name="DelayedSigning"></a>Delayed Signing
For added security of their private key, organizations often implement a delayed process for signing assemblies. This allows access to the private key to only a few individuals. Using this process, you sign the assembly with only the public key, and then complete the signing with the private key just before a release.

If your organization has an existing process for performing delayed signing of assemblies, you should use this process to seal your management pack for production. You can perform the initial partial sealing of the management pack by using the **\/DelaySign** option.

For more information about delayed signing of assemblies, see [Delay Signing an Assembly](http://go.microsoft.com/fwlink/?LinkID=231267).

## <a name="OperationsConsole"></a>Management Pack Files Created in the Operations Console
Management pack files created in the Operations console are unsealed. You can use the following procedures if you have to seal a management pack that you created in the Operations console.

#### To seal a management pack file that was created in the Operations console

1.  Export the management pack file to an .xml file. For more information, see [How to Export an Operations Manager Management Pack](./How-to-Export-an-Operations-Manager-Management-Pack.md).

2.  Seal the XML code. For more information, see [MPSeal Syntax](./How-to-Seal-a-Management-Pack-File.md#MPSeal).

3.  Delete the management pack file from the management group. For more information, see [How to Remove an Operations Manager Management Pack](./How-to-Remove-an-Operations-Manager-Management-Pack.md).

4.  Import the .mp file created by MPSeal. For more information, see [How to Import an Operations Manager Management Pack](./How-to-Import-an-Operations-Manager-Management-Pack.md).

## See Also
[Sealed Management Pack Files](./Sealed-Management-Pack-Files.md)


