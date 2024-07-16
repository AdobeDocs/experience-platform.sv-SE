---
title: Adobe Analytics Source Connector for Report-Suite Data
description: Det här dokumentet innehåller en översikt över Analytics och en beskrivning av användningsfall för Analytics-data.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: d56a37c5b1c5768b3f6811be9d30d45628fdabca
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 0%

---

# Adobe Analytics källanslutning för rapportsuite-data

Med Adobe Experience Platform kan ni importera Adobe Analytics-data via Analytics-källkopplingen. Källkopplingen [!DNL Analytics] strömmar data som samlats in av [!DNL Analytics] till plattformen i realtid och konverterar SCDS-formaterade [!DNL Analytics]-data till [!DNL Experience Data Model] (XDM)-fält för användning på plattformen.

Det här dokumentet innehåller en översikt över [!DNL Analytics] och en beskrivning av användningsfall för [!DNL Analytics]-data.

## Adobe Analytics och Analytics

[!DNL Analytics] är en kraftfull motor som hjälper dig att lära dig mer om dina kunder, hur de interagerar med dina webbegenskaper, se var era utgifter för digital marknadsföring är effektiva och identifiera områden med förbättringar. [!DNL Analytics] hanterar miljontals webbtransaktioner per år och med [!DNL Analytics]-källkopplingen kan du enkelt utnyttja dessa omfattande beteendedata och berika [!DNL Real-Time Customer Profile] på några minuter.

![En bild som illustrerar dataöverföringen från olika Adobe-program, inklusive Adobe Analytics.](./images/analytics-data-experience-platform.png)

På en hög nivå samlar [!DNL Analytics] in data från olika digitala kanaler och från flera datacenter runt om i världen. När data har samlats in tillämpas VISTA-regler (Visitor Identification, Segmentation and Transformation Architecture) och bearbetningsregler för att forma inkommande data. När rådata har genomgått den här enkla bearbetningen anses de vara klara att användas av [!DNL Real-Time Customer Profile]. I en process som är parallell med ovanstående är samma bearbetade data mikrobatchade och insamlade i plattformsdatauppsättningar för konsumtion av [!DNL Query Service] och andra program för dataidentifiering.

Mer information om bearbetningsregler finns i [översikten över bearbetningsregler](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html?lang=sv).

## Experience Data Model (XDM)

XDM är en offentligt dokumenterad specifikation som innehåller gemensamma strukturer och definitioner för en tillämpning som ska användas för att kommunicera med tjänster på Experience Platform.

Genom att följa XDM-standarder kan data integreras på ett enhetligt sätt, vilket gör det enklare att leverera data och samla in information.

Mer information om XDM finns i [XDM-systemöversikt](../../../xdm/home.md).

## Hur mappas fält från Adobe Analytics till XDM?

>[!IMPORTANT]
>
>Omformningar av dataförberedelser kan öka fördröjningen i det övergripande dataflödet. Den extra fördröjning som läggs till varierar beroende på komplexiteten i omvandlingslogiken.

När en källanslutning har upprättats för att hämta [!DNL Analytics]-data till Experience Platform via användargränssnittet för plattformen, mappas datafälten automatiskt och hämtas till [!DNL Real-Time Customer Profile] inom några minuter. Instruktioner om hur du skapar en källanslutning med [!DNL Analytics] med hjälp av plattformsgränssnittet finns i [självstudiekursen för Analytics-källkopplingen](../../tutorials/ui/create/adobe-applications/analytics.md).

Mer information om fältmappning mellan [!DNL Analytics] och Experience Platform finns i handboken om [Adobe Analytics-fältmappning](./mapping/analytics.md).

## Vilken fördröjning förväntas för Analytics Data on Platform?

Den förväntade fördröjningen för Analytics Data on Platform beskrivs i tabellen nedan. Svarstiden varierar beroende på kundens konfiguration, datavolymer och konsumentprogram. Om till exempel Analytics-implementeringen har konfigurerats med `A4T` kommer fördröjningen till Pipeline att öka till 5-10 minuter.

