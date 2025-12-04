---
title: Komma igång med taggtillägget Web SDK
description: Skicka händelsedata till Adobe Experience Platform Edge Network med taggtillägget Web SDK.
exl-id: 01ddbb19-40bb-4cb5-bfca-b272b88008b3
source-git-commit: 8dd658c46fc92ae6d450213ab79f2766f4211c53
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 3%

---

# Komma igång med taggtillägget Web SDK

Använd Adobe Experience Platform **tags** (tidigare Launch) för att skicka händelsedata från din webbplats till Edge Network och efterföljande Adobe-lösningar.

Innan du utför följande steg bör du kontrollera att du har åtkomst till följande [egenskapsrättigheter](/help/tags/ui/administration/user-permissions.md):

* [!UICONTROL Develop]
* [!UICONTROL Manage extensions]

Kontrollera dessutom att du har alla [behörigheter](/help/access-control/home.md#permissions) under följande kategorier:

* Datamodellering
* Identiteter

## Skapa ett XDM-schema {#schema}

[Experience Data Model (XDM)](/help/xdm/home.md) är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner för data i form av scheman. Vi rekommenderar att du konfigurerar ett schema när du skickar data till Edge Network.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Schemas]**.
1. Välj **[!UICONTROL Create schema]**.
1. Välj **[!UICONTROL Experience Event]** och sedan **[!UICONTROL Next]**.
1. Ge schemat ett önskat namn och välj sedan **[!UICONTROL Finish]**.
1. (Valfritt) Du kan lägga till fler fält eller [fältgrupper](/help/xdm/ui/resources/field-groups.md) för ytterligare data som du vill samla in.

![Schema Canvas](assets/getting-started/schema-structure.png)

>[!NOTE]\
>När scheman har sparats tillåts endast *additiva* ändringar. Mer information finns i [schemaevolutionen](/help/xdm/schema/composition.md#evolution).

## Skapa ett datastream {#datastream}

En [datastream](/help/datastreams/overview.md) är en konfiguration som anger för Edge Network hur data som du skickar ska hanteras. När du konfigurerar en datastream att skicka data till en viss produkt, skickar datastream automatiskt relevanta data till varje enskild produkt på ett sätt som den specifika produkten förstår.

1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**.
1. Välj **[!UICONTROL New datastream]**.
1. Ge datastream ett önskat namn och välj det nyligen skapade schemat under **[!UICONTROL Mapping schema]**.
1. Välj **[!UICONTROL Save]**.

![Datastreams-lista](assets/getting-started/datastreams.png)

## Skapa en taggegenskap

När du har skapat ett schema och ett datastream kan du skapa och konfigurera en taggegenskap.

1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj **[!UICONTROL New property]**.
1. Ge taggegenskapen önskat namn och domän och välj sedan **[!UICONTROL Save]**.

## Installera taggtillägget

Webbtaggtillägget för SDK installeras på en viss taggegenskap.

1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]** > **[!UICONTROL Extensions]**.
1. Klicka på fliken **[!UICONTROL Catalog]**.  
1. Sök efter tillägget **[!UICONTROL Adobe Experience Platform Web SDK]** med hjälp av sökfunktionen.
1. Markera tilläggskortet och välj sedan **[!UICONTROL Install]** till höger.

![Installera SDK](assets/getting-started/install-sdk.png)

## Konfigurera taggtillägget

När du installerar taggtillägget Web SDK dirigeras du automatiskt till sidan [Konfiguration](configure/config-overview.md) .

1. Under [Datastreams-avsnittet](configure/datastreams.md) väljer du önskat datastream för varje miljö.

Alla andra konfigurationsinställningar är antingen ifyllda åt dig eller valfria. Ange önskade konfigurationsinställningar och välj sedan **[!UICONTROL Save]**.

## Skapa ett variabelt dataelement

Adobe rekommenderar att dataelementen [Variabel](data-element-types.md#variable) används för att lagra nyttolasten som du vill skicka till Adobe. XDM-objekt är också tillgängliga dataelement, men är äldre och mer begränsade i tillämpliga fall.

1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Välj **[!UICONTROL Data elements]** > **[!UICONTROL Create new data element]**.
1. Ge dataelementet följande egenskaper till vänster:
   * **[!UICONTROL Name]**: Alla önskade namn
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Data element type]**: [!UICONTROL Variable]
1. Ange följande egenskaper till höger:
   **Variabeltyp**: XDM
   **[!UICONTROL Sandbox]**: Sandlådan som du skapade ditt schema i
   **[!UICONTROL Schema]**: Det önskade schemat
1. Välj **[!UICONTROL Save]**.

## Skapa en regel

Regler bestämmer när du vill utlösa något eller ange variabler. Om du skapar en regel som körs när biblioteket har lästs in kan du enkelt fylla i variabler som du vill ha ett värde på varje sida.

1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Välj **[!UICONTROL Rules]** > **[!UICONTROL Add rule]**.
1. Ge regeln ett namn.
1. Välj ikonen `+` bredvid **[!UICONTROL Events]**.
1. Ge händelsen följande inställningar:
   * **[!UICONTROL Extension]**: [!UICONTROL Core]
   * **[!UICONTROL Event type]**: [!UICONTROL Library loaded (page top)]
1. Välj **[!UICONTROL Keep changes]**.

Ovanstående steg utgör villkorsdelen av regeln, som aktiveras när biblioteket har lästs in. Följande steg anger vilka åtgärder som ska vidtas när dessa villkor är uppfyllda.

1. Välj ikonen `+` bredvid **[!UICONTROL Actions]**.
1. Ge funktionsmakrot följande inställningar till vänster:
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action type]**: [!UICONTROL Send event]
1. Ange följande fält till höger:
   * **[!UICONTROL XDM]**: XDM-variabeldataelementet
1. Välj **[!UICONTROL Keep changes]**.

![Åtgärdskonfiguration](assets/getting-started/action-config.png)

## Publicera

Taggegenskapen innehåller alla komponenter som behövs för att skicka data till Edge Network.

1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Publishing flow]**.
1. Välj **[!UICONTROL Add library]**.
1. Ge biblioteket ett önskat namn. Tänk på det här namnet som liknar ett implementeringsnamn när du arbetar i programvara för versionskontroll.
1. Ställ in listrutan för miljön på **[!UICONTROL Development]**.
1. Välj **[!UICONTROL Add all changed resources]**.
1. Välj **[!UICONTROL Save & build to Development]**.

Ändringarna är nu distribuerade till din utvecklingsmiljö.

1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Environments]**.
1. Välj installationsikonen bredvid utvecklingsmiljön
1. Installera inbäddningskoden på en testwebbsida på webbplatsen.

När du har verifierat att taggen fungerar i din utvecklingsmiljö kan du använda gränssnittet [!UICONTROL Publishing flow] för att publicera biblioteket till mellanlagring och sedan till produktion.

1. Lägg till tillägget och regeln i ett **bibliotek**, bygg det i en **miljö** och installera inbäddningskoden på din plats.
2. Validera med **Adobe Experience Platform Debugger**.

Nu har du en tunn konfiguration som fångar upp händelser och skickar dem till Edge Network. Du kan nu bygga vidare på implementeringen genom att lägga till fält i ditt schema, lägga till produkter i ett datastream eller lägga till dataelement i taggegenskapen.
