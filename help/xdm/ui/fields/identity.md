---
keywords: Experience Platform;home;populära topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;identity;field;
solution: Experience Platform
title: Definiera identitetsfält i användargränssnittet
description: Lär dig hur du definierar ett identitetsfält i Experience Platform användargränssnitt.
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---

# Definiera identitetsfält i användargränssnittet

I Experience Data Model (XDM) representerar ett identitetsfält ett fält som kan användas för att identifiera en enskild person som relaterar till en post- eller tidsseriehändelse. I det här dokumentet beskrivs hur du definierar ett identitetsfält i Adobe Experience Platform-gränssnittet.

## Förhandskrav

Identitetsfält är en viktig komponent i hur kundidentitetsdiagram skapas i Experience Platform, vilket i slutänden påverkar hur kundprofilen i realtid sammanfogar olika datafragment för att få en fullständig bild av kunden. Innan du definierar identitetsfält i dina scheman ska du läsa följande dokumentation för att lära dig mer om de viktigaste tjänsterna och begreppen som rör identitetsfält:

* [Adobe Experience Platform Identity Service](../../../identity-service/home.md): Förena identiteter mellan enheter och system genom att länka samman datauppsättningar baserat på de identitetsfält som definieras av XDM-scheman som de följer.
   * [Identitetsnamnutrymmen](../../../identity-service/features/namespaces.md): Identitetsnamnutrymmen definierar de olika typerna av identitetsinformation som kan relatera till en enskild person och är en obligatorisk komponent för varje identitetsfält.
* [Kundprofil i realtid](../../../profile/home.md): Använder kundidentitetsdiagram för att tillhandahålla en enhetlig konsumentprofil baserat på aggregerade data från flera källor, som uppdateras i nära realtid.

## Definiera ett identitetsfält {#define-a-identity-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_identityField_primaryIdentityRestriction"
>title="Begränsningar för primär identitet"
>abstract="Det här schemat använder en fältgrupp som är avsedd att användas i en specifik källanslutning. Anslutningen kräver identityMap som primär identitet och har ställt in den automatiskt."

När du [definierar ett nytt fält](./overview.md#define) i användargränssnittet kan du ange det som ett identitetsfält genom att markera kryssrutan **[!UICONTROL Identity]** i den högra listen.

![](../../images/ui/fields/special/identity.png)

Ytterligare kontroller visas när du har markerat kryssrutan. Om du vill att det här fältet ska vara den primära identiteten för schemat markerar du kryssrutan **[!UICONTROL Primary identity]**.

>[!NOTE]
>
>Ett enskilt schema kan ha många definierade identitetsfält, men kan bara ha en primär identitet. Alla identitetsfält (primära eller på annat sätt) bidrar till identitetsdiagrammet för en enskild kund, men i realtidskundprofilen används endast den primära identiteten som källa för sanningen när du sammanfogar datafragment. Om du vill aktivera ett schema för användning i profilen måste schemat ha en primär identitet definierad.

Under **[!UICONTROL Identity namespace]** använder du listrutemenyn för att välja lämpligt namnutrymme för identitetsfältet. Standardnamnutrymmen som tillhandahålls av Adobe visas tillsammans med anpassade namnutrymmen som definieras av din organisation.

När du är klar väljer du **[!UICONTROL Apply]** för att tillämpa ändringen på schemat.

>[!IMPORTANT]
>
>Om ett primärt identitetsfält redan är inställt kan du ändra det primära identitetsfältet i ditt schema genom att följa stegen ovan. Du måste dock inaktivera och sedan återaktivera alla associerade datauppsättningar i profilen för att ändringen ska börja gälla.

![](../../images/ui/fields/special/identity-config.png)

Arbetsytan uppdateras för att återspegla ändringarna och det valda fältet får en fingeravtryckssymbol (![](/help/images/icons/identity-service.png)) som anger att det är en identitet. I den vänstra listen visas nu identitetsfältet under namnet på den klass eller schemafältgrupp som tillhandahåller fältet till schemat.

Om fältet också har angetts som primär identitet visas det också under **[!UICONTROL Required fields]** i den vänstra listen. Om identitetsfältet är kapslat i schemastrukturen kommer alla överordnade fält också att listas efter behov.

![](../../images/ui/fields/special/identity-applied.png)

Om du har definierat en primär identitet för schemat kan du nu [aktivera schemat för användning i kundprofilen i realtid](../resources/schemas.md#profile).

## Nästa steg

I den här handboken beskrivs hur du definierar ett identitetsfält i användargränssnittet. När data importeras med det här schemat uppdateras dina kundidentitetsdiagram så att de återspeglar schemats identitetsfält. Se guiden för [identitetsdiagramvisningsprogrammet](../../../identity-service/features/identity-graph-viewer.md) om du vill veta mer om hur du utforskar organisationens privata diagram i användargränssnittet.

Mer information om hur du definierar andra XDM-fälttyper i [!DNL Schema Editor] finns i översikten [Definiera fält i användargränssnittet](./overview.md#special).

