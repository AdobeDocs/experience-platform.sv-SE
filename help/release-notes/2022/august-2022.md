---
title: Versionsinformation om Adobe Experience Platform, augusti 2022
description: Versionsinformation från augusti 2022 för Adobe Experience Platform.
source-git-commit: 925991d58c3cdd84e13b12a095e9681b8f4b254b
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 1%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 24 augusti 2022**

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Dataprep](#data-prep)
- [Experience Data Model (XDM)](#xdm)
- [Källor](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] gör det möjligt för datatekniker att mappa, omvandla och validera data till och från Experience Data Model (XDM).

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Stöd för inmatning av poster med varningar | Dataprep lokaliserar nu varningar (icke-kritiska fel) till fälten och tillåter att resten av raden importeras. Alla mappningsomformningsfel rapporteras nu som varningar och rader som är delvis inkapslade betraktas som lyckade, med en varning.  Övervakning stöds även för poster med varningar och diagnostikinformation. Det går för närvarande bara att få del av poster med varningar att strömma data. Läs dokumentationen om [importera poster med varningar](../../sources/tutorials/ui/monitor-streaming.md) för mer information. |

{style=&quot;table-layout:auto&quot;}

Mer information om [!DNL Data Prep], se [[!DNL Data Prep] översikt](../../data-prep/home.md).

## Experience Data Model (XDM) {#xdm}

XDM är en öppen källkodsspecifikation som innehåller gemensamma strukturer och definitioner (scheman) för data som hämtas till Adobe Experience Platform. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation för att ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och använda kundattribut i personaliseringssyfte.

**Nya XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Globalt schema | [[!UICONTROL AJO Entity Schema]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity.schema.json) | Beskriver normaliserade enheter för Adobe Journey Optimizer. |
| Klass | [[!UICONTROL AJO Execution Entities]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-execution-entity.schema.json) | Beskriver Adobe Journey Optimizer exekveringsenheter som kan användas i segmentering. |
| Fältgrupp | [[!UICONTROL Workfront Work Objects]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | En omslutningsfältgrupp som refererar till alla objektspecifika fältgrupper på den lägre nivån för Adobe Workfront. |

{style=&quot;table-layout:auto&quot;}

**Uppdaterade XDM-komponenter**

| Komponenttyp | Namn | Beskrivning |
| --- | --- | --- |
| Fältgrupp | [[!UICONTROL Journey Orchestration Step Event Common Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Två nya egenskaper har lagts till: `origTimeStamp` och `experienceID`. |
| Fältgrupp | [[!UICONTROL Segment Membership Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | Förutom [!UICONTROL XDM Individual Profile]kan den här fältgruppen nu även användas i scheman som baseras på klassen XDM Business Account. |
| Fältgrupp | (Flera) | Flera fältgrupper som rör Marketo B2B-aktiviteter har uppdaterats till stabil status. Se följande [pull-förfrågan](https://github.com/adobe/xdm/pull/1593/files) för mer information. |
| Fältgrupp | (Flera) | Flera väderrelaterade fältgrupper har uppdaterats för att åtgärda fel som uppstod i `uvIndex` och `sunsetTime`. Se följande [pull-förfrågan](https://github.com/adobe/xdm/pull/1602/files) för mer information. |
| Datatyp | [[!UICONTROL Product list item]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | En ny egenskap `productImageUrl` har lagts till. |
| Datatyp | [[!UICONTROL Qoe Data details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | En ny egenskap `framesPerSecond` har lagts till. |
| Datatyp | [[!UICONTROL Session details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion` har bytt namn till `appVersion`. `meta:enum` och `description` fält har också uppdaterats. |
| Datatyper och fältgrupper | (Flera) | Flera mediedatatyper och fältgrupper har nya fält och uppdaterade beskrivningar. Se följande [pull-förfrågan](https://github.com/adobe/xdm/pull/1582/files) för mer information. |
| (Alla) | (Flera) | Alla schemaobjekt som innehåller `enum` fältet innehåller nu även en motsvarande `meta:enum` fält för att ange visningsvärden för varje begränsning. Se följande [pull-förfrågan](https://github.com/adobe/xdm/pull/1601/files) för mer information. |

{style=&quot;table-layout:auto&quot;}

Mer information om XDM i Platform finns i [XDM - systemöversikt](../../xdm/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera dataöverföringshastigheter.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Allmän tillgänglighet för självbetjäningskällor (batch-SDK) | Utveckla, testa och integrera REST API-baserade datakällor för att importera batchdata till Experience Platform med hjälp av lättkonfigurerade källspecifikationer. Med Sources SDK kan du: <ul><li>Konfigurera en ny källa till Experience Platform-katalogen.</li><li>Definiera specifikationer för källan, inklusive information om vilka autentiseringstyper som stöds, schemaläggning och hur resursdata hämtas.</li><li>Skapa användarinriktad dokumentation för den nya källan.</li></ul> Mer information finns i dokumentationen om [Självbetjänade källor (batch-SDK)](../../sources/sources-sdk/overview.md). |
| Allmän tillgänglighet för [!DNL Google BigQuery] källa | Använd [!DNL Google BigQuery] källa att importera data från [!DNL Google BigQuery] data warehouse till Experience Platform. Mer information finns i dokumentationen för [[!DNL Google BigQuery] källa](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] källa (beta) | Använd [!DNL Teradata Vantage] källa till import av data från hybridmiljöer med flera moln till Experience Platform. Mer information finns i dokumentationen för [[!DNL Teradata Vantage] källa](../../sources/connectors/databases/teradata-vantage.md). |
| Stöd för olika regioner för Adobe Analytics | Du kan nu importera rapportsviter från valfri region (USA, Storbritannien eller Singapore). Rapportsviterna måste mappas till samma organisation som den Experience Platform Sandbox-instans i vilken källanslutningen skapas. Mer information finns i guiden [skapa en Adobe Analytics-källanslutning i användargränssnittet](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| API-stöd för on-demand-inmatning | Använd on-demand-inmatning för att skapa ad hoc-flöden för ett givet dataflöde med [!DNL Flow Service] API. Skapade flödeskörningar måste anges som engångsintag. Mer information finns i guiden [skapa en flödeskörning för on-demand-inmatning med API](../../sources/tutorials/api/on-demand-ingestion.md) för mer information. |

{style=&quot;table-layout:auto&quot;}

Mer information om källor finns i [källöversikt](../../sources/home.md).
