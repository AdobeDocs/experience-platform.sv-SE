---
keywords: Experience Platform;hem;populära ämnen
solution: Experience Platform
title: Privacy Service API Guide Appendix
description: Det här dokumentet innehåller ytterligare information om hur du arbetar med Privacy Service API.
role: Developer
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 36871289743f384207bb149df6e5e1af14d4d371
workflow-type: tm+mt
source-wordcount: '551'
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
| ADOBE ADVERTISING ID | `AdCloud` | `411` |
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

## Namnutrymmeskvalificerare {#namespace-qualifiers}

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

## Godkända produktvärden {#accepted-product-values}

I det här avsnittet visas de produktidentifieringsvärden som accepteras i attributet `include` när Privacy Service-jobb skapas (API eller UI). Använd dessa värden i `include`-arrayen för din jobbförfrågan.

I följande tabell visas vilka produkter som stöds, deras användargränssnitt och deras motsvarande kodvärden.

>[!NOTE]
>
>- Produktvärdena är inte skiftlägeskänsliga. Kamerafodral rekommenderas för enhetlighet.
>- Endast produkterna ovan stöds i gränssnittet och API:t. Om en produkt inte har etablerats för din organisation kan den ignoreras eller orsaka ett valideringsfel - se ditt Adobe kontrakt eller dokumentationen för etablering för att bekräfta berättigandet.

| Varumärkesnamn | Användargränssnittets visningsnamn | `include` värde |
| ------------------------------------------------------ | -------------------------- | ---------------------------------------- |
| Adobe Analytics | [!UICONTROL Analytics] | `analytics` |
| Adobe Audience Manager | [!UICONTROL Audience Manager] | `audienceManager` |
| Adobe Advertising | [!UICONTROL Ad Cloud] | `adCloud` |
| Adobe Experience Platform (Profilbutik) | [!UICONTROL Profile] | `profileService` |
| Adobe Experience Platform (Data Lake) | [!UICONTROL AEP Data Lake] | `aepDataLake` |
| Adobe Campaign | [!UICONTROL Campaign] | `campaign` |
| Adobe Target | [!UICONTROL Target] | `target` |
| Kundattribut | [!UICONTROL Customer Attributes (CRS)] | `CRS` |
| Adobe Journey Optimizer | [!UICONTROL Adobe Journey Optimizer] | `cjm` |
| Marketo Engage | [!UICONTROL Marketo Engage / AJO B2B] | `marketo` |
| Identitetstjänst | [!UICONTROL Identity] | `identity` |
| Marketo Measure | [!UICONTROL Marketo Measure] | `marketomeasure` |
| Adobe Commerce | [!UICONTROL Commerce (Personalization)] | `commerceMarketingData` |

{style="table-layout:auto"}
