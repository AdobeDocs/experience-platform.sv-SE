---
title: Versionsinformation om Adobe Experience Platform mars 2022
description: Versionsinformation mars 2022 för Adobe Experience Platform.
exl-id: 0d499aa6-e25d-4d34-ad32-5e4ab361cba1
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 2%

---

# Versionsinformation för Adobe Experience Platform

**Releasedatum: 30 mars 2022**

Nya funktioner i Adobe Experience Platform:

- [Granskningsloggar](#audit-logs)
- [Relaterade konton i Real-Time CDP B2B Edition](#related-accounts)

Uppdateringar av befintliga funktioner i Adobe Experience Platform:

- [Larm](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [Datainsamling](#data-collection)
- [[!DNL Query Service]](#query-service)
- [Källor](#sources)

## Granskningsloggar {#audit-logs}

Med Experience Platform kan du granska användaraktivitet för olika tjänster och funktioner. Granskningsloggarna innehåller information om vem som gjorde vad och när.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Granskningsloggar för datauppsättning, schema, klass, fältgrupp, datatyp, sandlåda, mål, segment, sammanfogningsprincip, beräknat attribut, produktprofil och konto (Adobe) | Detta är de resurser som registreras av granskningsloggar. Om funktionen är aktiverad samlas granskningsloggarna automatiskt in när aktiviteten inträffar. Du behöver inte aktivera loggsamling manuellt. |
| Exportera granskningsloggar | Granskningsloggarna kan hämtas som en `CSV` eller `JSON` -fil. De genererade filerna sparas direkt på datorn. |

{style="table-layout:auto"}

Mer information om granskningsloggar i Platform finns i [granskningsloggar - översikt](../../landing/governance-privacy-security/audit-logs/overview.md).

## Relaterade konton i Real-Time CDP B2B Edition {#related-accounts}

>[!NOTE]
>
>Funktionen för relaterade konton är endast tillgänglig för kunder som har Real-Time CDP B2B Edition.

B2B-företag har ofta sin kundinformation lagrad i flera system, där alla bara innehåller partiella eller till och med motstridiga data för samma verkliga affärsenhet. Detta skapar en stor utmaning i att få en korrekt bild av kunderna och minskar därmed effektiviteten och effektiviteten i B2B-marknadsförings- och säljsatsningarna. Med frisläppandet av relaterade konton [!DNL Real-Time CDP B2B] visar nu en lista över konton som liknar det konto du bläddrar i. Du kan inkludera de relaterade kontona i dina segmentdefinitioner för att bredda din räckvidd eller tillämpa fler kriterier i dina segment.

Läs mer om funktionen på följande dokumentationssidor:

- [Samhörande konton i Real-Time CDP B2B Edition - översikt](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [Fliken Relaterade konton i gränssnittsguiden för kontoprofiler](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [Så här använder du relaterade konton i segmentdefinitioner](../../rtcdp/segmentation/b2b.md#related-accounts)

Mer information om Real-Time CDP B2B Edition finns i [översikt](../../rtcdp/overview.md).

## Larm {#alerts}

Med Experience Platform kan du prenumerera på händelsebaserade aviseringar för olika plattformsaktiviteter. Du kan prenumerera på olika varningsregler via [!UICONTROL Alerts] -fliken i användargränssnittet för plattformen och kan välja att ta emot varningsmeddelanden i själva användargränssnittet eller via e-postmeddelanden.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nya varningsregler | Det finns nu två nya varningsregler för källor som rör dataöverföring. Se översikten på [varningsregler](../../observability/alerts/rules.md) för den uppdaterade listan över varningstyper. |

{style="table-layout:auto"}

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

{style="table-layout:auto"}

Mer information om profilpaneler finns i [Översikt över kontrollpaneler för profiler](../../dashboards/guides/profiles.md).

### Destinationspaneler

På kontrollpanelen Destinationer visas en ögonblicksbild av de destinationer som din organisation har aktiverat i Experience Platform.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Widgeten Antal destinationer | Widgeten visar totalt antal tillgängliga slutpunkter där en målgrupp kan aktiveras och levereras inom systemet. Detta nummer inkluderar både aktiva och inaktiva mål. Se [dokumentation för standardwidget](../../dashboards/guides/destinations.md#standard-widgets) för mer information. |

{style="table-layout:auto"}

Mer information om kontrollpaneler för destinationer i plattformen finns i [Översikt över kontrollpaneler för destinationer](../../dashboards/guides/destinations.md).

## Datainsamling {#data-collection}

Plattformen innehåller en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till Adobe eller andra destinationer än Adobe.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Globala datastream-inställningar | Du kan nu konfigurera flera nya globala inställningar när du konfigurerar ett datastream: geo location, first-party ID cookie, and third-party ID sync. Se avsnittet om [konfigurera ett datastream](../../edge/datastreams/overview.md#create) i användargränssnittsguiden för datastreams om du vill ha mer information. |
| [Server-API för Edge Network](../../server-api/overview.md) | Server-API:t gör det möjligt för kunder att interagera med Experience Platform Edge Network med en ny autentiserad slutpunkt som stöder en rad olika fall av datainsamling, personalisering, annonsering och marknadsföring. |

Mer information om datainsamling i Platform finns i [datainsamling - översikt](../../collection/home.md).

## Frågetjänst {#query-service}

[!DNL Query Service] låter dig använda standard-SQL för att fråga efter data i Adobe Experience Platform [!DNL Data Lake]. Du kan koppla alla datauppsättningar från [!DNL Data Lake] och samla in frågeresultaten som en ny datauppsättning som kan användas för rapportering, datavetenskapen eller för förtäring i kundprofilen i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| `table_exists` | Det nya funktionskommandot används för att bekräfta om det finns en tabell eller inte i systemet. Kommandot returnerar ett booleskt värde: `true` om tabellen **gör** finns, och `false` om tabellen **not** finns. Se [SQL-syntaxdokumentation](../../query-service/sql/syntax.md) för mer information. |

{style="table-layout:auto"}

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

{style="table-layout:auto"}

Mer information om källor finns i [källöversikt](../../sources/home.md).
