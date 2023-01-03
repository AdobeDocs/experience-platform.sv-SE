---
title: Versionsinformation om Adobe Experience Platform oktober 2020
description: Versionsinformation från oktober 2020 för Adobe Experience Platform.
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
exl-id: 89f5e2bd-8892-4d3f-a3fe-5433bb5ece7a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 1%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 14 oktober 2020**

- [Dataprep](#data-prep)
- [Kundprofil i realtid](#profile)
- [Segmenteringstjänst](#segmentation)
- [Källor](#sources)
- [Tid till värde](#time-to-value)

## Dataprep {#data-prep}

Med Data Prep kan datatekniker mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| `is_set` funktion | The `is_set` kan du kontrollera om det finns ett attribut i källdata. `is_set` kan användas i kombination med `is_empty` för att kontrollera både förekomsten av attributet och förekomsten av värdet i attributet. |
| `get_values` funktion | The `get_values` kan du hämta värden från indatamappningen för en given nyckel. |

Mer information finns i [Översikt över datapreflight](../../data-prep/home.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med [!DNL Real-Time Customer Profile]kan ni se en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. [!DNL Profile] kan ni sammanställa era olika kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

| Funktion | Beskrivning |
| ------- | ----------- |
| API-tillägg för förhandsgranskning av profil | API för förhandsgranskning av profil (`/previewsamplestatus`) kan nu visa en uppdelning av det totala antalet profilfragment i hela IMS-organisationen samt visa distributionen av profilfragment över identitetsnamnutrymmen. |
| Uppdateringar av unionens schemavy | I användargränssnittet i Experience Platform är det enklare att hitta information om alla scheman och datauppsättningar som bidrar till unionsschemat samt attribut för ytnycklar som identitets- och relationsfält. Dessa uppdateringar förbättrar möjligheten att felsöka och verifiera att profiler är korrekt konfigurerade, identiteterna är korrekt sammanfogade och data har importerats. |

Mer information om [!DNL Real-Time Customer Profile], inklusive självstudiekurser och metodtips för att arbeta med [!DNL Profile] data, läs [Översikt över kundprofiler i realtid](../../profile/home.md).

## Segmenteringstjänst {#segmentation}

Adobe Experience Platform Segmentation Service har ett användargränssnitt och RESTful API som gör att du kan skapa segment och generera målgrupper från din [!DNL Real-Time Customer Profile] data. Dessa segment är centralt konfigurerade och underhållna på [!DNL Platform], så att de är lättillgängliga i alla Adobe-program.

[!DNL Segmentation Service] definierar en viss underuppsättning profiler genom att beskriva kriterierna som särskiljer en säljbar grupp av personer inom kundbasen. Segment kan baseras på registerdata (t.ex. demografisk information) eller tidsseriehändelser som representerar kundinteraktioner med ert varumärke.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Borttagning av begränsning av direktuppspelad segmentering | Sjudagarsgränsen för uppslagsperioden har tagits bort. |

Mer information om [!DNL Segmentation Service], se [Översikt över segmentering](../../segmentation/home.md)

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| SSH-autentiseringsstöd för SFTP | Du kan ansluta ditt SFTP-konto till [!DNL Platform] med RSA/DSA Open SSH-nycklar. Se [Översikt över SFTP](../../sources/connectors/cloud-storage/sftp.md) för mer information. |
| UX-förbättringar | Du kan aktivera din datauppsättning för [!DNL Profile] under dataöverföringsprocessen. Se [arbetsflöde för dataflöde för molnlagring](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) självstudiekurs för mer information. |

Mer information om källor finns i [källöversikt](../../sources/home.md).

## Tid till värde {#time-to-value}

Med Adobe Experience Platform kan marknadsföringsteamen skapa en helhetsbild av sina kunder utan att behöva omfattande datateknik. Målet är att snabba upp team och öka värdet med datahastigheten.

&quot;Time to Value&quot; skär ut på olika personligheter. Datatekniker kan utföra uppgifter på ett effektivt och accelererat sätt med genomskinlighet i dataaktiviteten, så att en robust, skalbar kundprofil i realtid blir tillgänglig snabbare. Marknadsförarna kan sedan använda den kompletta, robusta kundprofilen för segmentering och aktivering.

### Funktioner i korthet

#### Schema

Uppgraderar användbarhet och arbetsflöde och ger körklara insikter, standardisering och genomskinlighet för nyckelfält i schemakompositioner. Exponerar datalinje för kombinationen av enskilda datamodeller, som representeras av fackschemat, och ger insikt i strukturen och ingredienserna till kundprofilen i realtid.

- Uppgradering av schemaarbetsflöde
   - Använd genvägar för den vanligaste typen av XDM-scheman, med automatiska inställningar i schemaredigeraren och rekommendationer för schemafältgrupper baserade på dina mål
   - Öka arbetsflödets effektivitet med möjlighet att markera och förhandsgranska flera fältgrupper
   - Ge genomskinlighet för nyckelattribut för schemakomposition, inklusive identitet, relation samt obligatoriska och inaktuella fält
- Genomskinlighet för datarad för unionsschema och nyckelattribut

#### Inmatning och insamling av data

Uppgraderingen av automatisk mappning, förgranskning av mappning och användbarhet gör att data kan användas i profiler, segmentering och aktivering från alla plattformar och källor. Systemet har den effektivitet och intelligens som krävs för att göra den här processen enklare att använda, även utanför IT-avdelningen.

- Enklare åtkomst till datakällor med katalogsidkort och datatabellsintern uppgradering av åtgärdsmönster
- Beräknat fält/uttryck för datainmatning
- Rekommendationer för datamappning snabbar upp inmatningsprocessen
- Förhandsgranskning och validering av mappning

#### Profilkonfiguration

Marknadsvänligt profilvisningsprogram med anpassning hjälper er att förstå hur en profil är sammansatt för användning vid segmentering, planering och aktivering. Det konsoliderade arbetsflödet överbryggar profilen på ett kontrollerat och effektivt sätt genom att tillhandahålla ett stegvis arbetsflöde för sammanslagningsprinciper.

- Visa varje enskild profil i ett förbättrat profilvisningsprogram som visar en instrumentpanel med fullständig anpassning, vilket möjliggör grupperade flerkanalsdata baserat på marknadsförarens affärsmål.
- Redigera standardattribut och anpassade attribut i widgeten Grundläggande information, efter behov.
- Anpassa widgetar med attribut från kundprofilen i realtid med hjälp av föreningsschemaväljaren. Unionsschemat härleds från de underliggande datamodeller som används inom profildatainmatning.


#### Övervakning

Säkerställer genomskinlighet i dataflödet och ger insikt om hur hälsosam datatrafiken är i systemet från källanslutningar, vilket ger mer självbetjäning och snabbare åtgärder för felsökningssituationer.

- Övervaka alla flödeskörningar och se en detaljerad översikt över varje körning, inklusive slutförandestatus, körningstid, lista över bearbetade filer, fel och körbar diagnostik
