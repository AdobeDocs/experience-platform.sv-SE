---
title: Versionsinformation om Adobe Experience Platform från augusti 2021
description: Versionsinformation för augusti 2021 för Adobe Experience Platform.
doc-type: release notes
last-update: August 25, 2021
author: ens28527
exl-id: 0513b9dc-b16c-43b3-8e17-4be4499308d4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 27%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 25 augusti 2021**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Mål](#destinations)
- [Insikter om observerbarhet](#observability)
- [Kundprofil i realtid](#profile)
- [Källor](#sources)

## Mål {#destinations}

Destinationer är färdiga integrationer med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Du kan använda mål för att aktivera dina kända och okända data för marknadsföringskampanjer över flera kanaler, e-postkampanjer, riktad reklam och många andra användningsområden.

**Nya mål**

| Mål | Beskrivning |
| ----------- | ----------- |
| [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md) | Målet för Airship Attributes, som tidigare fanns i betaversion, är nu allmänt tillgängligt. |
| [[!DNL Airship Tags]](../../destinations/catalog/mobile-engagement/airship-tags.md) | Målet för Airship Tags, som tidigare fanns i betaversion, är nu allmänt tillgängligt. |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | Braze-målet, som tidigare fanns i betaversionen, är nu allmänt tillgängligt. |
| [[!DNL Pinterest Customer List]](../../destinations/catalog/advertising/pinterest.md) | Med Pinterest kundlistdestination kan ni skapa målgrupper utifrån era kundlistor, personer som har besökt er webbplats eller personer som redan har interagerat med ert innehåll på Pinterest. |
| [[!DNL Twitter Custom Audiences]](../../destinations/catalog/social/twitter.md) | Rikta er till era befintliga följare och kunder på Twitter och skapa relevanta återmarknadsföringskampanjer genom att aktivera era målgrupper som skapats inom Adobe Experience Platform. |
| [[!DNL Verizon Media/Yahoo DataX]](../../destinations/catalog/advertising/datax.md) | DataX är en aggregerad Verizon Media/Yahoo-infrastruktur som är värd för olika komponenter som gör att Verizon Media/Yahoo kan utbyta data med sina externa partner på ett säkert, automatiserat och skalbart sätt. |

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [[!DNL Destination SDK]](../../destinations/destination-sdk/overview.md) | Adobe Experience Platform Destination SDK är en serie konfigurations-API:er som gör att du kan konfigurera målintegreringsmönster så att Experience Platform kan leverera målgrupps- och profildata till slutpunkten, baserat på vilka data- och autentiseringsformat du väljer. Konfigurationerna lagras i Experience Platform och kan hämtas via API för ytterligare uppdateringar. |
| [Användbarhetsförbättringar för mål](../../destinations/ui/activation-overview.md) | Förbättrad användarvänlighet för destinationer gör det möjligt för marknadsförare att smidigt aktivera segment till befintliga destinationer. |

För mer allmän information om mål, se [översikt över mål](../../destinations/home.md).

## Insikter om observerbarhet {#observability}

Med observationsinsikter kan ni övervaka Experience Platform-aktiviteter med hjälp av statistik och händelsemeddelanden.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Aviseringar | Du kan nu prenumerera på viktiga aviseringar om arbetsflöden som körs på Experience Platform. När du har prenumererat på specifika varningsregler får du meddelanden och e-postmeddelanden i användargränssnittet när en viktig livscykelhändelse inträffar (t.ex. slutförd datainmatning) eller om det finns problem som kräver din uppmärksamhet (t.ex. ett intag-flöde som misslyckas eller ett segmentjobb som tar längre tid än förväntat). Mer information finns i [varningsöversikten](../../observability/alerts/overview.md). |

Mer information om tjänsten finns i översikten [Insikter om observabilitet](../../observability/home.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan du skapa samordnade, konsekventa och relevanta upplevelser för dina kunder, oavsett var eller när de interagerar med ditt varumärke. Med kundprofilen i realtid får du en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online, offline, CRM och data från tredje part. Med profilen kan du konsolidera kunddata till en enhetlig vy som ger en handlingsbar, tidsstämplad redogörelse för varje kundinteraktion.

| Funktion | Beskrivning |
| ------- | ----------- |
| Bläddra bland profiler efter sammanfogningsprincip eller identitet | När du bläddrar bland profiler i Experience Platform kan du nu bläddra genom en sammanfogningsprincip och förhandsgranska 20 exempelprofiler baserat på den valda sammanfogningsprincipen. Du kan också bläddra efter identitet för att söka efter en viss profil med hjälp av ett identitetsnamnutrymme och relaterat identitetsvärde. Mer information finns i [Användargränssnittet för kundprofil i realtid](../../profile/ui/user-guide.md). |

Om du vill veta mer om kundprofilen i realtid, inklusive självstudiekurser och bästa praxis för arbete med profildata, börjar du med att läsa [Översikt över kundprofilen i realtid](../../profile/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

| Funktion | Beskrivning |
| ------- | ----------- |
| Källanslutning för lokal filöverföring | Kategorin för filinläsning har bytt namn till det lokala systemet, så att du kan överföra lokala filer direkt till Experience Platform med den lokala filöverföringskopplingen. Data som hämtas via den här kopplingen kan övervakas via kontrollpanelen för övervakning. Mer information finns i [Översikt över den lokala filöverföringskällan](../../sources/connectors/local-system/local-file-upload.md). |

Mer information om källor finns i [Källöversikt](../../sources/home.md).
