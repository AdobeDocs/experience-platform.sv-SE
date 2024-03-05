---
title: Versionsinformation om Adobe Experience Platform, februari 2022
description: Versionsinformation från februari 2022 för Adobe Experience Platform.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 1%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 7 mars 2022**

>[!NOTE]
>
>Den här versionen ändrades från det ursprungliga datumet 23 februari till 7 mars.

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data collection]](#data-collection)
- [[!DNL Destinations]](#destinations)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform erbjuder flera [!DNL dashboards] genom vilka ni kan få viktiga insikter om organisationens data, som de har fångats in under dagliga ögonblicksbilder.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nya widgetar för standarddestinationer | Med följande standardwidgetar kan du visualisera olika mätvärden för dina destinationer.<ul><li>Nyligen aktiverade segment efter mål. Den här widgeten visar de fem senast aktiverade segmenten i fallande ordning enligt det valda målet.</li><li>Storlekstrend för målgruppen. Den här widgeten visar relationen mellan profilantalet under en tidsperiod för ett segment som har mappats till det målkontot.</li><li>Omappade segment efter identitet. Den här widgeten visar de fem viktigaste omappade segmenten som rangordnats av fallande identitetsantal för ett visst mål och en viss identitet.</li><li>Mappade segment efter identitet. Den här widgeten visar de fem viktigaste mappade segmenten. Segmenten ordnas från hög till låg enligt deras respektive antal käll-ID:n som matchar det mål-ID som valts i widgetens listruta.</li><li>Gemensamma målgrupper. Den här widgeten innehåller en lista över de fem översta segment som är aktiverade över målkontot, som är valt längst upp på sidan, och det mål som är markerat i widgetens listruta.</li></ul> Mer information om tillgängliga standardwidgetar finns i [dokumentation för kontrollpanelen för destinationer.](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#standard-widgets). |

Mer information om [!DNL Dashboards], se [[!DNL Dashboards] översikt](../../dashboards/home.md).

## Datainsamling {#data-collection}

Plattformen innehåller en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Förbättrat gränssnittsarbetsflöde för datastream-konfiguration | Arbetsflödet för att skapa en ny datastam i användargränssnittet för datainsamling har uppdaterats. När du lägger till tjänster i ett dataflöde inkluderas endast de tjänster som du har tillgång till i listan med alternativ. Se guiden på [konfigurera ett datastream](../../datastreams/overview.md) för mer information. |
| Dataförberedelse för datainsamling | Om du använder Adobe Experience Platform Web SDK kan du nu utnyttja funktionerna för dataförberedelser för att mappa dina data till Experience Data Model (XDM) på serversidan. Se avsnittet om [Dataförberedelse för datainsamling](../../datastreams/data-prep.md) i datastreams-guiden om du vill ha mer information. |
| Enhets-ID:n från första part | Nu kan du skicka dina egna enhets-ID:n till Adobe Experience Platform Edge Network när du samlar in kunddata med Platform Web SDK, vilket ger en lösning för de senaste webbläsarbegränsningarna för cookie-intervall från tredje part. Se guiden på [enhets-ID:n från första part](../../web-sdk/identity/first-party-device-ids.md) för mer information. |

Mer information om datainsamling i Platform finns i [datainsamling - översikt](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| ----------- | ----------- |
| (Beta) Destination SDK support för filbaserade mål | [Stöd för Destination SDK för filbaserade mål](../../destinations/destination-sdk/functionality/destination-server/server-specs.md) är för närvarande i en privat betaversion och är endast tillgängligt för ett visst antal partners och kunder. Funktionerna och tillhörande dokumentation kan ändras före den allmänna tillgänglighetsversionen.<br><br>Kontakta din kontorepresentant på Adobe om du vill veta hur du får tillgång till funktionen. Företrädare för Adobe-interna konton bör vända sig till Experience Platform för att få kontakt med produkts- och konstruktionsgrupper för att diskutera vilka användningsområden som stöds. <br><br> I betaversionen av Destination SDK-support för filbaserade destinationer kan betatestare och -kunder använda [Experience Platform Destination SDK](../../destinations/destination-sdk/overview.md) för att bygga privata destinationer och få tillgång till följande funktionalitet: <ul><li>Skapa en filbaserad (batch) destination via Amazon S3, SFTP-servrar, Azure Blob, Azure Data Lake Storage, Data Landing Zone-lagring.</li><li>Konfigurera och ange standardalternativ för schemaläggning och frekvens för filexport.</li><li>Konfigurera och ange alternativ för att formatera de exporterade CSV-filerna (avgränsare, escape-tecken och andra alternativ).</li><li>Möjlighet att ange och redigera anpassade filhuvuden.</li><li>Möjlighet att få händelseaviseringar om export av filer och segment.</li><li>Möjlighet att exportera ytterligare filtyper som CSV, TSV, JSON, Parquet.</li></ul>  <br>Om du vill komma igång med de nya funktionerna läser du [(Beta) Använd Destination SDK för att konfigurera ett filbaserat mål](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md). <br><br> Funktionen för att skapa privata eller producerade *direktuppspelning* destinationer genom att använda Destination SDK är redan tillgängliga för alla kunder och partners i Experience Platform. Läs guiden om [använd Destination SDK för att konfigurera ett mål för direktuppspelning](../../destinations/destination-sdk/guides/configure-destination-instructions.md) för mer information. |

## [!DNL Identity Service] {#identity}

För att kunna leverera relevanta digitala upplevelser måste ni ha en fullständig förståelse för era kunder. Detta blir svårare när era kunddata fragmenteras över olika system, vilket gör att varje enskild kund ser ut att ha flera&quot;identiteter&quot;.

Adobe Experience Platform [!DNL Identity Service] hjälper er att få en bättre bild av era kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Ny behörighet för `view-identity-graph` | Nu kan du använda `view-identity-graph` behörighet att kontrollera om användare i organisationen kan visa data i identitetsdiagram. Användare utan denna behörighet tillåts inte att komma åt identitetsdiagramvisningsprogrammet i användargränssnittet eller vid åtkomst [!DNL Identity Service] API som returnerar identiteter. Se [åtkomstkontroll - översikt](../../access-control/home.md) för mer information om behörigheter. |

Mer allmän information om [!DNL Identity Service], se [Översikt över identitetstjänsten](../../identity-service/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Beta-källor som går över till GA | Följande källor har befordrats från beta till GA: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

Mer information om källor finns i [källöversikt](../../sources/home.md).