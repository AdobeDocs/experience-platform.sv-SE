---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: API-handbok för Privacy Service
description: Det här dokumentet innehåller ytterligare information om hur du arbetar med Privacy Service-API:t.
role: Developer
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 644e85fe5c9b1a37f69c75755713e929736c2e89
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 4%

---

# Privacy Service API guide appendix

Följande avsnitt innehåller ytterligare information om hur du arbetar med Adobe Experience Platform Privacy Service API.

## Standardnamnutrymmen för identiteter {#standard-namespaces}

Alla identiteter som skickas till [!DNL Privacy Service] måste anges under ett specifikt ID-namnområde. Identitetsnamnutrymmen är en komponent i [Adobe Experience Platform Identity Service](../../identity-service/home.md) som anger kontexten som en identitet relateras till.

I följande tabell visas flera vanliga, fördefinierade identitetstyper som är tillgängliga av [!DNL Experience Platform], tillsammans med tillhörande `namespace`-värden:

| Identitetstyp | `namespace` | `namespaceId` |
| --- | --- | --- |
| E-post | `Email` | `6` |
| Telefon | `Phone` | `7` |
| ADOBE ADVERTISING CLOUD ID | `AdCloud` | `411` |
| Adobe Audience Manager UUID | `CORE` | `0` |
| ADOBE EXPERIENCE CLOUD ID | `ECID` | `4` |
| ADOBE TARGET ID | `TNTID` | `9` |
| [!DNL Apple]-ID för annonsörer | `IDFA` | `20915` |
| [!DNL Google] annons-ID | `GAID` | `20914` |
| [!DNL Windows]-STÖD | `WAID` | `8` |

{style="table-layout:auto"}

>[!NOTE]
>
>Varje identitetstyp har också ett `namespaceId`-heltalsvärde, som kan användas i stället för `namespace`-strängen när identitetsegenskapen `type` anges till &quot;namespaceId&quot;. Mer information finns i avsnittet [namnutrymmeskvalificerare](#namespace-qualifiers).

Du kan hämta en lista med identitetsnamnutrymmen som används av din organisation genom att göra en GET-begäran till `idnamespace/identities`-slutpunkten i [!DNL Identity Service] API. Mer information finns i [Utvecklarhandboken för identitetstjänsten](../../identity-service/api/getting-started.md).

## Namnutrymmeskvalificerare

När du anger ett `namespace`-värde i [!DNL Privacy Service] API måste en **namnutrymmeskvalificerare** inkluderas i en motsvarande `type`-parameter. Följande tabell visar de olika godkända namnutrymmeskvalificerarna.

| Kvalificerare | Definition |
| --------- | ---------- |
| `standard` | Ett av standardnamnutrymmena som definierats globalt, inte kopplat till en enskild organisations datauppsättning (till exempel e-post, telefonnummer osv.). Namnområdes-ID anges. |
| `custom` | Ett unikt namnområde har skapats i kontexten för en organisation, som inte delas över [!DNL Experience Cloud]. Värdet representerar det egna namnet (&quot;namnfältet&quot;) som du vill söka efter. Namnområdes-ID anges. |
| `integrationCode` | Integrationskod - liknande&quot;anpassad&quot;, men specifikt definierad som integrationskoden för en datakälla som du vill söka efter. Namnområdes-ID anges. |
| `namespaceId` | Anger att värdet är det faktiska ID:t för namnutrymmet som skapades eller mappades via namnområdestjänsten. |
| `unregistered` | En friformssträng som inte är definierad i namnområdestjänsten och som tas &quot;as is&quot;. Alla program som hanterar den här typen av namnutrymmen kontrollerar mot dem och hanterar om det passar företagssammanhanget och datauppsättningen. Inget namnområdes-ID har angetts. |
| `analytics` | Ett anpassat namnutrymme som mappas internt i [!DNL Analytics], inte i namnområdestjänsten. Detta skickas in direkt enligt den ursprungliga begäran, utan något namnområdes-ID |
| `target` | Ett anpassat namnutrymme som tolkas internt av [!DNL Target], inte i namnområdestjänsten. Detta skickas in direkt enligt den ursprungliga begäran, utan något namnområdes-ID |

{style="table-layout:auto"}

## Godkända produktvärden

I följande tabell visas godkända värden för att ange en Adobe-produkt i attributet `include` för en jobbskapandebegäran.

>[!NOTE]
>
>Värdena för produktlistan är skiftlägeskänsliga. Fallstudier rekommenderas men inte.

| Produkt | Värde som ska användas i attributet `include` |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `audienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform (Data Lake) | `aepDataLake` |
| Adobe Experience Platform (kundprofil i realtid) | `profileService` |
| Adobe Pass-autentisering | `primetimeAuthentication` |
| Adobe Target | `target` |
| Kundattribut | `CRS` |
| Kundresehantering | `cjm` |
| Identitetstjänst | `identity` |
| Marketo Engage | `marketo` |
| Marketo Measure | `marketomeasure` |

{style="table-layout:auto"}
