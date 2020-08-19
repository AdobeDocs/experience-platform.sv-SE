---
keywords: destinations;destination;destinations detail page;destinations details page
title: Sidan Destinationsinformation
seo-title: Sidan Destinationsinformation
description: 'På informationssidan för ett enskilt mål finns en översikt över målinformationen, t.ex. målnamn, ID, segment som är mappade till målet samt kontroller för att redigera aktiveringen samt för att aktivera och inaktivera dataflödet. '
seo-description: 'På informationssidan för ett enskilt mål finns en översikt över målinformationen, t.ex. målnamn, ID, segment som är mappade till målet samt kontroller för att redigera aktiveringen samt för att aktivera och inaktivera dataflödet. '
translation-type: tm+mt
source-git-commit: 15323134f0c626cad2c4e90b3e1c0662cf7e57dd
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---


# Sidan med målinformation {#destinations-details-page}

På informationssidan för ett enskilt mål finns en översikt över målinformationen, t.ex. målnamn, ID, segment som är mappade till målet samt kontroller för att redigera aktiveringen samt för att aktivera och inaktivera dataflödet. Om du vill visa den här informationen går du till **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** och klickar på namnet på målet som du vill arbeta med.

Kärnkomponenterna för en enskild destination är:

* 1 - Målnamn och ID
* 2 - Segment aktiverade till målet
* 3 - Högerspaltsinformation
* 4 - Kontroller för att redigera aktivering och aktivera/inaktivera dataflöde

![Numrerad målsida](/help/rtcdp/destinations/assets/destination-page-numbered.png)

Navigera till en enskild målsida för att få en översikt över målinformationen, till exempel:

## 1. Destinationsnamn och -ID

Målnamnet visas i sidrubriken och mål-ID i sidans URL.

## 2. Segment aktiverade till målet

I det här avsnittet visas vilka segment som är mappade till målet samt ytterligare information om dessa segment. Se tabellen nedan för mer information:

| Objekt | Beskrivning |
---------|----------|
| Segmentnamn | Namnet på ditt segment. |
| Segmentbeskrivning | Beskrivning av ditt segment. |
| Startdatum | Det datum då dessa segment aktiveras till målet. |
| Slutdatum | Det datum då dessa segment slutar att aktiveras för målet. |
| Mappnings-ID | *Inte tillgängligt för e-postmarknadsföringsmål*. Anger det ID som segmentet är känt med i målplattformen. |

## 3. Höger rälsinformation

Rätt spår innehåller information om destinationen. Se tabellen nedan för mer information:

| Objekt | Beskrivning |
---------|----------|
| Plattform | Representerar målplattformen som målgrupperna skickas till. Mer information finns i [Målkatalog](/help/rtcdp/destinations/destinations-catalog.md) . |
| Beskrivning | Du kan redigera beskrivningen av målflödet. |
| Kategori | Anger typen av mål. Mer information finns i [Målkatalog](/help/rtcdp/destinations/destinations-catalog.md) . |
| Anslutningstyp | Anger i vilket format era målgrupper skickas till målet. Kan vara **[!UICONTROL Cookie]** eller **[!UICONTROL Profile-based]**. |
| Frekvens | Anger hur ofta målgrupperna skickas till målet. Kan vara **[!UICONTROL Streaming]** eller **[!UICONTROL Batch]**. |
| Identitet | Representerar det identitetsnamnutrymme som accepteras av målet. Identitetsfältet kan till exempel vara GAID, IDFA, email. Mer information om alla godkända identitetsnamnutrymmen finns i Standardnamnutrymmen i [översikten](../../identity-service/namespaces.md)över identitetsnamnen. |
| Skapad av | Anger den användare som skapade det här målflödet. |
| Skapad | Anger UTC-datum och UTC-tid när målflödet skapades. |

## 4. Kontroller för att redigera aktivering och aktivera/inaktivera dataflöde

Med redigeringsaktiveringskontrollen kan du redigera vilka segment som mappas till målet. Tryck på Redigera aktivering för att öppna [segmentaktiveringsarbetsflödet](/help/rtcdp/destinations/activate-destinations.md).

Använd **Aktivera/inaktivera** för att starta och pausa dataexporten till ett mål.