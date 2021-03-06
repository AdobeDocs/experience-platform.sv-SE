---
keywords: Experience Platform;hem;populära ämnen;Analytics Source Connector;analytics;Analytics;AAID;
title: Adobe Analytics Source Connector for Report-Suite Data
description: Det här dokumentet innehåller en översikt över Analytics och en beskrivning av användningsfall för Analytics-data.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: 352993365dfcd4f39e7aea337b014430f7bad41c
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# Adobe Analytics källanslutning för rapportsuite-data

Med Adobe Experience Platform kan ni importera Adobe Analytics-data via Analytics-källkopplingen. The [!DNL Analytics] källanslutningsströmmar data som samlats in av [!DNL Analytics] till plattformen i realtid, konvertera SCDS-formaterade [!DNL Analytics] data till [!DNL Experience Data Model] (XDM)-fält för förbrukning per plattform.

Dokumentet innehåller en översikt över [!DNL Analytics] och beskriver användningsfall för [!DNL Analytics] data.

## Adobe Analytics- och Analytics-data

[!DNL Analytics] är en kraftfull motor som hjälper er att lära er mer om era kunder, hur de interagerar med era webbegenskaper, se var era utgifter för digital marknadsföring är effektiva och identifiera områden där det finns förbättringar. [!DNL Analytics] hanterar miljontals webbtransaktioner per år och [!DNL Analytics] Med källanslutaren kan du enkelt utnyttja dessa omfattande beteendedata och berika [!DNL Real-time Customer Profile] på bara några minuter.

![](./images/analytics-data-experience-platform.png)

På en hög nivå [!DNL Analytics] samlar in data från olika digitala kanaler och från flera datacenter över hela världen. När data har samlats in tillämpas VISTA-regler (Visitor Identification, Segmentation and Transformation Architecture) och bearbetningsregler för att forma inkommande data. När rådata har genomgått den här enkla bearbetningen anses de vara klara att användas av [!DNL Real-time Customer Profile]. I en process som är parallell med ovanstående är samma bearbetade data mikrobatchade och insamlade i plattformsdatauppsättningar för konsumtion genom [!DNL Data Science Workspace], [!DNL Query Service]och andra program för dataidentifiering.

Se [översikt över bearbetningsregler](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html) för mer information om bearbetningsregler.

## Experience Data Model (XDM)

XDM är en offentligt dokumenterad specifikation som innehåller gemensamma strukturer och definitioner för en tillämpning som ska användas för att kommunicera med tjänster på Experience Platform.

Genom att följa XDM-standarder kan data integreras på ett enhetligt sätt, vilket gör det enklare att leverera data och samla in information.

Mer information om XDM finns i [XDM - systemöversikt](../../../xdm/home.md).

## Hur mappas fält från Adobe Analytics till XDM?

När en källanslutning upprättas för att [!DNL Analytics] data till Experience Platform med hjälp av användargränssnittet för plattformen, mappas datafälten automatiskt och hämtas till [!DNL Real-time Customer Profile] inom några minuter. Instruktioner om hur du skapar en källanslutning med [!DNL Analytics] med hjälp av plattformsgränssnittet, se [Självstudiekurs om anslutning till analyskälla](../../tutorials/ui/create/adobe-applications/analytics.md).

Detaljerad information om fältmappningen som finns mellan [!DNL Analytics] och Experience Platform, se [Adobe Analytics fältmappning](./mapping/analytics.md) guide.

## Vilken fördröjning förväntas för Analytics Data on Platform?

Den förväntade fördröjningen för Analytics Data on Platform beskrivs i tabellen nedan. Svarstiden varierar beroende på kundens konfiguration, datavolymer och konsumentprogram. Om till exempel Analytics-implementeringen har konfigurerats med `A4T` latensen till Pipeline kommer att öka till 5-10 minuter.

| Analysdata | Förväntad svarstid |
| -------------- | ---------------- |
| Nya data till [!DNL Real-time Customer Profile] (A4T **not** aktiverad) | &lt; 2 minuter |
| Nya data till [!DNL Real-time Customer Profile] (A4T **är** aktiverad) | &lt; 15 minuter |
| Nya data till Data Lake | &lt; 90 minuter |
| Fyll i data i bakgrunden (13 månaders data eller 10 miljarder händelser, beroende på vilket som är lägst) | &lt; 4 veckor |

