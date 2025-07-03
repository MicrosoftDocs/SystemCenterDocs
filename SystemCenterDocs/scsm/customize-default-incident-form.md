---
title: Customize the default incident form for the sample scenario
description: This sample scenario article describes how to apply simple customizations to a default form in the Service Manager Authoring Tool.
ms.custom: UpdateFrequency2, engagement-fy24
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 2af8b9d4-f736-4f96-b058-a96b10a64aca
---

# Customize the default incident form for the Service Manager Authoring Tool sample scenario



This sample scenario describes how to apply simple customizations to a default form in the Service Manager Authoring Tool. In this scenario, you customize the Incident form, which is the default form for interacting with incidents. You customize the form in the Authoring Tool and then save the customized form in a new management pack. Then, in the Service Manager console, you import this new management pack. Afterwards, whenever you create or view an incident, Service Manager displays the customized form. The Incident form, System.WorkItem.Incident.ConsoleForm, is defined in the Service Manager Incident Management Library management pack.

The sample scenario for customizing the default Incident form consists of three steps.

## Step 1: View the default incident form

Before you customize the form, view the default form in the Service Manager console and identify elements on the form that you want to customize. For example, you can plan to rearrange various text boxes on the form.

To view the default incident form, follow these steps:

1. In the Service Manager console, select **Work Items**.

2. In the **Work Items** pane, select **Incident Management**.

3. In the **Tasks** pane, select **Create Incident**.

4. Review the **Incident** form. This form is the form that you use to create and view incidents. You can identify elements in the form that you might want to customize.

## Step 2: Customize the default incident form

Use the following procedure to customize the default Incident form in the Authoring Tool.

To customize the Incident form, follow these steps:

1. Select **Start**, point to **Programs**, point to **Microsoft System Center**, point to **Service Manager \<version\> Authoring**, and select **Service Manager Authoring Tool**.

2. In the Authoring Tool, select **File**, and select **New**.

3. In the **New Management Pack** dialog, in the **File name** box, enter **MyIncidentFormCustomizations**, and select **Save**.

    > [!NOTE]
    > The **MyIncidentFormCustomizations** management pack is now listed in the **Management Pack Explorer**.

4. In the **Form Browser** pane, locate and then right\-click the **System.WorkfItem.Incident.ConsoleForm** form, which is the default Incident form, and select **View**.

    > [!NOTE]
    > The **Service Manager Incident Management Library** management pack, which contains the default Incident form, is now listed in the **Management Pack Explorer**.

5. In the authoring pane, select **Customize**.

6. In the **Target Management Pack** dialog, select **MyIncidentFormCustomizations**, and select **OK**.

7. Wait for the authoring pane to display the form that you're customizing. You can now add controls, such as a **Label**, a **Text Box**, or an **Image**, to the form. Ensure that the **Details** window is open and visible, so that you can browse and modify properties of the controls.

8. In the **Management Pack Explorer**, right\-click **MyIncidentFormCustomizations**, and select **Save**.

9. Exit the Authoring Tool.

## Step 3: Use the customized default incident form

Use the following procedure to view and use the customized Incident form in the Service Manager console.

To use the customized System.WorkItem.Incident.ConsoleForm form, follow these steps:

1. Start the Service Manager console, and select **Administration**.

2. In the **Administration** pane, select **Management Packs**.

3. In the **Tasks** pane, select **Import**.

4. In the **Select Management Packs to Import** dialog, select the **MyIncidentFormCustomizations.xml** management pack file. Select **Open**.

5. In the **Import Management Packs** dialog, select **Import**, wait for the management pack to be imported, and select **OK**.

6. Select **Incidents**, and then in the **Tasks** pane, select **Create Incident**.

    > [!NOTE]
    > The **Incident** form that is displayed is your customized form.

7. Fill in the form, and then save the incident.

## Next steps

- For information that can help you customize and create forms in the Service Manager Authoring Tool, review [Form control properties in the Authoring Tool](form-control-properties.md).
