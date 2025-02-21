---
title: Aktivera potentiella målgrupper till destinationer
type: Tutorial
description: Lär dig hur du aktiverar potentiella målgrupper till destinationer
exl-id: 3e034a14-09d0-4b08-b171-5afb62ae4b62
source-git-commit: e7c0551276d31d6809ace096c00e0dc2665090e6
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# Aktivera potentiella målgrupper

>[!AVAILABILITY]
>
>Den här funktionaliteten är tillgänglig för kunder som har köpt Real-Time CDP Prime- och Ultimate-paketet. Kontakta Adobe om du vill ha mer information.

I den här artikeln förklaras det arbetsflöde som krävs för att exportera [potentiella målgrupper](/help/segmentation/types/prospect-audiences.md) från Adobe Experience Platform till det önskade målet.

## Mål som stöds {#supported-destinations}

Gå till **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** och välj fliken **[!UICONTROL Catalog]**. Använd filtret **[!UICONTROL Data types]** och välj **[!UICONTROL Prospects]** för att se vilka mål som stöder aktivering av potentiella målgrupper. För närvarande är export av potentiella målgrupper bara tillgängligt för molnlagringsdestinationer.

![Destinationer som stöder potentiella målgrupper.](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

## Förhandskrav {#prerequisites}

* Du måste först importera [profiler för potentiella kunder](/help/profile/ui/prospect-profile.md) och skapa [målgrupper för potentiella kunder](/help/segmentation/types/prospect-audiences.md) innan du kan aktivera dem till underordnade mål.
* Om du vill aktivera potentiella målgrupper för destinationer måste du ha anslutit till ett mål. Om du inte redan har gjort det går du till [målkatalogen](../catalog/overview.md), bläddrar bland de mål som stöds och konfigurerar det mål som du vill använda. Mer information finns i självstudiekursen [Ansluta till mål](./connect-destination.md).

### Nödvändiga behörigheter {#permissions}

Om du vill aktivera potentiella målgrupper behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Activate Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Bläddra i målkatalogen för att se till att du har de behörigheter som krävs för att aktivera potentiella målgrupper. Om ett mål har en **[!UICONTROL Activate]**-kontroll har du rätt behörighet.

## Välj mål {#select-destination}

Följ instruktionerna för att välja ett mål där du kan exportera datauppsättningar:

1. Gå till **[!UICONTROL Connections > Destinations]** och välj fliken **[!UICONTROL Catalog]**.

   ![Fliken Målkatalog med katalogkontrollen markerad.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

2. Välj **[!UICONTROL Activate]** på kortet som motsvarar målet som du vill exportera datauppsättningar till.

>[!TIP]
>
>Destinationerna som kan exportera profilmålgrupper indikeras med en ikon i kortets övre högra hörn, som liknar målet som markeras nedan, eller så kan du använda datatypsfiltret för att endast visa destinationer som kan exportera potentiella målgrupper, vilket [visas högre på sidan](#supported-destinations).

![Amazon S3-målsida som kan exportera profilmålgrupper markerade.](/help/destinations/assets/ui/activate-prospect-audiences/amazon-s3-icon-activate-prospect-audiences.png)

1. Välj **[!UICONTROL Data type Prospects]**, följt av målanslutningen som du vill exportera datauppsättningar till, och välj sedan **[!UICONTROL Next]**.

>[!TIP]
> 
>Om du vill konfigurera ett nytt mål för att aktivera potentiella målgrupper väljer du **[!UICONTROL Configure new destination]** för att utlösa arbetsflödet [Anslut till mål](/help/destinations/ui/connect-destination.md).

![Arbetsflöde för målaktivering med kontroll för potentiell kund markerat.](/help/destinations/assets/ui/activate-prospect-audiences/activate-prospects-highlighted.png)

1. Gå till nästa avsnitt för att [välja dina profilmålgrupper](#select-profile-audiences) för export.

## Välj era potentiella målgrupper {#select-prospect-audiences}

Använd kryssrutorna till vänster om namnen på de potentiella målgrupperna för att välja de målgrupper som du vill exportera till målet och välj sedan **[!UICONTROL Next]**. Observera att endast de potentiella målgrupperna visas i den här vyn och att inga andra målgrupper visas.

![Arbetsflöde för dataexport med steget Välj målgrupper där du kan välja vilka potentiella målgrupper som ska exporteras.](/help/destinations/assets/ui/activate-prospect-audiences/select-prospect-audiences.png)

## Schemaläggning och nästa steg

För resten av aktiveringsarbetsflödet för att exportera målgrupper med potentiella kunder, läs självstudiekursen om hur du aktiverar data till filbaserade mål. Fortsätt från [schemalägg målgruppsexportsteget](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).

>[!NOTE]
>
>Observera att i schemaläggningssteget kan du bara [exportera fullständiga filer](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) i arbetsflödet för att aktivera potentiella målgrupper. Inkrementell filexport stöds inte.

<!--

Note that we will need to add links to other destination types here as more destinations become supported 

-->

## Andra användningsområden som uppnås genom stöd för partnerdata {#other-use-cases}

Upptäck fler användningsfall tack vare partnerdatastöd i Real-Time CDP:

* [Komplettera förstahandsprofiler med attribut från betrodda datapartners](/help/rtcdp/partner-data/supplement-first-party-profiles.md) för att förbättra er grund för data och få nya insikter om er kundbas och få bättre målgruppsoptimering.
* Använd datastöd från tredje part i Real-Time CDP för att [utöka din profilbas med profiler för potentiella kunder från datapartner och engagera med dem för att förvärva eller nå nya kunder](/help/rtcdp/partner-data/prospecting.md).
* [Utnyttja partnerstödd igenkänning för personalisering av webbplatsupplevelser](/help/rtcdp/partner-data/onsite-personalization.md) under besöket utan att användaren behöver autentisera eller ha en tidigare historik med varumärket.
