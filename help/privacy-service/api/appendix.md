---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Godkända ID-namnutrymmen och -kvalificerare
topic: developer guide
translation-type: tm+mt
source-git-commit: cc296670db91640e75fd7a47b874a46eaf57ecde

---


# Bilaga

## Standardnamnutrymmen för identiteter {#standard-namespaces}

Alla identiteter som skickas till Integritetstjänsten måste anges under ett specifikt namnområde. Identitetsnamnutrymmen är en komponent i [Adobe Experience Platform Identity Service](../../identity-service/home.md) som anger det sammanhang som en identitet relateras till.

I följande tabell visas flera vanliga, fördefinierade identitetstyper som finns tillgängliga via Experience Platform, tillsammans med tillhörande `namespace` värden:

| Identitetstyp | `namespace` | `namespaceId` |
| --- | --- | --- |
| E-post | E-post | 6 |
| Telefon | Telefon | 7 |
| Adobe Advertising Cloud ID | AdCloud | 411 |
| Adobe Audience Manager UUID | CORE | 0 |
| Adobe Experience Cloud ID | ECID | 4 |
| Adobe Target ID | TNTID | 9 |
| Apple ID för annonsörer | IDFA | 20915 |
| Google Ad ID | GAID | 20914 |
| Windows AID | WAID | 8 |

>[!NOTE] Varje identitetstyp har också ett `namespaceId` heltalsvärde som kan användas i stället för `namespace` strängen när identitetsegenskapen ställs in på `type` namespaceId. Mer information finns i avsnittet om [namnutrymmeskvalificerare](#namespace-qualifiers) .

Du kan hämta en lista med identitetsnamnutrymmen som används av din organisation genom att göra en GET-begäran till `idnamespace/identities` slutpunkten i Identitetstjänstens API. Mer information finns i utvecklarhandboken [för](../../identity-service/api/getting-started.md) identitetstjänsten.

## Namnutrymmeskvalificerare

När du anger ett `namespace` värde i sekretesstjänstens API måste en **namnutrymmeskvalificerare** inkluderas i en motsvarande `type` parameter. Följande tabell visar de olika godkända namnutrymmeskvalificerarna.

| Kvalificerare | Definition |
| --------- | ---------- |
| standard | Ett av standardnamnutrymmena som definierats globalt, inte kopplat till en enskild organisations datauppsättning (till exempel e-post, telefonnummer osv.). Namnområdes-ID anges. |
| anpassad | Ett unikt namnutrymme som skapas i en organisations sammanhang och inte delas över hela Experience Cloud. Värdet representerar det egna namnet (&quot;namnfältet&quot;) som du vill söka efter. Namnområdes-ID anges. |
| integrationCode | Integrationskod - liknande&quot;anpassad&quot;, men specifikt definierad som integrationskoden för en datakälla som du vill söka efter. Namnområdes-ID anges. |
| namespaceId | Anger att värdet är det faktiska ID:t för namnutrymmet som skapades eller mappades via namnområdestjänsten. |
| oregistrerad | En friformssträng som inte är definierad i namnområdestjänsten och som tas &quot;as is&quot;. Alla program som hanterar den här typen av namnutrymmen kontrollerar mot dem och hanterar om det passar företagssammanhanget och datauppsättningen. Inget namnområdes-ID har angetts. |
| analys | Ett anpassat namnutrymme som mappas internt i Analytics, inte i namnområdestjänsten. Detta skickas in direkt enligt den ursprungliga begäran, utan något namnområdes-ID |
| target | Ett anpassat namnutrymme som tolkas internt av Target, inte i namnområdestjänsten. Detta skickas in direkt enligt den ursprungliga begäran, utan något namnområdes-ID |

## Godkända produktvärden

I följande tabell visas godkända värden för att ange en Adobe-produkt i attributet för en förfrågan om att skapa jobb. `include`

| Produkt | Värde som ska användas i `include` attributet |
--- | ---
| Adobe Advertizing Cloud | &quot;AdCloud&quot; |
| Adobe Analytics | &quot;Analytics&quot; |
| Adobe Audience Manager | &quot;AudienceManager&quot; |
| Adobe Campaign | &quot;Campaign&quot; |
| Adobe Experience Platform | &quot;aepDataLake&quot; |
| Adobe Primetime-autentisering | &quot;primetimeAuthentication&quot; |
| Adobe Target | &quot;Target&quot; |
| Kundposttjänst | &quot;CRS&quot; |
| Kundprofil i realtid | &quot;ProfileService&quot; |