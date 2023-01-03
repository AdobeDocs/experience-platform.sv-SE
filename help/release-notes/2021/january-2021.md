---
title: Versionsinformation om Adobe Experience Platform januari 2021
description: Versionsinformation januari 2021 för Adobe Experience Platform.
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 27 januari 2021**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] gör det möjligt för datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Funktioner för reguljära uttryck | [!DNL Data Prep] Mapper har nu stöd för att matcha och extrahera delar av indatafältet baserat på reguljära uttryck. |

Mer information finns i [[!DNL Data Prep] översikt](../../data-prep/home.md).

## Mål  {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya destinationer**

| Destination | Beskrivning |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] är en Microsoft objektlagringslösning för molnet. |

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Avancerad ID-matchning | Förbättringar av målgruppsmatchningsmöjligheterna i [!DNL Facebook Custom Audiences] och [!DNL Google Customer Match]genom att lägga till stöd för ytterligare identitetsmatchning, som externa ID:n, telefonnummer och mobila enhets-ID:n. Mer information finns i följande dokumentation: <ul><li>[Facebook](../../destinations/catalog/social/facebook.md)</li><li>[Google kundmatchningsmål](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[Aktivera målgruppsdata för att direktuppspela segmentexportmål](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

Mer information finns på [destinationer, översikt](../../destinations/home.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med kundprofilen i realtid kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. [!DNL Profile] gör att ni kan sammanställa kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Ta bort datauppsättning från profilarkivet | När du tar bort en datauppsättning från Experience Platform Data Lake tas den automatiskt bort även från profilarkivet. Du behöver inte längre använda API-slutpunkten för profilsystemjobb för att göra en borttagningsbegäran för att ta bort datauppsättningen explicit från profilarkivet. Mer information finns i [API-slutpunktsguide för profilsystemjobb](../../profile/api/profile-system-jobs.md). |
| Beräknat ID-namnutrymmesantal för ett givet segment | För uppskattat antal profiler rapporterar API:t för förhandsgranskning nu:<ul><li>Totalt antal uppskattade profiler i ett segment för ett givet namnutrymme.</li><li>Totalt antal beräknade profiler i profilunionens schema för ett givet namnområde.</li></ul>Mer information finns i [API-slutpunktsguide för förhandsgranskning av profil](../../profile/api/preview-sample-status.md). |

Mer information om kundprofil i realtid, inklusive självstudiekurser och bästa metoder för att arbeta med [!DNL Profile] data, kan du börja med att läsa [Översikt över kundprofiler i realtid](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättringar av Adobe Audience Manager källanslutning | Nu kan du filtrera och välja enskilda förstahandssegment från Audience Manager till att importera till Platform, samt filtrera bort förstahandsegenskaper. Se självstudiekursen om [skapa en Audience Manager-källkoppling](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) för mer information. |
| [!DNL Google BigQuery] förbättringar av källkopplingen | Du kan nu importera filer som är större än 10 GB i en flödeskörning med [!DNL BigQuery] källkoppling. Se [[!DNL BigQuery] översikt över källkoppling](../../sources/connectors/databases/bigquery.md) för mer information. |
| Stöd för komplexa datatyper för molnlagring | Du kan nu importera komplexa datatyper, till exempel arrayer i JSON-filer, när du använder en anslutning till en molnlagringskälla. Se självstudiekurserna om hur du skapar ett molnlagringsdataflöde [i användargränssnittet](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) eller [med [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md) för mer information. |
| Stöd för huvudnyckelbaserad autentisering av tjänster för [!DNL Microsoft Dynamics] källa | Nu kan du autentisera [!DNL Dynamics] konto med en huvudnyckel för tjänsten som ett alternativ till lösenordsbaserad autentisering. Se [[!DNL Dynamics] översikt över källkoppling](../../sources/connectors/crm/ms-dynamics.md) för mer information. |
| Stöd för anpassade avgränsare i molnlagringskällor | Du kan nu ange en egen kolumnavgränsare, till exempel ett komma (`,`), tabb (`\t`), eller ett rör (`|`) för att samla in avgränsade filer i användargränssnittet. Se självstudiekursen om [skapa ett dataflöde med en anslutning för molnlagringskälla](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) för mer information |

Mer information om källor finns i [källöversikt](../../sources/home.md).
