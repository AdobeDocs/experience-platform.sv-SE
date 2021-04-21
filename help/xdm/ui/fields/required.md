---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;data model;ui;workspace;required;field;
solution: Experience Platform
title: Definiera obligatoriska fält i användargränssnittet
description: Lär dig hur du definierar ett obligatoriskt XDM-fält i användargränssnittet för Experience Platform.
topic-legacy: user guide
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---

# Definiera obligatoriska fält i användargränssnittet

I Experience Data Model (XDM) anger ett obligatoriskt fält att det måste anges som ett giltigt värde för att en viss post- eller tidsseriehändelse ska kunna accepteras under datainmatning. Vanliga användningsexempel för obligatoriska fält är användaridentitetsinformation och tidsstämplar.

När [du definierar ett nytt fält](./overview.md#define) i Adobe Experience Platform användargränssnitt kan du ange det som ett obligatoriskt fält genom att markera kryssrutan **[!UICONTROL Required]** i den högra listen. Välj **[!UICONTROL Apply]** om du vill använda ändringen i schemat.

![](../../images/ui/fields/special/required.png)

När fältet används visas sökvägen under **[!UICONTROL Required fields]** i den vänstra listen. Om fältet är kapslat visas även eventuella överordnade fält som obligatoriska.

![](../../images/ui/fields/special/required-applied.png)

## Nästa steg

I den här handboken beskrivs hur du definierar ett obligatoriskt fält i användargränssnittet. I översikten [definierar fält i användargränssnittet](./overview.md#special) finns mer information om hur du definierar andra XDM-fälttyper i [!DNL Schema Editor].
