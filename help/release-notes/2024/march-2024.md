---
title: Versionsinformation om Adobe Experience Platform mars 2024
description: Versionsinformationen för Adobe Experience Platform i mars 2024.
exl-id: cab47a76-04f3-48ec-82aa-d17645e4eb15
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 3%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 19 mars 2024**

>[!TIP]
>
>Använd [Adobe Experience Platform-ordlistan](/help/landing/glossary.md) för att bekanta dig med terminologi som används i Real-time Customer Data Platform och Adobe Experience Platform. Om du inte kan hitta en viss term som du söker efter kan du använda alternativen för feedback på sidan och begära att nya termer läggs till i ordlistan.

Uppdateringar av befintliga funktioner i Experience Platform:

- [Katalogtjänst](#catalog-service)
- [Datainsamling](#data-collection)
- [Dataförberedelse](#data-prep)
- [Mål ](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)

## Katalogtjänst {#catalog-service}

Katalogtjänsten är arkivsystemet för dataplatser och -länkar inom Adobe Experience Platform. Alla data som importeras till Experience Platform lagras i datarjön som filer och kataloger, men i Katalog finns metadata och beskrivning av dessa filer och kataloger för sökning och övervakning.

| Funktion | Beskrivning |
| --- | --- |
| Fler åtgärder | Om du vill göra åtgärderna mer flexibla och hjälpa dig att hantera dina data kan du nu använda funktionen&quot;Fler åtgärder&quot; från detaljvyn för att utföra ytterligare uppgifter på en datauppsättning. Du kan antingen ta bort datauppsättningen eller aktivera den för användning med kundprofilen i realtid från informationssidan för en vald datauppsättning.<br>**Obs!** Om du aktiverar en datauppsättning för profilinmatning måste datauppsättningens schema vara kompatibelt med kundprofilen i realtid.<br>![Arbetsytan Datauppsättningar med listrutan [!UICONTROL ... More] markerad.](../2024/assets/march/more-actions.png "Arbetsytan Datauppsättningar med listrutan Mer markerad."){width="100" zoomable="yes"}.<br>Läs [användarhandboken för datauppsättningar](../../catalog/datasets/user-guide.md) om du vill ha mer information. |

{style="table-layout:auto"}

Mer information om katalogtjänsten finns i [Katalogtjänstöversikt](../../catalog/home.md).

## Dataförberedelse {#data-prep}

Med Data Prep kan datatekniker mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nya mappningsfunktioner för Adobe Analytics | Nu kan du använda följande funktioner för att extrahera händelsedata från Adobe Analytics: <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> Mer information om de här funktionerna finns i [handboken om dataförberedelser](../../data-prep/functions.md#analytics-functions) |

{style="table-layout:auto"}

Mer information om Prep av data finns i [Översikt över Prep av data](../../data-prep/home.md).

## Datainsamling {#data-collection}

Adobe Experience Platform erbjuder en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya funktioner**

| Typ | Funktion | Beskrivning |
| --- | --- | --- |
| Tillägg | [!DNL Merkury]-taggtillägg | [[!DNL Merkury] Taggtillägget](https://exchange.adobe.com/apps/ec/600027/merkury-tag) ger branschledande matchningsfrekvenser för anonyma webbplatsbesökare till ett [!DNL Merkury]-ID. Varumärken kan utnyttja taggen [!DNL Merkury] och Adobe för att leverera personaliserade webbplatsupplevelser i realtid. Dessutom möjliggör taggen [!DNL Merkury] tillväxt av digitala data från första part tillsammans med anslutna kundprofiler online och offline. |

{style="table-layout:auto"}

Läs [datainsamlingsöversikten](../../tags/home.md) om du vill veta mer om datainsamling.

## Mål  {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya och uppdaterade mål** {#new-updated-destinations}

| Mål | Typ | Beskrivning |
| ----------- | --------- | ----------- |
| [(Beta) Dataförbättringsanslutning för Acxiom](../../destinations/catalog/data-partner/acxiom-data-enhancement.md) | Nytt | Använd den här kopplingen för att aktivera förstahandsprofiler från Real-Time CDP till Acxiom för att berika och använda data i alla marknadsföringskanaler. Du kan sedan använda Acxiom-källan för att importera profiler med förbättrade data och arbeta med dem i Real-Time CDP. |
| [(Beta) Prospect Suppression-anslutning för Acxiom ](../../destinations/catalog/data-partner/acxiom-prospect-suppression.md) | Nytt | Exportera era egna målgrupper till Acxiom-destinationen så att Acxiom kan inaktivera kända eller konverterade kunder. Använd sedan [källkopplingen för prospektering av dataimport](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md) för att importera och aktivera listor med potentiella kunder från Acxiom, med dina kända eller konverterade kunder borttagna. |
| [Amazon Ads-anslutning](../../destinations/catalog/advertising/amazon-ads.md) | Uppdatera | När du exporterar data till Amazon Ads-målet kan du nu dirigera data till Amazon DSP eller Amazon Marketing Cloud (nytt). |
| [LiveRamp-anslutning för onboarding](../../destinations/catalog/advertising/liveramp-onboarding.md) | Uppdatera | Målet för LiveRamp Onboarding har nu stöd för leveranser till instanser [!DNL LiveRamp] [!DNL SFTP] i Europa och Australien. Den maximala storleken på den exporterade filen ökades också till 10 miljoner rader (från 5 miljoner tidigare). |

{style="table-layout:auto"}

<!--

**New or updated functionality** {#destinations-new-updated-functionality}

-->

Mer allmän information om destinationer finns i [målöversikten](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för datatypen Experience Platform UI map | Anpassa XDM-datastrukturen (Experience Data Model) ytterligare genom att definiera kartfält i plattformens användargränssnitt. Nu kan du skapa mappningsfält i Schemaredigeraren för att modellera flexibla datastrukturer eller effektivt lagra nyckelvärdepar. Välj &quot;Karta&quot; i listrutan Typ när du definierar ett nytt fält för att konfigurera delfält och tilldela dem till fältgrupper. Värdetyper som stöds är sträng och heltal.<br>![Schemaredigeraren med fälten för typ och mappningsvärdetyp markerade.](../2024/assets/march/maps.png "Schemaredigeraren med fälten för typ och mappningsvärdetyp markerade."){width="100" zoomable="yes"}<br> Mer information om hur du [definierar kartfält i användargränssnittet](../../xdm/ui/fields/map.md) finns i gränssnittsguiden. |

{style="table-layout:auto"}

Mer information om XDM i Platform finns i [XDM-systemöversikt](../../xdm/home.md).

## Segmenteringstjänst {#segmentation}

Med [!DNL Segmentation Service] kan du segmentera data som lagras i [!DNL Experience Platform] och som relaterar till individer (t.ex. kunder, potentiella kunder, användare eller organisationer) till målgrupper. Du kan skapa målgrupper med hjälp av segmentdefinitioner eller andra källor från dina [!DNL Real-Time Customer Profile]-data. Dessa målgrupper är centralt konfigurerade och underhållna på [!DNL Platform] och är tillgängliga för alla Adobe-lösningar.

**Ny funktion**

| Funktion | Beskrivning |
| ------- | ----------- |
| Massåtgärder | Målgruppslagret har nu stöd för massåtgärder. Med gruppåtgärder kan du snabbt markera flera målgrupper för att flytta dem till en mapp, lägga till taggar, använda etiketter eller ta bort. <br> ![Massåtgärder på arbetsytan för publikens användargränssnitt.](../2024/assets/march/bulk-actions.png "Massåtgärder på arbetsytan för publikens användargränssnitt."){width="100" zoomable="yes"} <br>Mer information om den här funktionen finns i [Översikt över målportalen](../../segmentation/ui/audience-portal.md#bulk-actions). |

{style="table-layout:auto"}

Mer information om segmenteringstjänsten finns i [Översikt över segmenteringstjänsten](../../segmentation/home.md).

## Källor {#sources}

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya och uppdaterade källor**

| Funktion | Typ | Beskrivning |
| --- | --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Acxiom Data Ingestion] | Nytt | Använd [[!DNL Acxiom Data Ingestion] source](../../sources/tutorials/ui/create/data-partners/acxiom-data-ingestion.md) för att importera [!DNL Acxiom]-data till Real-time Customer Data Platform och berika förstapartsprofiler. Sedan kan du använda dina [!DNL Acxiom]-berikade förstahandsprofiler för att förbättra målgrupper och aktivera i alla marknadsföringskanaler. <br> ![Acxiom-källan för datainmatning.](../2024/assets/march/acxiom-data-ingestion.png "Ny Acxiom-källa för datainmatning."){width="100" zoomable="yes"} <br> Läs [[!DNL Acxiom Data Ingestion] översikten](../../sources/connectors/data-partners/acxiom-data-ingestion.md) för information om hur du kommer igång. |
| [!BADGE Beta]{type=Informative} [!DNL Stripe] | Nytt | Använd [[!DNL Stripe] källa](../../sources/connectors/payments/stripe.md) för att importera data som dina kunder har tagit in i Experience Platform under inköpsflödet. När ni väl har inhämtat data kan ni använda dessa data för att skapa personaliserade erbjudanden och få bättre affärsinsikter. <br> ![Stripe-källan.](../2024/assets/march/stripe.png "Ny Stripe-källa."){width="100" zoomable="yes"} <br> Läs [[!DNL Stripe] översikten](../../sources/connectors/payments/stripe.md) för information om hur du kommer igång. |
| Gränssnittsstöd för [!DNL Snowflake Streaming] | Nytt | Du kan nu använda [[!DNL Snowflake Streaming] source](../../sources/tutorials/ui/create/databases/snowflake-streaming.md) i användargränssnittet för Experience Platform för att strömma data från din [!DNL Snowflake]-databas. <br> ![Källan för direktuppspelning i Snowflake.](../2024/assets/march/snowflake-streaming.png "Ny strömningskälla för Snowflake."){width="100" zoomable="yes"} <br> Läs [[!DNL Snowflake Streaming] översikten](../../sources/connectors/databases/snowflake-streaming.md) för information om hur du kommer igång. |

{style="table-layout:auto"}

Mer information om källor finns i [Källöversikt](../../sources/home.md).
