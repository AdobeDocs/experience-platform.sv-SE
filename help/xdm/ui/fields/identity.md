---
keywords: Experience Platform;hem;populära ämnen;api;API;XDM;XDM system;experience data model;data model;ui;workspace;identity;field;
solution: Experience Platform
title: Definiera identitetsfält i användargränssnittet
description: Lär dig hur du definierar ett identitetsfält i användargränssnittet i Experience Platform.
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: f9917d6a6de81f98b472cff9b41f1526ea51cdae
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---

# Definiera identitetsfält i användargränssnittet

I Experience Data Model (XDM) representerar ett identitetsfält ett fält som kan användas för att identifiera en enskild person som relaterar till en post- eller tidsseriehändelse. I det här dokumentet beskrivs hur du definierar ett identitetsfält i Adobe Experience Platform-gränssnittet.

## Förutsättningar

Identitetsfält är en viktig komponent i hur kundidentitetsdiagram skapas i Platform, som i slutändan påverkar hur kundprofilen i realtid sammanfogar olika datablad för att få en fullständig bild av kunden. Innan du definierar identitetsfält i dina scheman ska du läsa följande dokumentation för att lära dig mer om de viktigaste tjänsterna och begreppen som rör identitetsfält:

* [Adobe Experience Platform Identity Service](../../../identity-service/home.md): Överbryggar identiteter mellan enheter och system, länkar samman datauppsättningar baserat på de identitetsfält som definieras av XDM-scheman som de följer.
   * [Identitetsnamnutrymmen](../../../identity-service/features/namespaces.md): Identitetsnamnutrymmen definierar de olika typerna av identitetsinformation som kan relateras till en enskild person, och är en obligatorisk komponent för varje identitetsfält.
* [Kundprofil i realtid](../../../profile/home.md): Använder kundidentitetsdiagram för att skapa en enhetlig konsumentprofil som bygger på aggregerade data från flera källor, som uppdateras i nära realtid.

## Definiera ett identitetsfält {#define-a-identity-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_identityField_primaryIdentityRestriction"
>title="Begränsningar för primär identitet"
>abstract="Det här schemat använder en fältgrupp som är avsedd att användas i en specifik källanslutning. Anslutningen kräver identityMap som primär identitet och har ställt in den automatiskt."

När [definiera ett nytt fält](./overview.md#define) i användargränssnittet kan du ange det som ett identitetsfält genom att välja **[!UICONTROL Identity]** i den högra listen.

![](../../images/ui/fields/special/identity.png)

Ytterligare kontroller visas när du har markerat kryssrutan. Om du vill att det här fältet ska vara schemats primära identitet väljer du **[!UICONTROL Primary identity]** kryssrutan.

>[!NOTE]
>
>Ett enskilt schema kan ha många definierade identitetsfält, men kan bara ha en primär identitet. Alla identitetsfält (primära eller på annat sätt) bidrar till identitetsdiagrammet för en enskild kund, men i realtidskundprofilen används endast den primära identiteten som källa för sanningen när du sammanfogar datafragment. Om du vill aktivera ett schema för användning i profilen måste schemat ha en primär identitet definierad.

Under **[!UICONTROL Identity namespace]** använder du listrutan för att välja lämpligt namnutrymme för identitetsfältet. Standardnamnutrymmen som tillhandahålls av Adobe visas tillsammans med anpassade namnutrymmen som definieras av din organisation.

När du är klar väljer du **[!UICONTROL Apply]** för att tillämpa ändringen på schemat.

![](../../images/ui/fields/special/identity-config.png)

Arbetsytan uppdateras med ändringarna och det valda fältet får en fingeravtryckssymbol (![](../../images/ui/fields/special/identity-symbol.png)) för att ange den som en identitet. I den vänstra listen visas nu identitetsfältet under namnet på den klass eller schemafältgrupp som tillhandahåller fältet till schemat.

Om fältet också har angetts som primär identitet listas det också under **[!UICONTROL Required fields]** till vänster. Om identitetsfältet är kapslat i schemastrukturen kommer alla överordnade fält också att listas efter behov.

![](../../images/ui/fields/special/identity-applied.png)

Om du har definierat en primär identitet för schemat kan du nu fortsätta till [aktivera schemat för användning i kundprofilen i realtid](../resources/schemas.md#profile).

## Nästa steg

I den här handboken beskrivs hur du definierar ett identitetsfält i användargränssnittet. När data importeras med det här schemat uppdateras dina kundidentitetsdiagram så att de återspeglar schemats identitetsfält. Se guiden på [visningsprogram för identitetsdiagram](../../../identity-service/features/identity-graph-viewer.md) om du vill lära dig hur du utforskar organisationens privata diagram i användargränssnittet.

Se översikten på [definiera fält i användargränssnittet](./overview.md#special) för att lära dig hur du definierar andra XDM-fälttyper i [!DNL Schema Editor].
