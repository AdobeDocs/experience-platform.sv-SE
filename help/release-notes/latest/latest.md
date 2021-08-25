---
title: Versionsinformation för Adobe Experience Platform
description: Den senaste versionsinformationen för Adobe Experience Platform.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 3d6402a35e1813b94af866d7aaea975d4f103906
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 3%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 25 augusti 2021**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Insikter om observerbarhet](#observability)
- [Kundprofil i realtid](#profile)
- [Källor](#sources)

## Insikter om observerbarhet {#observability}

Med observabilitetsinsikter kan ni övervaka plattformsaktiviteter med hjälp av statistik och händelsemeddelanden.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Larm | Du kan nu prenumerera på viktiga aviseringar om arbetsflöden som körs på plattformen. När du har prenumererat på specifika varningsregler får du meddelanden och e-postmeddelanden i användargränssnittet när en viktig livscykelhändelse inträffar (t.ex. slutförd datainmatning) eller om det finns problem som kräver din uppmärksamhet (t.ex. ett intag-flöde som misslyckas eller ett segmentjobb som tar längre tid än förväntat). Mer information finns i [varningsöversikten](../../observability/alerts/overview.md). |

Mer information om tjänsten finns i [Insights overview](../../observability/home.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med kundprofilen i realtid kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Med hjälp av profilen kan ni sammanställa kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

| Funktion | Beskrivning |
| ------- | ----------- |
| Bläddra bland profiler efter sammanfogningsprincip eller identitet | När du bläddrar bland profiler i Experience Platform kan du nu bläddra genom en sammanfogningsprincip och förhandsgranska 20 exempelprofiler baserat på den valda sammanfogningsprincipen. Du kan också bläddra efter identitet för att söka efter en viss profil med hjälp av ett identitetsnamnutrymme och relaterat identitetsvärde. Mer information finns i handboken [Kundprofil i realtid](../../profile/ui/user-guide.md). |

Om du vill veta mer om kundprofil i realtid, inklusive självstudiekurser och bästa praxis för arbete med profildata, kan du börja med att läsa [Kundprofilöversikt i realtid](../../profile/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

| Funktion | Beskrivning |
| ------- | ----------- |
| Källanslutning för lokal filöverföring | Kategorin för filinläsning har bytt namn till det lokala systemet, vilket gör att du kan överföra lokala filer direkt till plattformen med den lokala filöverföringskopplingen. Data som hämtas via den här kopplingen kan övervakas via kontrollpanelen för övervakning. Mer information finns i översikten över den lokala filöverföringskällan](../../sources/connectors/local-system/local-file-upload.md).[ |

Mer information om källor finns i [Källor - översikt](../../sources/home.md).