>[!NOTE]
>
>Data för analysbakåtfyllnad importeras inte till [!DNL Profile] och tas därför inte med i licensprofilerna.

## Primära identifierare i [!DNL Analytics] data

Varje träff från [!DNL Analytics] källkopplingen innehåller en primär identifierare som är beroende av om det finns ett ECID eller ett AAID. Om det finns ett ECID-id anges ECID som primär identifierare. Om det finns ett AAID-id anges AAID som primär.

Följande tabell innehåller mer information om identitetsfält i [!DNL Analytics] data.

| Identitetsfält | Beskrivning |
| --- | --- |
| AAID | AAID är den primära enhetsidentifieraren i Adobe Analytics och finns garanterat för varje händelse som skickas via [!DNL Analytics] källa. Stödet kallas ibland för *ID för äldre analys* eller som `s_vi` cookie-ID. Trots detta skapas ett AAID även om `s_vi` cookie finns inte. Stödet representeras av `post_visid_high` och `post_visid_low` kolumner i [[!DNL Analytics] dataflöden](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). För en given händelse innehåller AAID-fältet en enda identitet som kan vara någon av de olika typerna som beskrivs i [ordning för operationer [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **Anteckning**: Inom en hel rapportsvit kan ett AAID innehålla en blandning av typer för olika händelser. |
| ECID | ECID (Experience Cloud-ID) är ett separat fält för enhetsidentifierare, som fylls i i Adobe Analytics när [!DNL Analytics] implementeras med Experience Cloud Identity Service. ECID kallas ibland även MCID (Marketing Cloud-ID). Om ett ECID finns för en händelse kan detta baseras på ECID beroende på om Analytics [respitperiod](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) är konfigurerad. ECID representeras av `mcvisid` i Analytics-dataflöden. Mer information om ECID finns i [ECID - översikt](../../../identity-service/ecid.md). För information om hur ECID fungerar med [!DNL Analytics], se dokumentet på [Begäranden om analyser och Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html?lang=en). |
| AACUSTOMID | AACUSTOMID är ett separat identifierarfält som fylls i i Adobe Analytics baserat på användningen av `s.VisitorID` variabeln i [!DNL Analytics] implementering. AACUSTOMID representeras av `cust_visid` kolumn i [[!DNL Analytics] dataflöden](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). Om det finns ett AACUSTOMID kommer stödet att baseras på AACUSTOMID eftersom AACUSTOMID överför alla andra identifierare enligt definitionen i [ordning för operationer [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### Hur [!DNL Analytics] source behandlar identiteter

The [!DNL Analytics] source skickar dessa identiteter till Experience Platform i XDM-format som:

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

Dessa fält är inte markerade som identiteter. I stället kopieras samma identiteter till XDM:s `identityMap` som nyckelvärdepar:

* `{ “key”: “AAID”, “value”: [ { “id”: “<identity>”, “primary”: <true or false> } ] }`
* `{ “key”: “ECID”, “value”: [ { “id”: “<identity>”, “primary”: <true or false> } ] }`
* `{ “key”: “AACUSTOMID”, “value”: [ { “id”: “<identity>”, “primary”: false } ] }`

Om det finns ECID på identitetskartan markeras den som händelsens primära identitet. I detta fall kan stödet baseras på ECID på grund av [Giltighetsperiod för identitetstjänst](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). I annat fall markeras AID som händelsens primära identitet. AACUSTOMID markeras aldrig som händelsens primära ID. Om det finns ett AACUSTOMID, baseras emellertid AAID på AACUSTOMID på grund av att åtgärderna utförs i Experience Cloud.

### Customer Journey Analytics och primärt ID

För Customer Journey Analytics är definitionen av primärt ID bara viktig om du bestämmer dig för att använda primärt ID som person-ID. Detta är dock inte obligatoriskt. Du kan välja någon annan identitetskolumn som person-ID.