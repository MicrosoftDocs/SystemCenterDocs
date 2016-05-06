---
title: How to Modify the Self-Service Portal Attachment File Size
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddb44f0f-25a7-442d-a184-a509d69c118f
---
# How to Modify the Self-Service Portal Attachment File Size
By default, users can attach files in requests that they submit when they use the [!INCLUDE[smssp](./Token/smssp_md.md)] in [!INCLUDE[smlong12](./Token/smlong12_md.md)]. However, the [!INCLUDE[smssp](./Token/smssp_md.md)] limits the attachment file size to 10 megabytes \(MB\). You can modify the [!INCLUDE[smssp](./Token/smssp_md.md)] default attachment file size by editing a property manually in the Web.config file.

> [!NOTE]
> The maximum file size that the [!INCLUDE[smssp](./Token/smssp_md.md)] supports is independent of the work item maximum size settings that are specified in the [!INCLUDE[smcons](./Token/smcons_md.md)] in the Administration workspace.

### To modify the [!INCLUDE[smssp](./Token/smssp_md.md)] attachment file size

1.  Log in to the computer that hosts the Web Content Server with administrative credentials.

2.  Using a text editor of your choice \(for example, Notepad\), open the Web.config file in the %inetroot%\\inetpub\\wwwroot\\System Center Service Manager Portal\\servicehost folder.

3.  Locate the <binaryMessageEncoding> section, as shown in the following example:

    ```
    <binaryMessageEncoding>
           <readerQuotas maxArrayLength="10485760"/> 
          </binaryMessageEncoding>
    ```

4.  Modify the line `<readerQuotas maxArrayLength="10485760"/>` by replacing the `maxArrayLength` value with a value of your choice.

5.  Close the text editor, and save the changes.

## See Also
[Managing the System Center 2012 - Service Manager Self-Service Portal](./Managing-the-System-Center-2012---Service-Manager-Self-Service-Portal.md)


