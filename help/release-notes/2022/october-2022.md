---
title: Versionsinformation om Adobe Experience Platform oktober 2022
description: Versionsinformationen för Adobe Experience Platform i oktober 2022.
exl-id: 61ef2472-5e79-433f-9f60-b1245f619b42
source-git-commit: 18c1d32bbc2732c38a9c37ee8fb9d36a23d4e515
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 26 oktober 2022**

- [Kundhanterade nycklar](#cmk)
- [Datainsamling](#data-collection)
- [Mål ](#destinations)
- [Experience Data Model](#xdm)
- [Frågetjänst](#query-service)

## Kundhanterade nycklar {#cmk}

Alla data som lagras på Adobe Experience Platform krypteras i viloläge med hjälp av nycklar på systemnivå. Om du använder ett program som är byggt på plattformen kan du nu välja att använda dina egna krypteringsnycklar istället, vilket ger dig större kontroll över datasäkerheten.

Mer information om funktionen finns i översikten om [kundhanterade nycklar](../../landing/governance-privacy-security/customer-managed-keys/overview.md).

## Datainsamling {#data-collection}

Adobe Experience Platform erbjuder en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Känslig datahantering för datastreams | Datastreams utnyttjar nu flera plattformstekniker för att hantera känsliga data på ett lämpligt sätt, i enlighet med bestämmelser som HIPAA (Health Insurance Portability and Accounability Act). Mer information finns i avsnittet [Hantera känsliga data i dataströmmar](../../datastreams/overview.md#sensitive). |
| [!DNL Splunk]-tillägg för händelsevidarebefordran | Du kan nu skicka data till [!DNL Splunk] med ett [vidarebefordrande](../../tags/ui/event-forwarding/overview.md)-tillägg. Mer information finns i [[!DNL Splunk] tilläggsöversikten](../../tags/extensions/server/splunk/overview.md). |
| [!DNL Zendesk]-tillägg för händelsevidarebefordran | Du kan nu skicka data till [!DNL Zendesk] med ett [vidarebefordrande](../../tags/ui/event-forwarding/overview.md)-tillägg. Mer information finns i [[!DNL Zendesk] tilläggsöversikten](../../tags/extensions/server/zendesk/overview.md). |

{style="table-layout:auto"}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] är färdiga integreringar med målplattformar som möjliggör smidig aktivering av data från Adobe Experience Platform. Ni kan använda destinationer för att aktivera kända och okända data för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

**Nya eller uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| (Beta) Export av datauppsättningar | [Datauppsättningen exporterar Beta-funktioner](/help/destinations/ui/export-datasets.md) så att du kan exportera första generationens data (enligt definitionen i [Real-time Customer Data Platform produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)) från Adobe Experience Platform till dina egna externa kundsystem via målanvändargränssnittet. På så sätt kan du få ut data från Experience Platform med ett kodfritt/lågkodsarbetsflöde till sex molnlagringsmål (som anges i tabellen nedan) för analyser och efterlevnadsfall. |
| (Beta) Förbättrade funktioner för filexport | Du kan nu dra nytta av den förbättrade anpassningsfunktionen när du exporterar filer från Experience Platform: <br><ul><li>Ytterligare [namngivningsalternativ](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).</li><li>Möjlighet att ange anpassade filhuvuden i de exporterade filerna via det [förbättrade mappningssteget](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Möjlighet att anpassa formateringen för exporterade CSV-datafiler](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> <br> Den här funktionen stöds av de sex nya betolymlagringskorten som visas i tabellen nedan. |

{style="table-layout:auto"}

**Nya eller uppdaterade mål** {#new-or-updated-destinations}

| Mål | Beskrivning |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | Line är en populär kommunikationsplattform som knyter samman människor, tjänster och information och har växt från en chattapp till ett nav för underhållning, sociala aktiviteter och dagliga aktiviteter. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365 är en molnbaserad plattform för affärsapplikationer som kombinerar ERP (Enterprise Resource Planning) och CRM (Customer Relationship Management) med produktivitetsapplikationer och AI-verktyg, vilket ger smidigare och mer kontrollerad drift, bättre tillväxtpotential och minskade kostnader. |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | Med [!DNL (Beta) Adobe Commerce]-målanslutningen kan du välja ett eller flera Real-Time CDP-segment som ska aktiveras för ditt [!DNL Adobe Commerce]-konto för att leverera en dynamisk, personlig upplevelse till era kunder. Inom [!DNL Adobe Commerce] kan du sedan välja de Real-Time CDP-segmenten för att anpassa unika erbjudanden i kundvagnen, till exempel&quot;köp 2 få 1 utan kostnad&quot;. Ni kan också visa hjältebanners och ändra produktpriserna med hjälp av kampanjerbjudanden som alla är anpassade efter Adobe Real-Time CDP segment. |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | Skapa en utgående liveanslutning till [!DNL Azure Data Lake Storage Gen2] för att regelbundet exportera datafiler från Adobe Experience Platform till din egen lagringsplats. Det nya betaversionen ger bättre filexportfunktioner och stöder datauppsättningsexport. |
| [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone] är ett [!DNL Azure Blob] lagringsgränssnitt som tillhandahålls av Adobe Experience Platform, vilket ger dig tillgång till en säker, molnbaserad fillagringsfunktion för att exportera filer från plattformen. Det nya betaversionen ger bättre filexportfunktioner och stöder datauppsättningsexport. |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | Skapa en utgående liveanslutning till [!DNL Google Cloud Storage] för att regelbundet exportera datafiler från Adobe Experience Platform till dina egna bucket. Det nya betaversionen ger bättre filexportfunktioner och stöder datauppsättningsexport. |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Beta-deltagare ser nu två [!DNL Amazon S3]-destinationskort sida vid sida i målkatalogen. Det nya betaversionen ger utökade funktioner för filexport och stöder export av datauppsättningar. |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Beta-deltagare ser nu två [!DNL Azure Blob]-destinationskort sida vid sida i målkatalogen. Det nya betaversionen ger utökade funktioner för filexport och stöder export av datauppsättningar. |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Beta-deltagare ser nu två [!DNL SFTP]-destinationskort sida vid sida i målkatalogen. Det nya betaversionen ger utökade funktioner för filexport och stöder export av datauppsättningar. |

{style="table-layout:auto"}

**Ny eller uppdaterad dokumentation**

| Dokumentation | Beskrivning |
| ----------- | ----------- |
| [Målskyddsräcken](../../destinations/guardrails.md) | Den här sidan innehåller standardvärden för användning och hastighetsbegränsningar för aktiveringsbeteende. |

Mer allmän information om destinationer finns i [målöversikten](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Uppdaterade XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Datatyp | [[!UICONTROL Session details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Fältet `authorized` har uppdaterats från en boolesk typ till en sträng. `season` och `episode` har ändrats från heltal till strängar. |
| Datatyp | [[!UICONTROL Advertising details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` har bytt namn till `friendlyName` och `ID` har bytt namn till `name`. |
| Datatyp | [[!UICONTROL Error details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` har bytt namn till `name`. |

{style="table-layout:auto"}

Mer information om XDM i Platform finns i [XDM-systemöversikt](../../xdm/home.md).

## Frågetjänst {#query-service}

Med frågetjänsten kan du använda standard-SQL för att fråga efter data i Adobe Experience Platform [!DNL Data Lake]. Du kan ansluta till alla datauppsättningar från [!DNL Data Lake] och samla in frågeresultaten som en ny datamängd som kan användas för rapportering, Data Science Workspace eller för förtäring i kundprofilen i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Övervaka frågor via plattformsgränssnittet | Fliken Frågetjänst [!UICONTROL Scheduled Queries] ger förbättrad synlighet för statusen för alla frågefunktioner via gränssnittet. Du kan nu hitta viktig information om status för dina frågekörningar, inklusive felmeddelanden och koder om de misslyckas, på fliken [!UICONTROL Scheduled Queries]. Du kan även prenumerera på aviseringar via användargränssnittet för dessa frågor baserat på deras status. Läs dokumentet [Övervaka frågor](../../query-service/ui/monitor-queries.md) om du vill veta mer om den här funktionen. |
| Frågeaccelererad datamodell för rapportinsikter | Som en del av Data Distiller SKU kan du med hjälp av det frågeaccelererade arkivet minska den tid och processorkraft som krävs för att få viktiga insikter från dina data. Med det förbättrade arkivet kan ni skapa en anpassad datamodell och/eller utöka den med befintliga Adobe Real-time Customer Data Platform datamodeller för att förbättra era rapportinsikter och deras visualiseringar. Läs dokumentet [med förbättrade rapportinsikter för arkiv](../../query-service/data-distiller/customizable-insights/reporting-insights-data-model.md) om du vill veta mer om den här funktionen. |

{style="table-layout:auto"}

Mer information om frågetjänster finns i [Översikt över frågetjänsten](../../query-service/home.md).
Nya funktioner i Adobe Experience Platform:

