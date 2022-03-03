---
title: Quote Request Details Schema Field Group
description: This document provides an overview of the Quote Request Details schema field group.
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---

# [!UICONTROL Quote Request Details]

[!UICONTROL Quote Request Details][[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) `quotes`

![](../../images/field-groups/quote-request-details.png)

| Property | Data type | Beskrivning |
| --- | --- | --- |
| `discount` | [[!UICONTROL Currency]](../../data-types/currency.md) | The discount amount for a quote displayed to a visitor. |
| `premium` | [[!UICONTROL Currency]](../../data-types/currency.md) | The premium amount for a quote displayed to a visitor. |
| `location` | [!UICONTROL String] | The postal code used for finding retailers near the visitor&#39;s location. |
| `requestID` | [!UICONTROL String] | A unique identifier for the quote request. |
| `selectedRetailer` | [!UICONTROL String] | The selected retailer for the quote request, if applicable. |

{style=&quot;table-layout:auto&quot;}

[](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json)
