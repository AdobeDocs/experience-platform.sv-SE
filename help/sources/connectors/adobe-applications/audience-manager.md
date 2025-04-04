---
keywords: Experience Platform;home;populära topics;Audience Manager connector;Audience manager;målgruppshanterare
solution: Experience Platform
title: Audience Manager Source - översikt
description: Adobe Audience Manager-källan strömmar förstahandsdata som samlats in i Audience Manager till Adobe Experience Platform.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 0%

---

# Audience Manager-källa

>[!IMPORTANT]
>
>Vid den första konfigurationen returnerar Adobe Audience Manager-källan ett felmeddelande som förklarar att det inte finns något identitetsnamnutrymme med `namespaceCode={VALUE}`. **Obs!**: I den bakre änden används `namespaceCode` för att referera till identitetssymbol. För att slutföra integreringen måste du:
>
>- [Skapa ett anpassat namnutrymme i identitetstjänsten](../../../identity-service/features/namespaces.md#create-custom-namespaces) med den angivna identitetssymbolen (`VALUE`).
>- Importera dina data igen.

Adobe Audience Manager-källan strömmar förstahandsdata som samlats in i Adobe Audience Manager för aktivering i Adobe Experience Platform. Audience Manager-källan importerar två typer av data till Experience Platform:

- **Realtidsdata:** Data som har samlats in i realtid på Audience Manager datainsamlingsserver. Dessa data används i Audience Manager för att fylla i regelbaserade egenskaper och kommer att visas i Experience Platform på kortast möjliga latenstid.
- **Profildata:** Audience Manager använder realtidsdata och onboarddata för att härleda kundprofiler. De här profilerna används för att fylla i identitetsdiagram och egenskaper för segmentimplementeringar.

Audience Manager-källan mappar dessa datatyper till ett XDM-schema (Experience Data Model) och skickar dem sedan till Experience Platform. Realtidsdata skickas som XDM ExperienceEvent-data, medan profildata skickas som enskilda XDM-profildata.

Mer information finns i guiden om att [skapa en Audience Manager-källanslutning i användargränssnittet](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## Vad är Experience Data Model (XDM)?

XDM är en öppet dokumenterad specifikation som tillhandahåller ett standardiserat ramverk genom vilket Experience Platform organiserar kundupplevelsedata.

Genom att följa XDM-standarder kan kundupplevelsedata integreras enhetligt, vilket gör det enklare att leverera data och samla in information.

Mer information om hur XDM används i Experience Platform finns i [XDM-systemöversikten](../../../xdm/home.md). Om du vill veta mer om hur XDM-scheman är strukturerade mellan profiler och händelser läser du [grunderna i schemakomposition](../../../xdm/schema/composition.md).

## XDM-scheman - exempel

Nedan finns exempel på Audience Manager-strukturen som är mappad till XDM ExperienceEvent och XDM Individual Profile i Experience Platform.

### ExperienceEvent - för realtidsdata och inbyggda data

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Individuell XDM-profil - för profildata

![](images/aam-profile-xdm-for-profile-data.png)

Mer information om hur fält mappas från Audience Manager till XDM finns i dokumentationen om [Audience Manager-mappningsfält](./mapping/audience-manager.md).

## Datahantering för Experience Platform

### Datauppsättningar

En datauppsättning är en lagrings- och hanteringskonstruktion för en datainsamling, vanligtvis en tabell, som innehåller ett schema (kolumner) och fält (rader) och som görs tillgängliga via en dataanslutning. Audience Manager data består av realtidsdata, inkommande data och profildata. Om du vill hitta dina Audience Manager-datauppsättningar använder du sökfunktionen i användargränssnittet med de namnkonventioner som anges för varje datatyp.

Audience Manager datamängder är inaktiverade som standard för Profil och användare kan aktivera eller inaktivera datauppsättningar baserat på användningsfall. Vi rekommenderar inte att du inaktiverar datauppsättningar som ska användas för segmentmedlemskap i profilen.

>[!NOTE]
>
>AAM Real-time är den enda datamängden som går till datasjön. Alla andra Audience Manager-datauppsättningar går till [!DNL Profile], om de är aktiverade för [!DNL Profile]. Om de inte är aktiverade för [!DNL Profile], tar de inte emot några data och de visas som tomma.

| Namn på datauppsättning | Beskrivning | Klass |
| --- | --- | --- |
| AAM Real-time | Den här datauppsättningen innehåller data som samlats in med direktträffar på Audience Manager DCS-slutpunkter och identitetskartor för Audience Manager-profiler. Låt den här datauppsättningen vara aktiverad för profilinmatning. | Experience event |
| Profiluppdateringar i realtid för AAM | Med den här datauppsättningen kan ni målinrikta Audience Manager-egenskaper och -segment i realtid. Det innehåller information om Edge regionala routning, kontohantering och segmentmedlemskap. Låt den här datauppsättningen vara aktiverad för profilinmatning. Data visas inte som batchar i datauppsättningen. Du kan aktivera växeln **[!UICONTROL Profile]** för att direkt importera data till profilen. | Post |
| AAM Devices Data | Enhetsdata med ECID och motsvarande segmentimplementeringar samlade i Audience Manager. Data visas inte som batchar i datauppsättningen. Du kan aktivera växeln **[!UICONTROL Profile]** för att direkt importera data till profilen. | Post |
| AAM enhetsprofildata | Används för Audience Manager anslutningsdiagnostik. Data visas inte som batchar i datauppsättningen. Du kan aktivera växeln **[!UICONTROL Profile]** för att direkt importera data till profilen. | Post |
| AAM autentiserade profiler | Den här datauppsättningen innehåller Audience Manager autentiserade profiler. Data visas inte som batchar i datauppsättningen. Du kan aktivera växeln **[!UICONTROL Profile]** för att direkt importera data till profilen. | Post |
| Metadata för AAM-autentiserade profiler | Används för diagnostik av Audience Manager Connector. Data visas inte som batchar i datauppsättningen. Du kan aktivera växeln **[!UICONTROL Profile]** för att direkt importera data till profilen. | Post |
| AAM Devices Data Backfill | Datauppsättning från att hämta in tidigare enhetsdata. Detta innehåller ECID och motsvarande segmentimplementeringar som aggregerats i Audience Manager. Data visas inte som batchar i datauppsättningen. Du kan aktivera växeln **[!UICONTROL Profile]** för att direkt importera data till profilen. | Post |
| Bakgrundsfyllning för autentiserade AAM-profiler | Datauppsättning från att hämta in tidigare autentiserade data. Detta innehåller Audience Manager autentiserade profiler. Data visas inte som batchar i datauppsättningen. Du kan aktivera växeln **[!UICONTROL Profile]** för att direkt importera data till profilen. | Post |

### Anslutningar

Adobe Audience Manager skapar en anslutning i katalogen: Audience Manager Connection. Katalog är det system som används för att lagra och lagra data inom Adobe Experience Platform. En anslutning är ett katalogobjekt som är en kundspecifik instans av anslutningar. Läs [Katalogtjänstöversikt](../../../catalog/home.md) om du vill ha mer information om katalog, anslutningar och anslutningar.

### Segmentpopulation som påverkar profilen

Segmentpopulationsstorlekar har en direkt inverkan på profilnummer när du skickar ett Audience Manager-segment till Experience Platform första gången. Det innebär att om du väljer alla segment kan det potentiellt orsaka profilöverskridningar som överskrider din behörighet för licensanvändning. Experience Platform skiljer också mellan nya data och historiska data för profilinmatning. Ett segment med 100 förstahandsbaserade identiteter skapar 100 profiler. Om populationen i samma segment däremot höjdes till 150 och förtärdes i Experience Platform kommer antalet profiler endast att öka med 50, eftersom det bara finns 50 nya profiler.

Du kan också kontrollera profilanvändningen som ditt konto har tillgängligt via [kontrollpanelen för licensanvändning](../../../dashboards/guides/license-usage.md).

## Vilken fördröjning förväntas för Audience Manager Data på Experience Platform?

| Audience Manager Data | Typ | Latens | Anteckningar |
| --- | --- | --- | --- |
| Realtidsdata | Händelser | &lt;25 minuter | Tiden från att vara infångad på Audience Manager Edge-nod till att vara i datasjön. |
| Realtidsdata | Profiluppdateringar | &lt;10 minuter | Det är dags att lägga in kundprofilen i realtid. |
| Realtid och onboarddata | Profiluppdateringar | 24 till 36 timmar | Tid från att hämtas via DCS/PCS Edge-data och onboarddata, bearbetas till en användarprofil, till att sedan visas i kundprofilen i realtid. För närvarande landar dessa data inte direkt i datasjön. Profilväxling kan aktiveras för datauppsättningar i Audience Manager-profiler så att dessa data kan importeras direkt till kundprofilen i realtid. |
