---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;data model;ui;workspace;required;field;
solution: Experience Platform
title: Definiera ett obligatoriskt fält i användargränssnittet
description: Lär dig hur du definierar ett obligatoriskt XDM-fält i användargränssnittet för Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: 48025fc11558bf6773ce5c48054483758c7e993f
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 1%

---


# Definiera ett obligatoriskt fält i användargränssnittet

I Experience Data Model (XDM) anger ett obligatoriskt fält att det måste anges som ett giltigt värde för att en viss post- eller tidsseriehändelse ska kunna accepteras under datainmatning. Vanliga användningsexempel för obligatoriska fält är användaridentitetsinformation och tidsstämplar.

När [du definierar ett nytt fält](./overview.md#define) i Adobe Experience Platform användargränssnitt kan du ange det som ett obligatoriskt fält genom att markera kryssrutan **[!UICONTROL Required]** i den högra listen. Välj **[!UICONTROL Apply]** om du vill använda ändringen i schemat.

![](../../images/ui/fields/special/required.png)

När fältet används visas sökvägen under **[!UICONTROL Required fields]** i den vänstra listen. Om fältet är kapslat visas även eventuella överordnade fält som obligatoriska.

![](../../images/ui/fields/special/required-applied.png)

## Nästa steg

I den här handboken beskrivs hur du definierar ett obligatoriskt fält i användargränssnittet. I översikten [definierar fält i användargränssnittet](./overview.md#special) finns mer information om hur du definierar andra XDM-fälttyper i [!DNL Schema Editor].