---
title: Versionsinformation för Adobe Experience Platform
description: Den senaste versionsinformationen för Adobe Experience Platform.
source-git-commit: f4e9750685d641c83b4ceed79af739de43343aef
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 27 oktober 2021**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [Källor](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] gör det möjligt för datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| `contains_key` funktion | The `contains_key` -funktionen har introducerats, vilket gör att du kan kontrollera om objektet finns i källan. Den här funktionen ersätter `is_set` som nu är föråldrad. |
| Felmeddelanden | Felmeddelanden som returneras av `/mappingSets/preview` Slutpunkten i API:t för dataförberedelser är nu konsekvent med de felmeddelanden som genereras under körning. |

Se [[!DNL Data Prep] översikt](../../data-prep/home.md) om du vill veta mer om den här tjänsten.

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

| Funktion | Beskrivning |
| --- | --- |
| [!DNL Amazon S3] källförbättringar | Nu kan du använda `s3SessionToken` för att ansluta [!DNL Amazon S3] konto till plattformen med temporära säkerhetsuppgifter. Med den här variabeln kan du ge kortvarig, tillfällig åtkomst till din [!DNL Amazon S3] för användare i miljöer som inte är betrodda. Se [[!DNL Amazon S3] dokumentation](../../sources/connectors/cloud-storage/s3.md#prerequisites) för mer information. |
| [!DNL Generic REST API] (Beta) | Nu kan du skapa en [!DNL Generic REST API] källanslutning med [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) eller [användargränssnitt](../../sources/tutorials/ui/create/protocols/generic-rest.md) för att hämta data från en generisk REST-applikation till Platform. Se [[!DNL Generic REST API] översikt](../../sources/connectors/protocols/generic-rest.md) för mer information. |
| [!DNL Zoho CRM] (Beta) | Nu kan du skapa en [!DNL Zoho CRM] källanslutning med [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) eller [användargränssnitt](../../sources/tutorials/ui/create/crm/zoho.md) för att hämta data från [!DNL Zoho CRM] konto till plattform. Se [[!DNL Zoho CRM] översikt](../../sources/connectors/crm/zoho.md) för mer information. |

Mer information om källor finns i [källöversikt](../../sources/home.md).
