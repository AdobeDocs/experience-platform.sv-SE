---
title: Versionsinformation om Adobe Experience Platform mars 2022
description: Versionsinformationen för Adobe Experience Platform i mars 2022.
exl-id: 0d499aa6-e25d-4d34-ad32-5e4ab361cba1
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1171'
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
| Exportera granskningsloggar | Granskningsloggarna kan hämtas som en `CSV`- eller `JSON`-fil. De genererade filerna sparas direkt på datorn. |

{style="table-layout:auto"}

Mer information om granskningsloggar i Platform finns i [Översikt över granskningsloggar](../../landing/governance-privacy-security/audit-logs/overview.md).

## Relaterade konton i Real-Time CDP B2B Edition {#related-accounts}

>[!NOTE]
>
>Funktionen för relaterade konton är endast tillgänglig för kunder som har Real-Time CDP B2B Edition.

B2B-företag har ofta sin kundinformation lagrad i flera system, där alla bara innehåller partiella eller till och med motstridiga data för samma verkliga affärsenhet. Detta skapar en stor utmaning i att få en korrekt bild av kunderna och minskar därmed effektiviteten och effektiviteten i B2B-marknadsförings- och säljsatsningarna. I och med att relaterade konton har släppts visar [!DNL Real-Time CDP B2B] nu en lista över konton som liknar det konto du bläddrar i. Du kan inkludera de relaterade kontona i dina segmentdefinitioner för att bredda din räckvidd eller tillämpa fler kriterier i dina segment.

Läs mer om funktionen på följande dokumentationssidor:

