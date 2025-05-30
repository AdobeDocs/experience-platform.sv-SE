---
title: Marketo Measure Ultimate-mål
description: Lär dig hur du ansluter och aktiverar data till Marketo Measure Ultimate-målet.
last-substantial-update: 2023-03-07T00:00:00Z
exl-id: b4220841-8908-41ff-b977-dbeebfa787c8
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# Marketo Measure Ultimate Destination {#mmu-destination}

## Översikt {#overview}

Marketo Measure (tidigare Bizible) ger marknadsförarna insikt i vilka marknadsföringssatsningar som är mest effektiva när det gäller att öka intäkterna och maximera avkastningen på investeringen för deras företag. Marketo Measure är en marknadsföringsattribueringslösning som automatiskt håller reda på och rapporterar om kanalernas prestanda, vilket ger er insyn i vilka kanaler som ökar kundengagemanget och gör att ni kan optimera era era marknadsföringsutgifter i enlighet med detta.

Målet möjliggör dataflöden mellan företag (B2B) från Adobe Experience Platform till Marketo Measure. Kortet är endast tillgängligt för Marketo Measure Ultimate-kunder.

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda Marketo Measure-destinationen finns exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen. Den här integreringen:

* Uppfyller kraven på komplexa data- och resultatrapporter för stora företag.
* Möjliggör B2B-attribueringsrapportering med flera CRM- och marknadsföringssystem.
* Gör det enkelt att lägga in kontaktpunktsdata från tredje part offline.

## Förhandskrav {#prerequisites}

Observera följande krav för Marketo Measure-destinationen:

* Mappning av sandlådor i Experience Platform ska slutföras av administratören på inställningssidan för Marketo Measure. Utan sandlådemappning kan du inte slutföra arbetsflödet för att ansluta till målet och spara och aktivera data.
* Endast datauppsättningar av B2B XDM-klasser kan exporteras (se t.ex. XDM Business Account och XDM Business Opportunity-klasserna). Du kan inte hämta flera datauppsättningar av samma B2B XDM-klass för en viss datakälla.
* Varje datauppsättning kan bara inkluderas i ett dataflöde till Marketo Measure-målet.

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Dataset export]** | Du exporterar rådatamängder som inte är grupperade eller strukturerade efter målgruppsintressen eller kvalifikationer. Läs mer om [datauppsättningsexporter](/help/destinations/destination-types.md#dataset-export-destinations). |
| Exportfrekvens | **[!UICONTROL Batch]** | Detta batchmål exporterar filer till Marketo Measure-plattformen varannan timme. Läs mer om [schemaläggning av datauppsättningsexporter](/help/destinations/ui/export-datasets.md#scheduling). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage and Activate Dataset Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som visas i avsnittet nedan.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.

![Arbetsflödet Anslut till mål för Marketo Measure-målet.](/help/destinations/assets/catalog/adobe/marketo-measure-ultimate/marketo-measure-connect-to-destination.png)

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Exportera datauppsättningar till det här målet {#export-datasets}

>[!IMPORTANT]
> 
>För att kunna aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage and Activate Dataset Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Läs självstudiekursen [Exportera datauppsättningar](/help/destinations/ui/export-datasets.md) om du vill ha omfattande instruktioner om hur du exporterar datauppsättningar till det här målet.

## Validera dataexport {#exported-data}

Om du vill validera en lyckad datauppsättningsexport kan du kontrollera att datauppsättningen har gått igenom till datalagret [Snowflake](https://experienceleague.adobe.com/docs/marketo-measure/using/marketo-measure-data-warehouse/data-warehouse-access-reader-account.html?lang=sv-SE).

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).
