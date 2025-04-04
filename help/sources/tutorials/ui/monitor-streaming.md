---
keywords: Experience Platform;hem;populära ämnen;bildskärmskonton;bildskärmsdataflöden;dataflöden
description: Source-anslutningar i Adobe Experience Platform gör det möjligt att importera externa data på schemalagd basis. I den här självstudiekursen beskrivs hur du övervakar direktuppspelade dataflöden från arbetsytan Källor.
title: Övervaka dataflöden för strömningskällor i användargränssnittet
exl-id: b080e398-e71f-40bd-aea1-7ea3ce86b55d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 0%

---

# Övervaka dataflöden för strömningskällor i användargränssnittet

I den här självstudien beskrivs stegen för att övervaka dataflöden för direktuppspelningskällor med arbetsytan [!UICONTROL Sources].

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Dataflöden](../../../dataflows/home.md): Dataflöden är en representation av datajobb som flyttar data mellan Experience Platform. Dataflöden är konfigurerade för olika tjänster, vilket hjälper dig att flytta data från källanslutningar till måldatauppsättningar, till [!DNL Identity] och [!DNL Profile] samt till [!DNL Destinations].
   * [Dataflöden körs](../../notifications.md): Dataflöden är återkommande schemalagda jobb som baseras på frekvenskonfigurationen för valda dataflöden.
