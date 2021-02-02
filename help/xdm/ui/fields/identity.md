---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;data model;ui;workspace;identity;field;
solution: Experience Platform
title: Definiera ett identitetsfält i användargränssnittet
description: Lär dig hur du definierar ett identitetsfält i användargränssnittet i Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: f5f507c2e962e2ff9f81376bfe363a6f438056cd
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---


# Definiera ett identitetsfält i användargränssnittet

I Experience Data Model (XDM) representerar ett identitetsfält ett fält som kan användas för att identifiera en enskild person som relaterar till en post- eller tidsseriehändelse. I det här dokumentet beskrivs hur du definierar ett identitetsfält i Adobe Experience Platform-gränssnittet.

## Förutsättningar

Identitetsfält är en viktig komponent i hur kundidentitetsdiagram skapas i Platform, som i slutändan påverkar hur kundprofilen i realtid sammanfogar olika datablad för att få en fullständig bild av kunden. Innan du definierar identitetsfält i dina scheman ska du läsa följande dokumentation för att lära dig mer om de viktigaste tjänsterna och begreppen som rör identitetsfält:

* [Adobe Experience Platform Identity Service](../../../identity-service/home.md): Överbryggar identiteter mellan enheter och system och länkar samman datauppsättningar baserat på de identitetsfält som definieras av XDM-scheman som de följer.
   * [Identitetsnamnutrymmen](../../../identity-service/namespaces.md): Identitetsnamnutrymmen definierar de olika typerna av identitetsinformation som kan relateras till en person, och är en obligatorisk komponent för varje identitetsfält.
* [Kundprofil](../../../profile/home.md) i realtid: Använder kundidentitetsdiagram för att skapa en enhetlig konsumentprofil som bygger på aggregerade data från flera källor, som uppdateras i nära realtid.

## Definiera ett identitetsfält

När [du definierar ett nytt fält](./overview.md#define) i användargränssnittet kan du ange det som ett identitetsfält genom att markera kryssrutan **[!UICONTROL Identity]** i den högra listen.

![](../../images/ui/fields/special/identity.png)

Ytterligare kontroller visas när du har markerat kryssrutan. Om du vill att det här fältet ska vara den primära identiteten för schemat markerar du kryssrutan **[!UICONTROL Primary identity]**.

>[!NOTE]
>
>Ett enskilt schema kan ha många definierade identitetsfält, men kan bara ha en primär identitet. Alla identitetsfält (primära eller på annat sätt) bidrar till identitetsdiagrammet för en enskild kund, men kundprofilen i realtid använder bara den primära identiteten som källa för sanningen när du sammanfogar datafragment. Om du vill aktivera ett schema för användning i profilen måste schemat ha en primär identitet definierad.

Under **[!UICONTROL Identity namespace]** använder du listrutemenyn för att välja lämpligt namnutrymme för identitetsfältet. Standardnamnutrymmen som tillhandahålls av Adobe visas tillsammans med anpassade namnutrymmen som definieras av din organisation.

När du är klar väljer du **[!UICONTROL Apply]** för att tillämpa ändringen på schemat.

![](../../images/ui/fields/special/identity-config.png)

Arbetsytan uppdateras för att återspegla ändringarna, och det valda fältet får en fingeravtryckssymbol (![](../../images/ui/fields/special/identity-symbol.png)) för att ange den som en identitet. I den vänstra listen visas nu identitetsfältet under namnet på den klass eller blandning som innehåller fältet till schemat.

Eftersom alla identitetsfält är obligatoriska som standard visas fältet nu under **[!UICONTROL Required fields]** i den vänstra listen. Om identitetsfältet är kapslat i schemastrukturen kommer alla överordnade fält också att listas efter behov.

![](../../images/ui/fields/special/identity-applied.png)

Om du har definierat en primär identitet för schemat kan du nu gå vidare till [aktivera schemat för användning i kundprofilen ](../resources/schemas.md#profile) i realtid.

## Nästa steg

I den här handboken beskrivs hur du definierar ett identitetsfält i användargränssnittet. När data importeras med det här schemat uppdateras dina kundidentitetsdiagram så att de återspeglar schemats identitetsfält. Se guiden för [identitetsdiagramvisningsprogrammet](../../../identity-service/ui/identity-graph-viewer.md) för att lära dig hur du utforskar organisationens privata diagram i användargränssnittet.

I översikten [definierar fält i användargränssnittet](./overview.md#special) finns mer information om hur du definierar andra XDM-fälttyper i [!DNL Schema Editor].