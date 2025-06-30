---
title: Versionsinformation om Adobe Experience Platform oktober 2021
description: Versionsinformationen för Adobe Experience Platform i oktober 2021.
exl-id: 8f8bcb24-6478-4281-9362-9559158384af
source-git-commit: 2e41a1716e057cd33e4635c11ba9c3cfc185418a
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 18%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 27 oktober 2021**

## Uppdateringar till Experience Platform

Uppdateringar till Experience Platform.

### Användargränssnitt {#ui}

Användargränssnittet har uppdaterats med följande ändringar:

| Funktion | Beskrivning |
| --- | --- |
| Mörkt tema | Använd den mörka temagränsen för att växla mellan ljusa och mörka teman i Experience Platform gränssnitt. Växeln finns i användarprofilen under användarnamnet och e-postadressen. |
| Växla vänster navigering | Använd det förbättrade navigeringsreglaget längst upp i programhuvudet för att visa eller dölja menyn som visar dina Experience Platform-funktioner. Systemet kommer ihåg ditt senaste val och visar bara de funktioner du har tillgång till. |
| Åtkomstsynlighet | I det vänstra navigeringsfältet visas bara de funktioner som du har tillgång till. I tidigare versioner av Adobe Experience Platform var otillgängliga objekt synliga, även om du inte kunde komma åt dem. |

Mer information finns i [Experience Platform användargränssnittshandbok](../../landing/ui-guide.md).

## Uppdateringar av befintliga funktioner

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [Källor](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] tillåter datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Funktionen `contains_key` | Funktionen `contains_key` har introducerats, vilket gör att du kan kontrollera om objektet finns i källan. Den här funktionen ersätter funktionen `is_set`, som nu är inaktuell. |
| Felmeddelanden | Felmeddelanden som returneras av `/mappingSets/preview`-slutpunkten i API:t för dataförberedelser är nu konsekventa med de felmeddelanden som genereras under körning. |

Mer information om den här tjänsten finns i [[!DNL Data Prep] översikten](../../data-prep/home.md).

### Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Med dessa källanslutningar kan du autentisera och ansluta till externa lagringssystem och CRM-tjänster, ställa in tider för inmatningskörningar och hantera datainmatningens genomströmning.

| Funktion | Beskrivning |
| --- | --- |
| [!DNL Amazon S3] källförbättringar | Du kan nu använda parametern `s3SessionToken` för att ansluta ditt [!DNL Amazon S3]-konto till Experience Platform med temporära säkerhetsuppgifter. Med den här variabeln kan du ge kortvarig, tillfällig åtkomst till dina [!DNL Amazon S3]-resurser för användare i miljöer som inte är betrodda. Mer information finns i [[!DNL Amazon S3] dokumentationen](../../sources/connectors/cloud-storage/s3.md#prerequisites). |
| [!DNL Generic REST API] (Beta) | Du kan nu skapa en [!DNL Generic REST API]-källanslutning med [[!DNL Flow Service]  API](../../sources/tutorials/api/create/protocols/generic-rest.md) för att hämta data från ett generiskt REST-program till Experience Platform. Mer information finns i [[!DNL Generic REST API] översikten](../../sources/connectors/protocols/generic-rest.md). |

Mer information om källor finns i [Källöversikt](../../sources/home.md).
