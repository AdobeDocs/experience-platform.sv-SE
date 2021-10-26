---
title: Versionsinformation för Adobe Experience Platform
description: Den senaste versionsinformationen för Adobe Experience Platform.
source-git-commit: 0c507a26f551af1eb17889e8e77a036e3c106240
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 1%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 27 oktober 2021**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Källor](#sources)

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

| Funktion | Beskrivning |
| --- | --- |
| [!DNL Amazon S3] källförbättringar | Nu kan du använda `s3SessionToken` för att ansluta [!DNL Amazon S3] konto till plattformen med temporära säkerhetsuppgifter. Med den här variabeln kan du ge kortvarig, tillfällig åtkomst till din [!DNL Amazon S3] för användare i miljöer som inte är betrodda. Se [[!DNL Amazon S3] dokumentation](../../sources/connectors/cloud-storage/s3.md#prerequisites) för mer information. |
| [!DNL Generic REST API] (Beta) | Nu kan du skapa en [!DNL Generic REST API] källanslutning med [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) eller [användargränssnitt](../../sources/tutorials/ui/create/protocols/generic-rest.md) för att hämta data från en generisk REST-applikation till Platform. Se [[!DNL Generic REST API] översikt](../../sources/connectors/protocols/generic-rest.md) för mer information. |
| [!DNL Zoho CRM] (Beta) | Nu kan du skapa en [!DNL Zoho CRM] källanslutning med [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) eller [användargränssnitt](../../sources/tutorials/ui/create/crm/zoho.md) för att hämta data från [!DNL Zoho CRM] konto till plattform. Se [[!DNL Zoho CRM] översikt](../../sources/connectors/crm/zoho.md) för mer information. |

Mer information om källor finns i [källöversikt](../../sources/home.md).
