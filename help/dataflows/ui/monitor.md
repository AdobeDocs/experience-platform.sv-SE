---
title: Översikt över kontrollpanelen för övervakning
description: Lär dig hur du använder kontrollpanelen för övervakning i användargränssnittet i Adobe Experience Platform
exl-id: 06ea5380-d66e-45ae-aa02-c8060667da4e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 0%

---

# Översikt över kontrollpanelen för övervakning

Använd kontrollpanelen i Adobe Experience Platform-användargränssnittet för att se hur data rör sig från intag till aktivering. Med kontrollpanelen kan du

* Övervaka dataresan från Sources, Identity Service, Real-Time Customer Profile, Audiences och slutligen i Destinations.
* Visa olika mått och statusvärden beroende på i vilken fas dina data befinner sig.
* Filtrera datarätningsvyn efter datatyp.

Kontrollpanelen har stöd för vyn av flera olika datatyper:

* **Kund och konto**: Kunddata refererar till de data som används i [Real-Time Customer Data Platform](../../rtcdp/home.md), medan kontodata refererar till [kontoprofildata](../../rtcdp/accounts/account-profile-overview.md) som är tillgängliga när du prenumererar på [Real-Time CDP, B2B edition](../../rtcdp/b2b-overview.md). Om din Real-Time CDP-licens inte innehåller Real-Time CDP, B2B edition, kan du bara använda kontrollpanelen för att övervaka kunddata.
* **Prospekt**: [Prospekteringsprofiler](../../profile/ui/prospect-profile.md) används för att representera personer som ännu inte har engagerat ditt företag men som du vill kontakta. Med profiler för potentiella kunder kan ni komplettera era kundprofiler med attribut från betrodda tredjepartspartners. Du måste ha licens för Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime och Real-Time CDP Ultimate för att kunna se datatypen för den potentiella kunden.
* **Berikning av kontoprofiler**: Med kontoprofiler kan du sammanställa kontoinformation från flera källor. Du måste ha licens för Real-Time CDP, B2B edition för att kunna övervaka kontouppgifter.

Läs det här dokumentet för att lära dig hur du använder kontrollpanelen för att övervaka hur dina data överförs mellan olika Experience Platform-tjänster.

## Kom igång

Dokumentet kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Dataflöden](../home.md): Dataflöden är representationer av datajobb som flyttar data mellan Experience Platform. Du kan använda källarbetsytan för att skapa dataflöden som importerar data från en viss källa till Experience Platform.
* [Källor](../../sources/home.md): Använd källor i Experience Platform för att importera data från ett Adobe-program eller en datakälla från tredje part.
* [Identitetstjänst](../../identity-service/home.md): Få en bättre bild av enskilda kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system.
* [Kundprofil i realtid](../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Segmentering](../../segmentation/home.md): Använd segmenteringstjänsten för att skapa segment och målgrupper utifrån kundprofildata i realtid.
* [Destinationer](../../destinations/home.md): Destinationer är färdiga integreringar med vanliga program som möjliggör smidig aktivering av data från Experience Platform för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.

## Övervaka instrumentpanelsguide

I Experience Platform-gränssnittet väljer du **[!UICONTROL Monitoring]** under [!UICONTROL Data Management] i den vänstra navigeringen.

![Kontrollpanelen i Experience Platform-gränssnittet.](../assets/ui/monitor-overview/monitoring.png)

Välj **[!UICONTROL Data Type]** och använd sedan listrutan för att välja vilken typ av data du vill visa. Datatyperna definieras av XDM-schemaklasser (Experience Data Model) för att säkerställa att deras data följer ett standardformat när de hämtas till Experience Platform. Mer information finns i följande dokumentation:

* [B2B-kontodatatyp](../../rtcdp/b2b-tutorial.md)
* [Datatyp för potentiell kund](../../rtcdp/partner-data/prospecting.md)

Du kan filtrera vyn baserat på följande datatyper:

>[!BEGINTABS]

>[!TAB Alla]

Välj **[!UICONTROL All]** om du vill uppdatera instrumentpanelen och visa mått på alla data som har importerats till Experience Platform under en viss period.

![Övervakningens datatyp är inställd på &quot;Alla&quot;.](../assets/ui/monitor-overview/all.png)

>[!TAB Kund och konto]

Välj **[!UICONTROL Customer & Account]** om du vill uppdatera instrumentpanelen och visa mått på kund- och kontodata som har importerats till Experience Platform under en viss period.

![Övervakningens datatyp har angetts till Kund och konto.](../assets/ui/monitor-overview/customer-account.png)

>[!TAB Prospekt]

