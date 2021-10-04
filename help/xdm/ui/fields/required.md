---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;data model;ui;workspace;required;field;
title: Definiera obligatoriska fält i användargränssnittet
description: Lär dig hur du definierar ett obligatoriskt XDM-fält i användargränssnittet för Experience Platform.
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: 1d04bf56c51506f84c5156e6d2ed6c9f58f15235
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Definiera obligatoriska fält i användargränssnittet

I Experience Data Model (XDM) anger ett obligatoriskt fält att det måste anges som ett giltigt värde för att en viss post- eller tidsseriehändelse ska kunna accepteras under datainmatning. Vanliga användningsexempel för obligatoriska fält är användaridentitetsinformation och tidsstämplar.

När [du definierar ett nytt fält](./overview.md#define) i Adobe Experience Platform användargränssnitt kan du ange det som ett obligatoriskt fält genom att markera kryssrutan **[!UICONTROL Required]** i den högra listen. Välj **[!UICONTROL Apply]** om du vill använda ändringen i schemat.

![Kryssrutan Obligatoriskt](../../images/ui/fields/required/root.png)

Om fältet är ett rotnivåattribut under klientorganisations-ID-objektet visas sökvägen omedelbart under **[!UICONTROL Required fields]** i den vänstra listen.

![Obligatoriskt fält på rotnivå](../../images/ui/fields/required/applied.png)

Om ett obligatoriskt fält är kapslat i ett objekt som inte är markerat som obligatoriskt, visas emellertid inte det kapslade fältet under **[!UICONTROL Required fields]** i den vänstra listen.

I exemplet nedan anges fältet `loyaltyId` som obligatoriskt, men det överordnade objektet `loyalty` är det inte. I det här fallet skulle inga valideringsfel uppstå om `loyalty` uteslöts vid inmatning av data, även om det underordnade fältet `loyaltyId` markerats som nödvändigt. Det innebär att även om `loyalty` är valfritt måste det innehålla ett `loyaltyId`-fält i den händelse det inkluderas.

![Kapslat obligatoriskt fält](../../images/ui/fields/required/nested.png)

Om du vill att ett kapslat fält alltid ska vara obligatoriskt i ett schema, måste du även ange alla överordnade fält som obligatoriska (med undantag för klient-ID-objektet).

![Överordnade och underordnade obligatoriska fält](../../images/ui/fields/required/parent-and-child.png)

## Nästa steg

I den här handboken beskrivs hur du definierar ett obligatoriskt fält i användargränssnittet. I översikten [definierar fält i användargränssnittet](./overview.md#special) finns mer information om hur du definierar andra XDM-fälttyper i [!DNL Schema Editor].
