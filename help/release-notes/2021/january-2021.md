---
title: Versionsinformation om Adobe Experience Platform januari 2021
description: Versionsinformationen för Adobe Experience Platform i januari 2021.
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '718'
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

[!DNL Data Prep] tillåter datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Funktioner för reguljära uttryck | [!DNL Data Prep] Mapper har nu stöd för matchning och extrahering av en del av indatafältet baserat på reguljära uttryck. |

Mer information finns i [[!DNL Data Prep] översikten](../../data-prep/home.md).

## Mål  {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya mål**

| Mål | Beskrivning |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] är en Microsoft objektlagringslösning för molnet. |

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Avancerad ID-matchning | Förbättringar av funktioner för målgruppsmatchning i [!DNL Facebook Custom Audiences] och [!DNL Google Customer Match], genom att lägga till stöd för ytterligare identitetsmatchning, som externa ID:n, telefonnummer och mobila enhets-ID:n. Mer information finns i följande dokumentation: <ul><li>[Facebook-mål](../../destinations/catalog/social/facebook.md)</li><li>[Google kundmatchningsmål](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[Aktivera målgruppsdata för att direktuppspela segmentets exportmål](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

Mer information finns på [målöversikten](../../destinations/home.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med kundprofilen i realtid kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Med [!DNL Profile] kan du konsolidera kunddata i en enhetlig vy med ett åtgärdbart, tidsstämplat konto för varje kundinteraktion.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Ta bort datauppsättning från profilarkivet | När du tar bort en datauppsättning från Experience Platform Data Lake tas den automatiskt bort även från profilarkivet. Du behöver inte längre använda API-slutpunkten för profilsystemjobb för att göra en borttagningsbegäran för att ta bort datauppsättningen explicit från profilarkivet. Mer information finns i [API-slutpunktshandboken för profilsystemjobb](../../profile/api/profile-system-jobs.md). |
| Beräknat ID-namnutrymmesantal för ett givet segment | För uppskattat antal profiler rapporterar API:t för förhandsgranskning nu:<ul><li>Totalt antal uppskattade profiler i ett segment för ett givet namnutrymme.</li><li>Totalt antal beräknade profiler i profilunionens schema för ett givet namnområde.</li></ul>Mer information finns i [API-slutpunktshandboken för förhandsgranskning av profil](../../profile/api/preview-sample-status.md). |

Mer information om kundprofil i realtid, inklusive självstudiekurser och bästa praxis för att arbeta med [!DNL Profile]-data, får du genom att läsa [Översikt över kundprofilen i realtid](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Förbättringar av Adobe Audience Manager källanslutning | Nu kan du filtrera och välja enskilda förstahandssegment från Audience Manager till att importera till Platform, samt filtrera bort förstahandsegenskaper. Mer information finns i självstudiekursen [Skapa en Audience Manager-källkoppling](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). |
| [!DNL Google BigQuery] förbättringar av källkopplingen | Du kan nu importera filer som är större än 10 GB i en flödeskörning med [!DNL BigQuery]-källkopplingen. Mer information finns i översikten för [[!DNL BigQuery] källkopplingen](../../sources/connectors/databases/bigquery.md). |
| Stöd för komplexa datatyper för molnlagring | Du kan nu importera komplexa datatyper, till exempel arrayer i JSON-filer, när du använder en anslutning till en molnlagringskälla. Se självstudiekurserna om hur du skapar ett molnlagringsdataflöde [ i gränssnittet ](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) eller [med  [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md) för mer information. |
| Stöd för huvudnyckelbaserad autentisering för tjänsten för källan [!DNL Microsoft Dynamics] | Du kan nu autentisera ditt [!DNL Dynamics]-konto med en tjänsthuvudnyckel som ett alternativ till lösenordsbaserad autentisering. Mer information finns i översikten för [[!DNL Dynamics] källkopplingen](../../sources/connectors/crm/ms-dynamics.md). |
| Stöd för anpassade avgränsare i molnlagringskällor | Du kan nu ange en anpassad kolumnavgränsare, till exempel ett komma (`,`), en flik (`\t`) eller ett rör (`|`), för att samla in avgränsade filer i användargränssnittet. Mer information finns i självstudiekursen [Skapa ett dataflöde med en anslutning för molnlagringskälla](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) |

Mer information om källor finns i [Källöversikt](../../sources/home.md).
