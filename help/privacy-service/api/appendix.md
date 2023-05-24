---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: API-handbok för Privacy Service
description: Det här dokumentet innehåller ytterligare information om hur du arbetar med Privacy Service-API:t.
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 4%

---

# Privacy Service API guide appendix

Följande avsnitt innehåller ytterligare information om hur du arbetar med Adobe Experience Platform Privacy Service API.

## Standardnamnutrymmen för identiteter {#standard-namespaces}

Alla identiteter som skickas till [!DNL Privacy Service] måste anges under ett specifikt ID-namnutrymme. Identitetsnamnutrymmen är en komponent i [Adobe Experience Platform Identity Service](../../identity-service/home.md) som anger det sammanhang som en identitet hör till.

I följande tabell beskrivs flera vanliga, fördefinierade identitetstyper som är tillgängliga av [!DNL Experience Platform], tillsammans med deras associerade `namespace` värden:

| Identitetstyp | `namespace` | `namespaceId` |
| --- | --- | --- |
| E-post | `Email` | `6` |
| Telefon | `Phone` | `7` |
| Adobe Advertising Cloud ID | `AdCloud` | `411` |
| Adobe Audience Manager UUID | `CORE` | `0` |
| Adobe Experience Cloud ID | `ECID` | `4` |
| Adobe Target ID | `TNTID` | `9` |
| [!DNL Apple] ID för annonsörer | `IDFA` | `20915` |
| [!DNL Google] Annons-ID | `GAID` | `20914` |
| [!DNL Windows] AID | `WAID` | `8` |

{style="table-layout:auto"}

>[!NOTE]
>
>Varje identitetstyp har också en `namespaceId` heltalsvärde, som kan användas i stället för `namespace` sträng när identiteten anges `type` till namespaceId. Se avsnittet om [namnutrymmeskvalificerare](#namespace-qualifiers) för mer information.

Du kan hämta en lista över identitetsnamnutrymmen som används av din organisation genom att göra en GET-förfrågan till `idnamespace/identities` slutpunkt i [!DNL Identity Service] API. Se [Utvecklarhandbok för identitetstjänst](../../identity-service/api/getting-started.md) för mer information.

## Namnutrymmeskvalificerare

När du anger en `namespace` värdet i [!DNL Privacy Service] API, en **namnutrymmeskvalificerare** måste inkluderas i en `type` parameter. Följande tabell visar de olika godkända namnutrymmeskvalificerarna.

| Kvalificerare | Definition |
| --------- | ---------- |
| `standard` | Ett av standardnamnutrymmena som definierats globalt, inte kopplat till en enskild organisations datauppsättning (till exempel e-post, telefonnummer osv.). Namnområdes-ID anges. |
| `custom` | Ett unikt namnutrymme som skapats i en organisations sammanhang och inte delas över hela organisationen [!DNL Experience Cloud]. Värdet representerar det egna namnet (&quot;namnfältet&quot;) som du vill söka efter. Namnområdes-ID anges. |
| `integrationCode` | Integrationskod - liknande&quot;anpassad&quot;, men specifikt definierad som integrationskoden för en datakälla som du vill söka efter. Namnområdes-ID anges. |
| `namespaceId` | Anger att värdet är det faktiska ID:t för namnutrymmet som skapades eller mappades via namnområdestjänsten. |
| `unregistered` | En friformssträng som inte är definierad i namnområdestjänsten och som tas &quot;as is&quot;. Alla program som hanterar den här typen av namnutrymmen kontrollerar mot dem och hanterar om det passar företagssammanhanget och datauppsättningen. Inget namnområdes-ID har angetts. |
| `analytics` | Ett anpassat namnutrymme som mappas internt i [!DNL Analytics], inte i namnområdestjänsten. Detta skickas in direkt enligt den ursprungliga begäran, utan något namnområdes-ID |
| `target` | Ett anpassat namnutrymme som tolkas internt av [!DNL Target], inte i namnområdestjänsten. Detta skickas in direkt enligt den ursprungliga begäran, utan något namnområdes-ID |

{style="table-layout:auto"}

## Godkända produktvärden

I följande tabell visas godkända värden för att ange en Adobe-produkt i `include` attribut för en jobbskapandebegäran.

| Produkt | Värde som ska användas i `include` attribute |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `AudienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform (Data Lake) | `aepDataLake` |
| Adobe Experience Platform (kundprofil i realtid) | `profileService` |
| Adobe Primetime-autentisering | `primetimeAuthentication` |
| Adobe Target | `target` |
| Kundattribut | `CRS` |
| Identitetstjänst | `identity` |
| Marketo Engage | `marketo` |

{style="table-layout:auto"}
