---
title: Versionsinformation för Adobe Experience Platform
description: Den senaste versionsinformationen för Adobe Experience Platform.
source-git-commit: d046c17a7b376f5c2e2f25c38fac0916ed2dba73
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 1%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 26 oktober 2022**

Nya funktioner i Adobe Experience Platform:

- [Kundhanterade nycklar](#cmk)

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Datainsamling](#data-collection)
- [Mål ](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Frågetjänst](#query-service)
- [Källor](#sources)

## Kundhanterade nycklar {#cmk}

Alla data som lagras på Adobe Experience Platform krypteras i viloläge med hjälp av nycklar på systemnivå. Om du använder ett program som är byggt på plattformen kan du nu välja att använda dina egna krypteringsnycklar istället, vilket ger dig större kontroll över datasäkerheten.

Se översikten på [kundhanterade nycklar](../../landing/governance-privacy-security/customer-managed-keys.md) om du vill ha mer information om funktionen.

## Datainsamling {#data-collection}

Adobe Experience Platform erbjuder en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Känslig datahantering för datastreams | Datastreams utnyttjar nu flera plattformstekniker för att hantera känsliga data på ett lämpligt sätt, i enlighet med bestämmelser som HIPAA (Health Insurance Portability and Accounability Act). Se avsnittet om [hantera känsliga data i dataströmmar](../../edge/datastreams/overview.md#sensitive) för mer information. |
| [!DNL Splunk] tillägg för händelsevidarebefordran | Nu kan du skicka data till [!DNL Splunk] med [händelsevidarebefordran](../../tags/ui/event-forwarding/overview.md) tillägg. Se [[!DNL Splunk] tilläggsöversikt](../../tags/extensions/web/splunk/overview.md) för mer information. |
| [!DNL Zendesk] tillägg för händelsevidarebefordran | Nu kan du skicka data till [!DNL Zendesk] med [händelsevidarebefordran](../../tags/ui/event-forwarding/overview.md) tillägg. Se [[!DNL Zendesk] tilläggsöversikt](../../tags/extensions/web/zendesk/overview.md) för mer information. |

{style=&quot;table-layout:auto&quot;}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| (Beta) Datauppsättningsexport | The [Datauppsättningen exporterar betafunktioner](/help/destinations/ui/export-datasets.md) gör att du kan exportera första generationens data (enligt definitionen i [Real-time Customer Data Platform produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)) från Adobe Experience Platform till era egna externa kundsystem via användargränssnittet. På så sätt kan du få ut data från Experience Platform med ett kodfritt/lågkodsarbetsflöde till sex molnlagringsmål (som anges i tabellen nedan) för analyser och efterlevnadsfall. |
| (Beta) Förbättrade funktioner för filexport | Nu kan du dra nytta av förbättrade anpassningsfunktioner när du exporterar filer från Experience Platform: <br><ul><li>Ytterligare [filnamnsalternativ](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).</li><li>Möjlighet att ange anpassade filhuvuden i de exporterade filerna via [förbättrat mappningssteg](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Möjlighet att anpassa formateringen i exporterade CSV-datafiler](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> <br> Den här funktionaliteten stöds av de sex nya betolymminneskorten i tabellen nedan. |

{style=&quot;table-layout:auto&quot;}

**Nya eller uppdaterade destinationer**

| Destination | Beskrivning |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | Line är en populär kommunikationsplattform som knyter samman människor, tjänster och information och har växt från en chattapp till ett nav för underhållning, sociala aktiviteter och dagliga aktiviteter. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365 är en molnbaserad plattform för affärsapplikationer som kombinerar ERP (Enterprise Resource Planning) och CRM (Customer Relationship Management) med produktivitetsapplikationer och AI-verktyg, vilket ger smidigare och mer kontrollerad drift, bättre tillväxtpotential och minskade kostnader. |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | The [!DNL (Beta) Adobe Commerce] med målanslutningen kan du välja ett eller flera Real-Time CDP-segment som ska aktiveras för [!DNL Adobe Commerce] för att leverera en dynamisk personaliserad upplevelse till era kunder. Inom [!DNL Adobe Commerce]kan du sedan välja de Real-Time CDP-segmenten för att personalisera unika erbjudanden i kundvagnen, till exempel&quot;köp 2 få 1 utan kostnad&quot;. Ni kan också visa hjältebanners och ändra produktpriserna med hjälp av kampanjerbjudanden som alla är anpassade efter Adobe Real-Time CDP segment. |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | Skapa en utgående liveanslutning till [!DNL Azure Data Lake Storage Gen2] att regelbundet exportera datafiler från Adobe Experience Platform till din egen lagringsplats. Det nya betaversionen ger bättre filexportfunktioner och stöder datauppsättningsexport. |
| [[!DNL (Beta) Azure Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone] är en [!DNL Azure Blob] lagringsgränssnittet som tillhandahålls av Adobe Experience Platform och ger dig tillgång till en säker, molnbaserad fillagringsfunktion för att exportera filer från plattformar. Det nya betaversionen ger bättre filexportfunktioner och stöder datauppsättningsexport. |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | Skapa en utgående liveanslutning till [!DNL Google Cloud Storage] att regelbundet exportera datafiler från Adobe Experience Platform till era egna fickor. Det nya betaversionen ger bättre filexportfunktioner och stöder datauppsättningsexport. |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Betatestare ser nu två [!DNL Amazon S3] destinationskort sida vid sida i målkatalogen. Det nya betaversionen ger utökade funktioner för filexport och stöder export av datauppsättningar. |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Betatestare ser nu två [!DNL Azure Blob] destinationskort sida vid sida i målkatalogen. Det nya betaversionen ger utökade funktioner för filexport och stöder export av datauppsättningar. |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Betatestare ser nu två [!DNL SFTP] destinationskort sida vid sida i målkatalogen. Det nya betaversionen ger utökade funktioner för filexport och stöder export av datauppsättningar. |

{style=&quot;table-layout:auto&quot;}

**Ny eller uppdaterad dokumentation**

| Dokumentation | Beskrivning |
| ----------- | ----------- |
| [Skyddsräcken för destinationer](../../destinations/guardrails.md) | Den här sidan innehåller standardvärden för användning och hastighetsbegränsningar för aktiveringsbeteende. |

Mer allmän information om destinationer finns i [destinationer, översikt](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Uppdaterade XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Datatyp | [[!UICONTROL Session details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Uppdaterade `authorized` fält från en boolesk typ till en sträng. `season` och `episode` har ändrats från heltal till strängar. |
| Datatyp | [[!UICONTROL Advertising details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` har bytt namn till `friendlyName`och `ID` har bytt namn till `name`. |
| Datatyp | [[!UICONTROL Error details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` har bytt namn till `name`. |

{style=&quot;table-layout:auto&quot;}

Mer information om XDM i Platform finns i [XDM - systemöversikt](../../xdm/home.md).

## Frågetjänst {#query-service}

Med frågetjänsten kan du använda standard-SQL för att fråga data i Adobe Experience Platform [!DNL Data Lake]. Du kan koppla alla datauppsättningar från [!DNL Data Lake] och samla in frågeresultaten som en ny datauppsättning som kan användas för rapportering, datavetenskapen eller för förtäring i kundprofilen i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Övervaka frågor via plattformsgränssnittet | Frågetjänsten [!UICONTROL Scheduled Queries] -fliken ger förbättrad synlighet för statusen för alla frågejobb via gränssnittet. Du kan nu hitta viktig information om status för dina frågekörningar, inklusive felmeddelanden och koder om de misslyckas, från [!UICONTROL Scheduled Queries] -fliken. Du kan även prenumerera på aviseringar via användargränssnittet för dessa frågor baserat på deras status. Se [Övervaka frågedokument](../../query-service/monitor-queries.md) om du vill veta mer om den här funktionen. |
| Frågeaccelererad datamodell för rapportinsikter | Som en del av Data Distiller SKU kan du med hjälp av det frågeaccelererade arkivet minska den tid och processorkraft som krävs för att få viktiga insikter från dina data. Med det förbättrade arkivet kan ni skapa en anpassad datamodell och/eller utöka den med befintliga Adobe Real-time Customer Data Platform datamodeller för att förbättra era rapportinsikter och deras visualiseringar. Se [frågerapport för rapporter i butiker - dokument](../../query-service/query-accelerated-store/reporting-insights-data-model.md) om du vill veta mer om den här funktionen. |

{style=&quot;table-layout:auto&quot;}

Mer information om frågetjänster finns i [Översikt över frågetjänsten](../../query-service/home.md).
Nya funktioner i Adobe Experience Platform:

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- | 
| Tillgänglighet för betaversion av Adobe Workfront-källa | Använd [Adobe Workfront-källa](../../sources/connectors/adobe-applications/workfront.md) för att ta med dina Workfront-data till Experience Platform och utföra användningsexempel som att kombinera dina arbetsdata med data från tredje part, använda historik- och tidsserieanalyser på arbetsregistreringar och fråga arbetsdata med standard-SQL. Mer information finns i guiden [skapa en Workfront-källanslutning i användargränssnittet](../../sources/tutorials/ui/create/adobe-applications/workfront.md). |
| Betaversion av Oraclets Service Cloud-källa | Använd Oraclets Service Cloud-källa för att importera data från ditt Oracle Service Cloud-konto till Experience Platform. Mer information finns i dokumentationen för [Oracle Service Cloud-källa](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Läs mer om källor i [källöversikt](../../sources/home.md).