Välj **[!UICONTROL Prospect]** om du vill uppdatera instrumentpanelen och visa statistik om prospekteringsdata som har importerats till Experience Platform under en viss period. **Obs!**: Du kan bara visa datatypsaktiviteter för potentiella kunder om du är [berättigad till data för potentiella kunder](../../rtcdp/partner-data/prospecting.md).

![Övervakningens datatyp har angetts till Prospect.](../assets/ui/monitor-overview/prospect.png)

>[!TAB Berikning av kontoprofil]

Välj **[!UICONTROL Account profile enrichment]** om du vill uppdatera din instrumentpanel och visa mått på profilberikningsdata. **Obs!**: Du kan bara visa anrikningsvärden för kontoprofiler om du är berättigad till [B2B-data](../../rtcdp/b2b-tutorial.md).

![Övervakningens datatyp har angetts till &quot;Berikning av kontoprofil&quot;.](../assets/ui/monitor-overview/account-profile-enrichment.png)

>[!ENDTABS]

Använd panelens översta huvud för att få en upplevelse av övervakning över flera tjänster. Du kan filtrera mätvärden och diagram genom att välja vilket funktionskort du vill i datakategorihuvudet.

>[!BEGINTABS]

>[!TAB Källor]

Välj **[!UICONTROL Sources]** om du vill visa mätvärden för dina källors inmatningsfrekvens. Läs guiden om [övervakning av källdata](monitor-sources.md) om du vill ha mer information.

![Kontrollpanelen i gränssnittet med källkortet markerat.](../assets/ui/monitor-overview/sources.png)

>[!TAB Identiteter]

Välj **[!UICONTROL Identities]** om du vill visa hur lyckad bearbetningen av dina identitetsdata är. Läs guiden om [övervakning av identitetsdata](monitor-identities.md) om du vill ha mer information.

![Kontrollpanelen i gränssnittet med identitetskortet valt.](../assets/ui/monitor-overview/identities.png)

>[!TAB Profiler]

Välj **[!UICONTROL Profiles]** om du vill visa hur framgångsrik bearbetningen av dina profildata är. Läs guiden om [övervakning av profildata](monitor-profiles.md) om du vill ha mer information.

![Kontrollpanelen i gränssnittet med profilkortet markerat.](../assets/ui/monitor-overview/profiles.png)

>[!TAB Publiker]

Välj **[!UICONTROL Audiences]** om du vill visa mätvärden för dina målgrupper och segmenteringsjobb. Läs guiden [Övervaka målgruppsdata](monitor-audiences.md) om du vill ha mer information.

![Kontrollpanelen i användargränssnittet med målgruppskortet markerat.](../assets/ui/monitor-overview/audiences.png)

>[!TAB Mål]

Välj **[!UICONTROL Destinations]** om du vill visa mätvärden för [!UICONTROL Streaming activate rate] och [!UICONTROL Batch failed dataflow runs]. Läs guiden om [övervakning av måldata](monitor-destinations.md) om du vill ha mer information.

![Kontrollpanelen i gränssnittet med målkortet markerat.](../assets/ui/monitor-overview/destinations.png)

>[!ENDTABS]

### Konfigurera tidsram för övervakning {#configure-monitoring-time-frame}

Som standard visar kontrollpanelen mätvärden på data som importerats under de senaste 24 timmarna. Välj **[!UICONTROL Last 24 hours]** om du vill uppdatera tidsramen.

![Kontrollpanelen i gränssnittet med tidskonfigurationen vald.](../assets/ui/monitor-overview/select-time.png)

Du kan konfigurera en ny tidsram för datarapporteringen i den dialogruta som visas. Du kan skapa en anpassad tidsram eller välja ett alternativ i listan med förkonfigurerade alternativ:

* [!UICONTROL Last 24 hours]
* [!UICONTROL Last 7 days]
* [!UICONTROL Last 30 days]

När du är klar väljer du **[!UICONTROL Apply]**.

![Popup-fönstret för konfiguration av tidsbildrutor på kontrollpanelen.](../assets/ui/monitor-overview/update-time.png)

## Nästa steg

Genom att läsa det här dokumentet kan du nu navigera genom kontrollpanelen i användargränssnittet. Mer information om hur du övervakar data för en viss Experience Platform-tjänst finns i dokumentationen nedan:

* [Övervaka källdata](monitor-sources.md).
* [Övervaka identitetsdata](monitor-identities.md).
* [Övervaka profildata](monitor-profiles.md).
* [Övervaka målgruppsdata](monitor-audiences.md).
* [Övervaka måldata](monitor-destinations.md).
