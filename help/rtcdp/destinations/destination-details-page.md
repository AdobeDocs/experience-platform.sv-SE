---
title: Sidan Destinationsinformation
seo-title: Sidan Destinationsinformation
description: 'På informationssidan för ett enskilt mål finns en översikt över målinformationen, t.ex. målnamn, ID, segment som är mappade till målet samt kontroller för att redigera aktiveringen samt för att aktivera och inaktivera dataflödet. '
seo-description: 'På informationssidan för ett enskilt mål finns en översikt över målinformationen, t.ex. målnamn, ID, segment som är mappade till målet samt kontroller för att redigera aktiveringen samt för att aktivera och inaktivera dataflödet. '
translation-type: tm+mt
source-git-commit: b784b67092ea8d30ad00cda9a40779b3890862fd

---


# Sidan med målinformation {#destinations-details-page}

På informationssidan för ett enskilt mål finns en översikt över målinformationen, t.ex. målnamn, ID, segment som är mappade till målet samt kontroller för att redigera aktiveringen samt för att aktivera och inaktivera dataflödet. Om du vill visa den här informationen går du till **Destinationer** > **Bläddra** och klickar på namnet på målet som du vill arbeta med.

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
| Anslutningstyp | Anger i vilket format era målgrupper skickas till målet. Kan vara **cookie** eller **profilbaserad**. |
| Frekvens | Anger hur ofta målgrupperna skickas till målet. Kan vara **Streaming** eller **Batch**. |
| Identitet | Representerar det identitetsnamnutrymme som accepteras av målet. Identitetsfältet kan till exempel vara GAID, IDFA, email. Mer information om alla godkända identitetsnamnutrymmen finns i Standardnamnutrymmen i [översikten](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md)över identitetsnamnen. |
| Skapad av | Anger den användare som skapade det här målflödet. |
| Skapad | Anger UTC-datum och UTC-tid när målflödet skapades. |

## 4. Kontroller för att redigera aktivering och aktivera/inaktivera dataflöde

Med redigeringsaktiveringskontrollen kan du redigera vilka segment som mappas till målet. Tryck på Redigera aktivering för att öppna [segmentaktiveringsarbetsflödet](/help/rtcdp/destinations/activate-destinations.md).

Använd **Aktivera/inaktivera** för att starta och pausa dataexporten till ett mål.