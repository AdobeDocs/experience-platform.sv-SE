---
title: Versionsinformation för Adobe Experience Platform
description: Den senaste versionsinformationen för Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 6ae54c1f3f06c8daaf7c0d36beb4d5884bc258eb
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 30 mars 2022**

Nya funktioner i Adobe Experience Platform:

- [Granskningsloggar](#audit-logs)

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Larm](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Query Service]](#query-service)
- [Källor](#sources)
<!-- - [Experience Data Model (XDM)](#xdm) -->

## Granskningsloggar {#audit-logs}

Med Experience Platform kan du granska användaraktivitet för olika tjänster och funktioner. Granskningsloggarna innehåller information om vem som gjorde vad och när.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Granskningsloggar för datauppsättning, schema, klass, fältgrupp, datatyp, sandlåda, mål, segment, sammanfogningsprincip, beräknat attribut, produktprofil och konto (Adobe) | Detta är de resurser som registreras av granskningsloggar. Om funktionen är aktiverad samlas granskningsloggarna automatiskt in när aktiviteten inträffar. Du behöver inte aktivera loggsamling manuellt. |
| Exportera granskningsloggar | Granskningsloggarna kan hämtas som en `CSV` eller `JSON` -fil. De genererade filerna sparas direkt på datorn. |

{style=&quot;table-layout:auto&quot;}

Mer information om granskningsloggar i Platform finns i [granskningsloggar - översikt](../../landing/governance-privacy-security/audit-logs/overview.md).

## Larm {#alerts}

Med Experience Platform kan du prenumerera på händelsebaserade aviseringar för olika plattformsaktiviteter. Du kan prenumerera på olika varningsregler via [!UICONTROL Alerts] -fliken i användargränssnittet för plattformen och kan välja att ta emot varningsmeddelanden i själva användargränssnittet eller via e-postmeddelanden.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nya varningsregler | Det finns nu två nya varningsregler för källor som rör dataöverföring. Se översikten på [varningsregler](../../observability/alerts/rules.md) för den uppdaterade listan över varningstyper. |

{style=&quot;table-layout:auto&quot;}

Mer information om varningar i Platform finns i [varningsöversikt](../../observability/alerts/overview.md).

## Kontrollpaneler {#dashboards}

Adobe Experience Platform erbjuder flera [!DNL dashboards] genom vilken ni kan visa viktig information om organisationens data, som de har hämtats in under dagliga ögonblicksbilder.

### Profilinstrumentpaneler

På profilpanelen visas en ögonblicksbild av attributdata (postdata) som din organisation har i profilarkivet i Experience Platform.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Widgeten Osegmenterade profiler | Widgeten visar det totala antalet profiler som inte är kopplade till något segment. Det genererade numret är korrekt vid den senaste ögonblicksbilden och representerar möjligheten till profilaktivering i hela organisationen. Se [profiler standarddokumentation för widgetar](../../dashboards/guides/profiles.md#standard-widgets) för mer information. |
| widgeten Trend för osegmenterade profiler | Den här widgeten innehåller en illustration av linjediagram för antalet profiler som inte är kopplade till något segment under en viss tidsperiod. Trenden kan visualiseras under 30 dagar, 90 dagar och 12 månader. Se [profiler standarddokumentation för widgetar](../../dashboards/guides/profiles.md#standard-widgets) för mer information. |
| Osegmenterade profiler efter identitetswidget | Den här widgeten kategoriserar det totala antalet osegmenterade profiler efter deras unika identifierare. Data visas i ett stapeldiagram. Se [profiler standarddokumentation för widgetar](../../dashboards/guides/profiles.md#standard-widgets) för mer information. |
| widgeten Enstaka identitetsprofiler | Den här widgeten innehåller information om organisationens profiler som bara har en typ av ID som skapar deras identitet, antingen ett e-postmeddelande eller ett ECID. Se [profiler standarddokumentation för widgetar](../../dashboards/guides/profiles.md#standard-widgets) för mer information. |

{style=&quot;table-layout:auto&quot;}

Mer information om profilpaneler finns i [Översikt över kontrollpaneler för profiler](../../dashboards/guides/profiles.md).

### Destinationspaneler

På kontrollpanelen Destinationer visas en ögonblicksbild av de destinationer som din organisation har aktiverat i Experience Platform.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Widgeten Antal destinationer | Widgeten visar totalt antal tillgängliga slutpunkter där en målgrupp kan aktiveras och levereras inom systemet. Detta nummer inkluderar både aktiva och inaktiva mål. Se [dokumentation för standardwidget](../../dashboards/guides/destinations.md#standard-widgets) för mer information. |

{style=&quot;table-layout:auto&quot;}

Mer information om kontrollpaneler för destinationer i plattformen finns i [Översikt över kontrollpaneler för destinationer](../../dashboards/guides/destinations.md).

<!-- ## Experience Data Model (XDM) {#xdm}

Experience Data Model (XDM) is an open-source specification that provides common structures and definitions (schemas) for data that is brought into Adobe Experience Platform. By adhering to XDM standards, all customer experience data can be incorporated into a common representation to deliver insights in a faster, more integrated way. You can gain valuable insights from customer actions, define customer audiences through segments, and use customer attributes for personalization purposes.

| Feature | Description |
| --- | --- |
| Add or remove individual standard fields for a schema | The Schema Editor UI now allows you to add portions of standard field groups to your schemas, providing more flexibility for the fields you choose to include without needing to build custom resources from scratch.<br><br>You can now also define ad-hoc custom fields directly within the schema structure and assign them to a new or existing custom field group without needing to create or edit the field group beforehand.<br><br>See the guide on [creating and editing schemas in the UI](../../xdm/ui/resources/schemas.md) for more information on these new workflows. |

{style="table-layout:auto"}

For more information on XDM in Platform, see the [XDM System overview](../../xdm/home.md). -->

## Frågetjänst {#query-service}

[!DNL Query Service] låter dig använda standard-SQL för att fråga efter data i Adobe Experience Platform [!DNL Data Lake]. Du kan koppla alla datauppsättningar från [!DNL Data Lake] och samla in frågeresultaten som en ny datauppsättning som kan användas för rapportering, datavetenskapen eller för förtäring i kundprofilen i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| `table_exists` | Det nya funktionskommandot används för att bekräfta om det finns en tabell eller inte i systemet. Kommandot returnerar ett booleskt värde: `true` om tabellen **gör** finns, och `false` om tabellen **not** finns. Se [SQL-syntaxdokumentation](../../query-service/sql/syntax.md) för mer information. |

{style=&quot;table-layout:auto&quot;}

Mer information om tillgängliga funktioner finns i [Översikt över frågetjänsten](../../query-service/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera datainmatning genom hela processen.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nu finns nya källor för B2B-användning | Du kan nu använda alla tillgängliga källor på plattformen för B2B-användning. Se [källkatalog](../../sources/home.md) för en fullständig lista över tillgängliga källor. |
| Allmän tillgänglighet för nya [!DNL Oracle Eloqua] källa | Nu kan du använda [!DNL Oracle Eloqua] källa till smidig import av data från [!DNL Oracle Eloqua] -instans (konto, kampanj, kontakter) till Platform. Läs dokumentationen om [skapa [!DNL Oracle Eloqua] källanslutning](../../sources/connectors/marketing-automation/oracle-eloqua.md) för mer information. |
| API-förbättringar för [!DNL Data Landing Zone] | The [!DNL Data Landing Zone] -källan har nu stöd för automatisk identifiering av filegenskaper när du använder [!DNL Flow Service] API. Läs dokumentationen om [skapa [!DNL Data Landing Zone] källanslutning](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) för mer information. |

{style=&quot;table-layout:auto&quot;}

Mer information om källor finns i [källöversikt](../../sources/home.md).