- [Samhörande konton i Real-Time CDP B2B Edition - översikt](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [Fliken Relaterade konton i gränssnittsguiden för kontoprofiler](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [Så här använder du relaterade konton i segmentdefinitioner](../../rtcdp/segmentation/b2b.md#related-accounts)

Mer information om Real-Time CDP B2B Edition finns i [översikten](../../rtcdp/overview.md).

## Larm {#alerts}

Med Experience Platform kan du prenumerera på händelsebaserade aviseringar för olika plattformsaktiviteter. Du kan prenumerera på olika varningsregler via fliken [!UICONTROL Alerts] i användargränssnittet för plattformen och du kan välja att ta emot varningsmeddelanden i själva användargränssnittet eller via e-postmeddelanden.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nya varningsregler | Det finns nu två nya varningsregler för källor som rör dataöverföring. I översikten över [varningsregler](../../observability/alerts/rules.md) finns en uppdaterad lista över varningstyper. |

{style="table-layout:auto"}

Mer information om aviseringar i Platform finns i [varningsöversikten](../../observability/alerts/overview.md).

## Kontrollpaneler {#dashboards}

Adobe Experience Platform tillhandahåller flera [!DNL dashboards] som du kan använda för att visa viktig information om organisationens data, som de har hämtats under dagliga ögonblicksbilder.

### Profilinstrumentpaneler

På kontrollpanelen Profiler visas en ögonblicksbild av attributdata (postdata) som din organisation har i profilarkivet i Experience Platform.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Widgeten Osegmenterade profiler | Widgeten visar det totala antalet profiler som inte är kopplade till något segment. Det genererade numret är korrekt vid den senaste ögonblicksbilden och representerar möjligheten till profilaktivering i hela organisationen. Mer information finns i dokumentationen för [standardwidgetar](../../dashboards/guides/profiles.md#standard-widgets). |
| widgeten Trend för osegmenterade profiler | Den här widgeten innehåller en illustration av linjediagram för antalet profiler som inte är kopplade till något segment under en viss tidsperiod. Trenden kan visualiseras under 30 dagar, 90 dagar och 12 månader. Mer information finns i dokumentationen för [standardwidgetar](../../dashboards/guides/profiles.md#standard-widgets). |
| Osegmenterade profiler efter identitetswidget | Den här widgeten kategoriserar det totala antalet osegmenterade profiler efter deras unika identifierare. Data visas i ett stapeldiagram. Mer information finns i dokumentationen för [standardwidgetar](../../dashboards/guides/profiles.md#standard-widgets). |
| widgeten Enstaka identitetsprofiler | Den här widgeten innehåller information om organisationens profiler som bara har en typ av ID som skapar deras identitet, antingen ett e-postmeddelande eller ett ECID. Mer information finns i dokumentationen för [standardwidgetar](../../dashboards/guides/profiles.md#standard-widgets). |

{style="table-layout:auto"}

Mer information om profilpaneler finns i [Översikt över profilpaneler](../../dashboards/guides/profiles.md).

### Destinationspaneler

På kontrollpanelen Destinationer visas en ögonblicksbild av de destinationer som din organisation har aktiverat i Experience Platform.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Widgeten Antal destinationer | Widgeten visar totalt antal tillgängliga slutpunkter där en målgrupp kan aktiveras och levereras inom systemet. Detta nummer inkluderar både aktiva och inaktiva mål. Mer information finns i [dokumentationen för standardwidgeten ](../../dashboards/guides/destinations.md#standard-widgets). |

{style="table-layout:auto"}

Mer information om instrumentpaneler för destinationer i plattformen finns i [Översikt över instrumentpaneler för destinationer](../../dashboards/guides/destinations.md).

## Datainsamling {#data-collection}

Platform innehåller en serie teknologier som gör att ni kan samla in kundupplevelsedata på klientsidan och skicka dem till Adobe Experience Platform Edge Network där de kan berikas, omformas och distribueras till destinationer som Adobe eller inte är Adobe.

**Nya funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Globala datastream-inställningar | Du kan nu konfigurera flera nya globala inställningar när du konfigurerar ett datastream: geografisk plats, cookie för första parts-ID och synkronisering med tredje parts-ID. Mer information finns i avsnittet [Konfigurera en datastream](../../datastreams/overview.md#create) i gränssnittsguiden för datastreams. |
| [Edge Network Server-API](../../server-api/overview.md) | Server-API:t gör det möjligt för kunder att interagera med Experience Platform Edge Network med en ny autentiserad slutpunkt för att driva en mängd olika fall av datainsamling, personalisering, reklam och marknadsföring. |

Mer information om datainsamling i Platform finns i [datainsamlingsöversikten](../../collection/home.md).

## Frågetjänst {#query-service}

[!DNL Query Service] låter dig använda standard-SQL för att fråga efter data i Adobe Experience Platform [!DNL Data Lake]. Du kan ansluta till alla datauppsättningar från [!DNL Data Lake] och samla in frågeresultaten som en ny datamängd som kan användas för rapportering, Data Science Workspace eller för förtäring i kundprofilen i realtid.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| `table_exists` | Det nya funktionskommandot används för att bekräfta om det finns en tabell eller inte i systemet. Kommandot returnerar ett booleskt värde: `true` om tabellen **inte** finns och `false` om tabellen **inte** finns. Mer information finns i [SQL-syntaxdokumentationen](../../query-service/sql/syntax.md). |

{style="table-layout:auto"}

Mer information om tillgängliga funktioner finns i [Översikt över frågetjänsten](../../query-service/home.md).

## Källor {#sources}

Adobe Experience Platform kan importera data från externa källor och samtidigt strukturera, etikettera och förbättra dessa data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor som Adobe-program, molnbaserad lagring, tredjepartsprogram och ditt CRM-system.

Experience Platform tillhandahåller ett RESTful-API och ett interaktivt användargränssnitt som gör att du enkelt kan konfigurera källanslutningar för olika dataleverantörer. Dessa källanslutningar gör att du kan autentisera och ansluta till externa lagringssystem och CRM-tjänster, ange tider för matning och hantera datainmatning genom hela processen.

**Uppdaterade funktioner**

| Funktion | Beskrivning |
| --- | --- |
| Nu finns nya källor för B2B-användning | Du kan nu använda alla tillgängliga källor på plattformen för B2B-användning. En fullständig lista över tillgängliga källor finns i [källkatalogen](../../sources/home.md). |
| Allmän tillgänglighet för den nya [!DNL Oracle Eloqua]-källan | Du kan nu använda källan [!DNL Oracle Eloqua] för att importera data från din [!DNL Oracle Eloqua]-instans (konto, kampanj, kontakter) till plattformen. Mer information finns i dokumentationen för [att skapa en [!DNL Oracle Eloqua] källanslutning](../../sources/connectors/marketing-automation/oracle-eloqua.md). |
| API-förbättringar för [!DNL Data Landing Zone] | [!DNL Data Landing Zone]-källan stöder nu automatisk identifiering av filegenskaper när API:t [!DNL Flow Service] används. Mer information finns i dokumentationen om [att skapa en [!DNL Data Landing Zone] källanslutning](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

Mer information om källor finns i [Källöversikt](../../sources/home.md).
