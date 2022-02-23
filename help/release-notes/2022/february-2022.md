---
title: Versionsinformation för Adobe Experience Platform
description: Den senaste versionsinformationen för Adobe Experience Platform.
source-git-commit: 07dc417cbeb5ac0a59d2405986e9bb771b0735f2
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 23 februari 2022**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Datainsamling](#data-collection)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Identity Service]](#identity)
- [Källor](#sources)

## Datainsamling {#data-collection}

Plattformen innehåller en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Förbättrat gränssnittsarbetsflöde för datastream-konfiguration | Arbetsflödet för att skapa en ny datastam i användargränssnittet för datainsamling har uppdaterats. När du lägger till tjänster i ett dataflöde inkluderas endast de tjänster som du har tillgång till i listan med alternativ. Se guiden [konfigurera ett datastream](../../edge/fundamentals/datastreams.md) för mer information. |
| Dataförberedelse för datainsamling | Om du använder Adobe Experience Platform Web SDK kan du nu utnyttja funktionerna för dataförberedelser för att mappa dina data till Experience Data Model (XDM) på serversidan. Se avsnittet om [Dataförberedelse för datainsamling](../../edge/fundamentals/datastreams.md#data-prep) i datastreams-guiden om du vill ha mer information. |
| Enhets-ID:n från första part | Nu kan du skicka dina egna enhets-ID:n till Adobe Experience Platform Edge Network när du samlar in kunddata med Platform Web SDK, vilket ger en lösning för de senaste webbläsarbegränsningarna för cookie-intervall från tredje part. Se guiden [enhets-ID:n från första part](../../edge/identity/first-party-device-ids.md) för mer information. |

Mer information om datainsamling i Platform finns i [datainsamling - översikt](../../collection/home.md).


## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] gör det möjligt för datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| [!DNL Data Prep] stöd för Adobe Analytics källanslutning | Adobe Analytics-källkopplingen har nu stöd för dataprep-funktioner, vilket gör att du kan mappa dina data i Analytics-rapportsviten till ett mål-XDM-schema när du skapar ett dataflöde. Se självstudiekursen om [skapa en Analytics-källkoppling](../../sources/tutorials/ui/create/adobe-applications/analytics.md) för mer information. |

Mer information om [!DNL Data Prep], se [[!DNL Data Prep] översikt](../../data-prep/home.md).

## [!DNL Identity Service] {#identity}

För att kunna leverera relevanta digitala upplevelser måste ni ha en fullständig förståelse för era kunder. Detta blir svårare när era kunddata fragmenteras över olika system, vilket gör att varje enskild kund ser ut att ha flera&quot;identiteter&quot;.

Adobe Experience Platform [!DNL Identity Service] hjälper er att få en bättre bild av era kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Ny behörighet för `view-identity-graph` | Nu kan du använda `view-identity-graph` behörighet att kontrollera om användare i organisationen kan visa data i identitetsdiagram. Användare utan denna behörighet tillåts inte att komma åt identitetsdiagramvisningsprogrammet i användargränssnittet eller vid åtkomst [!DNL Identity Service] API:er som returnerar identiteter. Se [åtkomstkontroll - översikt](../../access-control/home.md) för mer information om behörigheter. |

Mer allmän information om [!DNL Identity Service], se [Översikt över identitetstjänsten](../../identity-service/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

| Funktion | Beskrivning |
| --- | --- |
| Beta-källor som går över till GA | Följande källor har befordrats från beta till GA: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

Mer information om källor finns i [källöversikt](../../sources/home.md).