* [Källor](../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Övervaka dataflöden för strömningskällor

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i [!UICONTROL Sources]. På skärmen [!UICONTROL Catalog] visas en mängd olika källor som du kan skapa ett konto med.

Om du vill visa befintliga dataflöden för direktuppspelningskällor väljer du **[!UICONTROL Dataflows]** i den övre rubriken.

![katalog](../../images/tutorials/monitor-streaming/catalog.png)

Sidan [!UICONTROL Dataflows] innehåller en lista över alla befintliga dataflöden i organisationen, inklusive information om deras källdata, kontonamn och dataflödeskörningsstatus.

Välj namnet på det dataflöde som du vill visa.

![dataflöden](../../images/tutorials/monitor-streaming/dataflows.png)

Följande tabell innehåller mer information om status för dataflödeskörning:

| Status | Beskrivning |
| ------ | ----------- |
| Slutförd | Statusen `Completed` anger att alla poster för motsvarande dataflödeskörning har bearbetats inom en timmes period. En `Completed`-status kan fortfarande innehålla fel i dataflödeskörningar. |
| Lyckades | Statusen `Success` anger att alla poster för motsvarande dataflödeskörning har bearbetats inom en timmes period och att inga fel uppstod under dataflödeskörningen. |
| Bearbetar | Statusen `Processing` anger att ett dataflöde ännu inte är aktivt. Denna status inträffar ofta omedelbart efter att ett nytt dataflöde har skapats. |
| Fel | Statusen `Error` indikerar att aktiveringsprocessen för ett dataflöde har avbrutits. |
| Inga körningar | Statusen `No runs` anger att dataflödet skapades men att inga dataflödeskörningar startades. |

På sidan [!UICONTROL Dataflow Activity] visas specifik information om ditt dataflöde för direktuppspelning. Den översta banderollen innehåller det kumulativa antalet poster som importerats och poster som misslyckats för alla strömmande dataflöden i det valda datumintervallet.

![dataflödesaktivitet](../../images/tutorials/monitor-streaming/dataflow-activity.png)

Som standard innehåller de data som visas mängder av konsumtion från de senaste sju dagarna. Välj **[!UICONTROL Last 7 days]** om du vill justera tidsramen för de poster som visas.

Ett kalender-popup-fönster visas med alternativ för alternativa tidsramar för inmatning. Du kan konfigurera bildrutan för körtid för dataflöde så att flödet från de föregående sju dagarna eller de senaste 30 dagarna visas. Du kan också konfigurera den interaktiva kalendern så att den anger en anpassad tidsram. När du är klar väljer du **[!UICONTROL Apply]**.

![kalender](../../images/tutorials/monitor-streaming/calendar.png)

Den nedre halvan av sidan visar information om antalet poster som tagits emot, importerats och misslyckats, per flödeskörning. Varje flödeskörning registreras i ett timfönster.

![dataflöde-run](../../images/tutorials/monitor-streaming/dataflow-run.png)

### Mätvärden för dataflödeskörning {#dataflow-run-metrics}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_received"
>title="Mottagna poster"
>abstract="Måttet Mottagna poster anger det totala antalet poster som tagits emot i dataflödet."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_ingested"
>title="Insamlade poster"
>abstract="Posterna i fältet Ingrederat anger det totala antalet poster som har importerats till datasjön."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_failed"
>title="Misslyckade poster"
>abstract="Måttet Poster misslyckades anger det totala antalet poster som inte har importerats till datasjön på grund av fel i data."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_warnings"
>title="Poster med varningar"
>abstract="Poster med varningar anger det totala antalet poster som har importerats med mappningsomformningsvarningar. Alla mappartransformeringsfel rapporteras som varningar och rader som delvis har importerats anses vara lyckade med en varning"
>text="Learn more in documentation"

Varje enskild dataflödeskörning visar följande information:

* **[!UICONTROL Dataflow run start]**: Den tid som dataflödet körs från.
* **[!UICONTROL Processing time]**: Den tid det tog för dataflödet att bearbeta.
* **[!UICONTROL Records Received]**: Det totala antalet poster som tagits emot i dataflödet från en källkoppling.
* **[!UICONTROL Records Ingested]**: Det totala antalet poster som har importerats till [!DNL Data Lake].
* **[!UICONTROL Records with Warnings]**: Det totala antalet poster med varningar som importerats. Alla mappartransformeringsfel rapporteras som varningar och rader som är delvis inkapslade markeras som `success` med en varning. **Obs!**: Stöd för inmatning av poster med varningar är bara tillgängligt för direktuppspelningskällor.
* **[!UICONTROL Records Failed]**: Antalet poster som inte har importerats till [!DNL Data Lake] på grund av datafel.
* **[!UICONTROL Ingestion Rate]**: Antal poster som har importerats till [!DNL Data Lake]. Det här måttet gäller när [!UICONTROL Partial Ingestion] är aktiverat.
* **[!UICONTROL Status]**: Representerar det tillstånd som dataflödet är i: [!UICONTROL Completed] eller [!UICONTROL Processing]. [!UICONTROL Completed] betyder att alla poster för motsvarande dataflödeskörning bearbetades inom en timma. [!UICONTROL Processing] betyder att dataflödeskörningen inte har slutförts än.

Sidan [!UICONTROL Dataflow run overview] innehåller ytterligare information om dataflödet, till exempel motsvarande körnings-ID för dataflöde, måldatauppsättning och organisations-ID.

En flödeskörning med fel innehåller även panelen [!UICONTROL Dataflow run errors], som visar det specifika fel som ledde till att körningen misslyckades samt det totala antalet poster som misslyckades.

![dataflow-run-overview](../../images/tutorials/monitor-streaming/dataflow-run-overview.png)

### Visa poster med varningar {#warnings}

[!UICONTROL Records with warnings] visar en lista med mappartransformeringsvarningar som inträffade under flödeskörningen. Rader som är delvis inkapslade betraktas som lyckade och läggs till med varningar om det finns några mappningsomformningsfel.

Som standard betraktas alla mappningsomformningsfel som varningar, förutom om de är något av följande:

* Syntaxfel
* Referenser till attribut som inte finns
* Felmatchning av XDM-datatyper

Välj **[!UICONTROL Preview error diagnostics]** om du vill visa feldiagnostik.

![records-with-warnings](../../images/tutorials/monitor-streaming/records-with-warnings.png)

I fönstret [!UICONTROL Error diagnostics preview] kan du förhandsgranska upp till 100 fel och/eller varningar för dataflödeskörningen. Härifrån kan du även hämta manifestet för misslyckade inmatningar för mer information med hjälp av API:t [!DNL Data Access].

![diagnostik](../../images/tutorials/monitor-streaming/diagnostics.png)

## Nästa steg

Genom att följa den här självstudiekursen har du använt arbetsytan [!UICONTROL Sources] för att övervaka dina dataflöden för direktuppspelning och identifiera de fel som ledde till eventuella felaktiga dataflöden. Mer information finns i följande dokument:

* [Översikt över källor](../../home.md)
* [Översikt över dataflöden](../../../dataflows/home.md)
