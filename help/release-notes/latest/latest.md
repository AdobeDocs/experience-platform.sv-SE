---
title: Versionsinformation för Adobe Experience Platform
description: Versionsinformation för Experience Platform 14 oktober 2020
doc-type: release notes
last-update: October 13, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 43ceda3d95511c3972fd0588f472c6c412dd95bf
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 2%

---


# Versionsinformation för Adobe Experience Platform

**Releasedatum: 14 oktober 2020**

- [Dataprep](#data-prep)
- [Kundprofil i realtid](#profile)
- [Källor](#sources)

## Dataprep {#data-prep}

Med Data Prep kan datatekniker mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Viktiga funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| `is_set` funktion | Med den här `is_set` funktionen kan du kontrollera om det finns ett attribut i källdata. `is_set` kan användas tillsammans med `is_empty` för att kontrollera både förekomsten av attributet och förekomsten av värdet i attributet. |
| `get_values` funktion | Med den här funktionen kan du hämta värden från indatamappningen för en given nyckel. `get_values` |

Mer information finns i översikten över [dataförberedelser](../../data-prep/home.md).

## Kundprofil i realtid {#profile}

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med [!DNL Real-time Customer Profile]det kan ni få en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. [!DNL Profile] kan ni sammanställa era olika kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

| Funktion | Beskrivning |
| ------- | ----------- |
| API-tillägg för förhandsgranskning av profil | API:t för förhandsgranskning av profil (`/previewsamplestatus`) innehåller nu möjligheten att visa en uppdelning av det totala profilfragmentet i hela IMS-organisationen samt att visa distributionen av profilfragment över identitetsnamnutrymmen. |
| Uppdateringar av unionens schemavy | I användargränssnittet i Experience Platform är det enklare att hitta information om alla scheman och datauppsättningar som bidrar till unionsschemat samt attribut för ytnycklar som identitets- och relationsfält. Dessa uppdateringar förbättrar möjligheten att felsöka och verifiera att profiler är korrekt konfigurerade, identiteterna är korrekt sammanfogade och data har importerats. |

Mer information om [!DNL Real-time Customer Profile]bland annat självstudiekurser och bästa metoder för att arbeta med [!DNL Profile] data finns i [Kundprofilöversikt](../../profile/home.md)i realtid.

## Sources {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av [!DNL Platform] tjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

[!DNL Experience Platform] innehåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| ------- | ----------- |
| Hierarkisk mappning | Du kan förhandsgranska en hierarkisk källfil, som JSON eller Parquet, under dataöverföringsprocessen. |
| SSH-autentiseringsstöd för SFTP | Du kan ansluta ditt SFTP-konto till [!DNL Platform] med RSA/DSA Open SSH-nycklar. Mer information finns i [SFTP-översikten](../../sources/connectors/cloud-storage/ftp-sftp.md) . |
| UX-förbättringar | Du kan aktivera datauppsättningen för [!DNL Profile] under dataöverföringsprocessen. Mer information finns i självstudiekursen om arbetsflöde [](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) för molnlagring. |

Mer information om källor finns i [Källöversikt](../../sources/home.md).