| Analysdata | Förväntad svarstid |
| -------------- | ---------------- |
| Nya data till [!DNL Real-Time Customer Profile] (A4T **inte** aktiverat) | &lt; 2 minuter |
| Nya data till [!DNL Real-Time Customer Profile] (A4T **är** aktiverat) | upp till 30 minuter |
| Nya data till Data Lake | &lt; 2,25 timmar |
| Nya data till Customer Journey Analytics utan [sammanfogning](https://experienceleague.adobe.com/docs/analytics-platform/using/stitching/overview.html?lang=en) | &lt; 3,75 timmar |
| Nya data för Customer Journey Analytics med sammanfogning | &lt; 7 timmar |
| Bakgrundsfyllning av mindre än 10 miljarder händelser | &lt; 4 veckor |

Mer information om latenser för Customer Journey Analytics finns i: [Customer Journey Analytics GuarDRAils](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html?lang=en).

Analysens bakgrundsfyllning för produktionssandlådor är som standard 13 månader. För Analytics-data i icke-produktionssandlådor anges backfill till tre månader. Den gräns på 10 miljarder händelser som nämns i tabellen ovan är strikt relaterad till förväntad fördröjning.

När du skapar ett datakällflöde för Analytics i en produktionssandlåda skapas två dataflöden:

* Ett dataflöde som gör en 13-månaders efterfyllning av historiska rapportsvitdata till datasjön. Det här dataflödet avslutas när bakgrundsfyllningen är slutförd.
* Ett dataflöde som skickar livedata till datavjön och till [!DNL Real-Time Customer Profile]. Det här dataflödet körs kontinuerligt.

>[!NOTE]
>
>Data för analysbakåtfyllnad importeras inte till [!DNL Profile] och tas därför inte med i licensprofiler.

## Primära identifierare i [!DNL Analytics]-data

Varje träff från [!DNL Analytics]-källkopplingen innehåller en primär identifierare som är beroende av om det finns ett ECID eller ett AAID. Om det finns ett ECID-id anges ECID som primär identifierare. Om det finns ett AAID-id anges AAID som primär.

Följande tabell innehåller mer information om identitetsfält i dina [!DNL Analytics]-data.

| Identitetsfält | Beskrivning |
| --- | --- |
| STÖD | AAID är den primära enhetsidentifieraren i Adobe Analytics och finns garanterat för varje händelse som skickas via källan [!DNL Analytics]. AAID kallas ibland *Legacy Analytics ID* eller `s_vi` cookie ID. Trots detta skapas ett AAID även om cookien `s_vi` inte finns. AAID representeras av kolumnerna `post_visid_high` och `post_visid_low` i [[!DNL Analytics] dataflöden](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). För en given händelse innehåller AAID-fältet en enda identitet som kan vara någon av de olika typerna som beskrivs i [åtgärdsordningen för [!DNL Analytics] ID:n](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **Obs!**: Inom en hel rapportserie kan ett AAID innehålla en blandning av typer för olika händelser. |
| ECID | ECID (Experience Cloud-ID) är ett separat enhetsidentifieringsfält som fylls i i Adobe Analytics när [!DNL Analytics] implementeras med hjälp av identitetstjänsten för Experience Cloud. ECID kallas ibland även MCID (Marketing Cloud-ID). Om det finns ett ECID för en händelse kan AAID baseras på ECID, beroende på om [respitperioden](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) för Analytics har konfigurerats. ECID representeras av `mcvisid` i Analytics-dataflöden. Mer information om ECID finns i [Översikt över ECID](../../../identity-service/features/ecid.md). Mer information om hur ECID fungerar med [!DNL Analytics] finns i dokumentet om [Analytics and Experience Cloud ID Requests](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html). |
| AACUSTOMID | AACUSTOMID är ett separat identifierarfält som fylls i i Adobe Analytics baserat på användningen av variabeln `s.VisitorID` i implementeringen av [!DNL Analytics]. AACUSTOMID representeras av kolumnen `cust_visid` i [[!DNL Analytics] dataflöden](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). Om det finns ett AACUSTOMID kommer AAID att baseras på AACUSTOMID eftersom AACUSTOMID överför alla andra identifierare enligt [ordningen för åtgärder för [!DNL Analytics] ID:n](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### Så här behandlar källan [!DNL Analytics] identiteter

[!DNL Analytics]-källan skickar dessa identiteter till Experience Platform i XDM-format som:

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

Dessa fält är inte markerade som identiteter. I stället kopieras samma identiteter (om sådana finns i händelsen) till XDM:s `identityMap` som nyckelvärdepar:

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

När identiteten eller identiteterna kopieras till `identityMap` ställs `endUserIDs._experience.mcid.namespace.code` också in på samma händelse:

* Om det finns ett AAID är `endUserIDs._experience.aaid.namespace.code` inställt på AAID.
* Om det finns ett ECID är `endUserIDs._experience.mcid.namespace.code` inställt på ECID.
* Om det finns ett AACUSTOMID är `endUserIDs._experience.aacustomid.namespace.code` inställt på &quot;AACUSTOMID&quot;.

Om det finns ECID på identitetskartan markeras den som händelsens primära identitet. I det här fallet kan AAID baseras på ECID på grund av den [respitperiod för identitetstjänsten](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). I annat fall markeras AID som händelsens primära identitet. AACUSTOMID markeras aldrig som händelsens primära ID. Om det finns ett AACUSTOMID, baseras emellertid AAID på AACUSTOMID på grund av att åtgärderna utförs i Experience Cloud.

>[!NOTE]
>
>Du kan använda Data Prep för att filtrera bort sekundära identiteter som kommer från Analytics, till exempel AAID och AACUSTOMID. Om de filtreras bort kommer dessa identiteter inte att importeras till profilen om de är tillgängliga i inkommande analysdata. Ofiltrerade data kommer även i fortsättningen att läsas in i datasjön.
