---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Audience Manager-koppling
topic: overview
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

---


# Audience Manager-koppling

Adobe Audience Manager-datakopplingen strömmar data från första part som samlats in i Adobe Audience Manager till Adobe Experience Platform. Audience Manager-kopplingen importerar tre olika datakategorier till plattformen:

- **Realtidsdata:** Data som samlats in i realtid på Audience Managers datainsamlingsserver. Dessa data används i Audience Manager för att fylla i regelbaserade egenskaper och kommer att visas i plattformen på kortast möjliga latenstid.
- **Inbyggda (inkommande) data:** Det här är de filer som har överförts av en användare till en Amazon S3-plats hos Audience Manager. Audience Manager använder dessa data för att fylla i anpassade egenskaper med den inkommande filmetoden och har viss fördröjning.
- **Profildata:** Audience Manager använder realtids- och onboarddata för att ta fram kundprofiler. De här profilerna används för att fylla i identitetsdiagram och egenskaper för segmentimplementeringar.

Audience Manager-kopplingen mappar dessa datakategorier till XDM-schemat (Experience Data Model) och skickar dem till Platform. Realtidsdata och onboarddata skickas som XDM ExperienceEvent-data, medan profildata skickas som enskilda XDM-profiler.

Instruktioner om hur du skapar en anslutning med Adobe Audience Manager med hjälp av plattformsgränssnittet finns i självstudiekursen [för Audience Manager-koppling](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## Vad är Experience Data Model (XDM)?

XDM är en öppet dokumenterad specifikation som tillhandahåller ett standardiserat ramverk genom vilket Platform organiserar kundupplevelsedata.

Genom att följa XDM-standarder kan kundupplevelsedata integreras på ett enhetligt sätt, vilket gör det enklare att leverera data och samla in information.

Mer information om hur XDM används i Experience Platform finns i [XDM-systemöversikten](../../../xdm/home.md). Mer information om hur XDM-scheman som Profile och ExperienceEvent är strukturerade finns i [grunderna för schemakomposition](../../../xdm/schema/composition.md).

## XDM-scheman - exempel

Nedan visas exempel på Audience Manager-strukturen som är mappad till XDM ExperienceEvent och XDM Individual Profile i Platform.

### ExperienceEvent - för realtidsdata och onboarddata

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Individuell XDM-profil - för profildata

![](images/aam-profile-xdm-for-profile-data.png)

## Hur mappas fält från Adobe Audience Manager till XDM?

Mer information finns i dokumentationen för mappningsfält [för][audience-manager-mapping-fields] Audience Manager.

## Datahantering på plattformen

### Datauppsättningar

Datauppsättningar är en lagrings- och hanteringskonstruktion för en samling data, vanligtvis en tabell, som innehåller schema (kolumner) och fält (rader) och som görs tillgängliga via en dataanslutning. Audience Manager-data består av Realtime-data, inkommande data och profildata. Om du vill hitta dina Audience Manager-datauppsättningar använder du sökfunktionen i gränssnittet med de namnkonventioner som anges för varje datatyp.

Även om användare kan inaktivera datauppsättningar rekommenderar vi inte att du inaktiverar datauppsättningar som ska användas för segmentmedlemskap i profilen.

| Namn på datauppsättning | Beskrivning |
| ------------ | ----------- |
| Audience Manager Realtime | Den här datauppsättningen innehåller data som samlats in med direktträffar på Audience Manager DCS-slutpunkter och identitetskartor för Audience Manager-profiler. Låt den här datauppsättningen vara aktiverad för profilinmatning. |
| Profiluppdateringar för Audience Manager Realtime | Den här datauppsättningen gör att målgruppsanpassning för Audience Manager-egenskaper och segment kan användas i realtid. Det innehåller information om Edge regional routning, egenskaper och segmentmedlemskap. Låt den här datauppsättningen vara aktiverad för profilinmatning. |
| Data för Audience Manager-enheter | Enhetsdata med ECID:n och motsvarande segmentimplementeringar sammanställda i Audience Manager. |
| Profildata för målgruppshanteraren | Används för Audience Manager-anslutningsdiagnostik. |
| Audience Manager-autentiserade profiler | Den här datauppsättningen innehåller autentiserade profiler för Audience Manager. |
| Metadata för autentiserade profiler för Audience Manager | Används för diagnostik av Audience Manager Connector. |
| Audience Manager Inbound {Datasource ID} **(inaktuellt)** | Den här datauppsättningen representerar onboardade poster i Audience Manager via metoden för inkommande filer. Detta dataflöde är föråldrat och kommer att tas bort i en senare version. |
| Inkommande metadata för Audience Manager **(inaktuellt)** | Används för Audience Manager-anslutningsdiagnostik. Detta dataflöde är föråldrat och kommer att tas bort i en senare version. |

### Anslutningar

Adobe Audience Manager skapar en anslutning i katalogen: Audience **Manager Connection**. Katalog är det system som används för att registrera dataplatser och datalänkning inom Adobe Experience Platform. En anslutning är ett katalogobjekt som är en kundspecifik instans av Connectors. Mer information om kataloger, anslutningar och anslutningar finns i översikten [för](../../../catalog/home.md) katalogtjänsten.

## Vilken fördröjning förväntas för Audience Manager-data på plattformen?

| Data för Audience Manager | Latens | Anteckningar |
| --- | --- | --- |
| Realtidsdata | &lt; 35 minuter. | Tid från att hämtas vid Realtime-noden till att visas på en plattformsdatasjön. |
| Inkommande data | &lt; 13 timmar | Tiden från att bli fångad i S3-bucket till att visas på Platform Data Lake. |
| Profildata | &lt; 2 dagar | Tiden från att hämtas från Realtime/Inbound-data till att läggas till i en användarprofil och slutligen visas på Platform Data Lake. |