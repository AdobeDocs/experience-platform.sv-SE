---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: API-handbok för Privacy Service
topic: developer guide
description: Det här dokumentet innehåller ytterligare information om hur du arbetar med Privacy Service-API:t.
translation-type: tm+mt
source-git-commit: b395535cbe7e4030606ee2808eb173998f5c32e0
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 6%

---


# Privacy Service API guide appendix

Följande avsnitt innehåller ytterligare information om hur du arbetar med Adobe Experience Platform Privacy Service API.

## Standardnamnutrymmen för identiteter {#standard-namespaces}

Alla identiteter som skickas till [!DNL Privacy Service] måste anges under ett specifikt identitetsnamnutrymme. Identitetsnamnutrymmen är en komponent i [Adobe Experience Platform Identity Service](../../identity-service/home.md) som anger kontexten som en identitet relateras till.

I följande tabell visas flera vanliga, fördefinierade identitetstyper som är tillgängliga av [!DNL Experience Platform], tillsammans med deras associerade `namespace`-värden:

| Identitetstyp | `namespace` | `namespaceId` |
| --- | --- | --- |
| E-post | E-post | 6 |
| Telefon | Telefon | 7 |
| Adobe Advertising Cloud ID | AdCloud | 411 |
| Adobe Audience Manager UUID | CORE | 0 |
| Adobe Experience Cloud ID | ECID | 4 |
| Adobe Target ID | TNTID | 9 |
| [!DNL Apple] ID för annonsörer | IDFA | 20915 |
| [!DNL Google] Annons-ID | GAID | 20914 |
| [!DNL Windows] AID | WAID | 8 |

>[!NOTE]
>
>Varje identitetstyp har också ett `namespaceId`-heltalsvärde, som kan användas i stället för strängen `namespace` när identitetsegenskapen `type` anges till &quot;namespaceId&quot;. Mer information finns i avsnittet [namnutrymmeskvalificerare](#namespace-qualifiers).

Du kan hämta en lista med identitetsnamnutrymmen som används av din organisation genom att göra en GET-begäran till `idnamespace/identities`-slutpunkten i [!DNL Identity Service]-API:t. Mer information finns i [Utvecklarhandboken för identitetstjänsten](../../identity-service/api/getting-started.md).

## Namnutrymmeskvalificerare

När du anger ett `namespace`-värde i API:t [!DNL Privacy Service] måste en **namnutrymmeskvalificerare** inkluderas i en motsvarande `type`-parameter. Följande tabell visar de olika godkända namnutrymmeskvalificerarna.

| Kvalificerare | Definition |
| --------- | ---------- |
| standard | Ett av standardnamnutrymmena som definierats globalt, inte kopplat till en enskild organisations datauppsättning (till exempel e-post, telefonnummer osv.). Namnområdes-ID anges. |
| anpassad | Ett unikt namnutrymme som skapats i en organisations kontext, som inte delas över [!DNL Experience Cloud]. Värdet representerar det egna namnet (&quot;namnfältet&quot;) som du vill söka efter. Namnområdes-ID anges. |
| integrationCode | Integrationskod - liknande&quot;anpassad&quot;, men specifikt definierad som integrationskoden för en datakälla som du vill söka efter. Namnområdes-ID anges. |
| namespaceId | Anger att värdet är det faktiska ID:t för namnutrymmet som skapades eller mappades via namnområdestjänsten. |
| oregistrerad | En friformssträng som inte är definierad i namnområdestjänsten och som tas &quot;as is&quot;. Alla program som hanterar den här typen av namnutrymmen kontrollerar mot dem och hanterar om det passar företagssammanhanget och datauppsättningen. Inget namnområdes-ID har angetts. |
| analys | Ett anpassat namnutrymme som mappas internt i [!DNL Analytics], inte i namnområdestjänsten. Detta skickas in direkt enligt den ursprungliga begäran, utan något namnområdes-ID |
| target | Ett anpassat namnutrymme som tolkas internt av [!DNL Target], inte i namnområdestjänsten. Detta skickas in direkt enligt den ursprungliga begäran, utan något namnområdes-ID |

## Godkända produktvärden

I följande tabell visas godkända värden för att ange en Adobe-produkt i attributet `include` för en jobbskapandebegäran.

| Produkt | Värde som ska användas i attributet `include` |
--- | ---
| Adobe Advertising Cloud | &quot;AdCloud&quot; |
| Adobe Analytics | &quot;Analytics&quot; |
| Adobe Audience Manager | &quot;AudienceManager&quot; |
| Adobe Campaign | &quot;Campaign&quot; |
| Adobe Experience Platform | &quot;aepDataLake&quot; |
| Adobe Primetime-autentisering | &quot;primetimeAuthentication&quot; |
| Adobe Target | &quot;Målgrupp&quot; |
| Kundposttjänst | &quot;CRS&quot; |
| Kundprofil i realtid | &quot;ProfileService&quot; |