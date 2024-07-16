---
description: Lär dig hur du använder kontrollpanelen för övervakning för att övervaka data som hämtas från källor.
title: Övervaka dataflöden för källor i användargränssnittet
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: 51f8a8c77518a0b2e9e4b914c891f97433db1ef2
workflow-type: tm+mt
source-wordcount: '1229'
ht-degree: 0%

---

# Övervaka dataflöden för källor i användargränssnittet

>[!IMPORTANT]
>
>Direktuppspelningskällor, som [HTTP API-källan](../../sources/connectors/streaming/http.md), stöds för närvarande inte av kontrollpanelen. För tillfället kan du bara använda kontrollpanelen för att övervaka batchkällor.

Läs det här dokumentet för att lära dig hur du använder kontrollpanelen för att övervaka dina källdata i användargränssnittet i Experience Platform.

## Kom igång {#get-started}

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Dataflöden](../home.md): Dataflöden är en representation av datajobb som flyttar data mellan plattformar. Dataflöden är konfigurerade för olika tjänster, vilket hjälper dig att flytta data från källanslutningar till måldatauppsättningar, till [!DNL Identity] och [!DNL Profile] samt till [!DNL Destinations].
   * [Dataflöden körs](../../sources/notifications.md): Dataflöden är återkommande schemalagda jobb som baseras på frekvenskonfigurationen för valda dataflöden.
* [Källor](../../sources/home.md): Experience Platform tillåter data att hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av plattformstjänster.
* [Identitetstjänst](../../identity-service/home.md): Få en bättre bild av enskilda kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system.
* [Kundprofil i realtid](../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Sandlådor](../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Övervaka källdata med kontrollpanelen

>[!CONTEXTUALHELP]
>id="platform_monitoring_source_ingestion"
>title="Source-intag"
>abstract="Inmatningsvyn i Source innehåller information om dataaktivitetsstatus och mått i sjödatatjänsten, inklusive inmatade och misslyckade poster. Läs måttdefinitionsguiden om du vill veta mer om mått och diagram."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_ingestion"
>title="Information om dataflödeskörning"
>abstract="Källhanteringen innehåller information om dataaktivitetsstatus och mått i sjödatatjänsten, inklusive inmatade och misslyckade poster. Läs måttdefinitionsguiden om du vill veta mer om mått och diagram."
>text="Learn more in documentation"

<!-- In the [Platform UI](https://platform.adobe.com), select **[!UICONTROL Monitoring]** from the left navigation to access the [!UICONTROL Monitoring] dashboard. The [!UICONTROL Monitoring] dashboard contains metrics and information on all sources dataflows, including insights into the health of data traffic from a source to [!DNL Identity Service], and to [!DNL Profile].

At the center of the dashboard is the [!UICONTROL Source ingestion] panel, which contains metrics and graphs that display data on records ingested and records failed. -->

I kontrollpanelen väljer du [!UICONTROL Sources] i huvudrubriken för att uppdatera instrumentpanelen med en visning av källans dataflödeshastighet.

![Kontrollpanelen med källkortet valt.](../assets/ui/monitor-sources/sources.png)

Diagrammet [!UICONTROL Ingestion rate] visar dataöverföringshastigheten baserat på den konfigurerade tidsramen. Som standard visar kontrollpanelen hur många gånger de senaste 24 timmarna har fått i sig det. Anvisningar om hur du konfigurerar tidsramen finns i guiden [Konfigurera tidsbildruta för övervakning](monitor.md#configure-monitoring-time-frame).

Diagrammet är aktiverat för visning som standard. Om du vill dölja diagrammet väljer du **[!UICONTROL Metrics and graphs]** för att inaktivera växlingen och dölja diagrammet.

![Mätdiagrammet för intagsfrekvens.](../assets/ui/monitor-sources/metrics-graph.png)

I den nedre delen av kontrollpanelen visas en tabell som visar den aktuella mätrapporten för alla befintliga källdata.

![Kontrollpanelens mättabell.](../assets/ui/monitor-sources/metrics-table.png)

| Mätvärden | Beskrivning |
| --- | --- |
| Mottagna poster | Det totala antalet poster som tagits emot från källan. |
| Insamlade poster | Det totala antalet poster som har importerats till datasjön. |
| Överhoppade poster | Det totala antalet poster som hoppats över. |
| Misslyckade poster | Det totala antalet poster som inte kunde importeras på grund av fel. |
| Fakturerad frekvens | Procentandelen poster som har importerats baserat på det totala antalet mottagna poster. |
| Totalt antal misslyckade dataflöden | Totalt antal misslyckade dataflöden. |

{style="table-layout:auto"}

Du kan filtrera dina data ytterligare med hjälp av alternativen ovan i mättabellen:

| Filtreringsalternativ | Beskrivning |
| --- | --- |
| Sök | Använd sökfältet för att filtrera vyn till en enda källtyp. |
| Källor | Välj **[!UICONTROL Sources]** om du vill filtrera vyn och visa måttdata per källtyp. Det här är standardvisningen som kontrollpanelen använder. |
| Dataflöden | Välj **[!UICONTROL Dataflows]** om du vill filtrera vyn och visa mätdata per dataflöde. |
| Visa endast fel | Välj **[!UICONTROL Show failures only]** om du vill filtrera vyn och endast visa dataflöden som rapporterade misslyckade inläsningar. |
| Mina källor | Du kan filtrera vyn ytterligare genom att använda listrutan [!UICONTROL My sources]. Använd listrutan för att filtrera vyn efter kategori. Du kan också välja **[!UICONTROL All sources]** om du vill visa mått på alla eller källorna, eller välja **[!UICONTROL My sources]** om du bara vill visa de källor som du har ett motsvarande konto med. |

{style="table-layout:auto"}

Om du vill övervaka data som importeras i ett specifikt dataflöde väljer du filterikonen ![filter](../assets/ui/monitor-sources/filter.png) bredvid en källa.

![Övervaka ett specifikt dataflöde genom att välja filterikonen bredvid en viss källa.](../assets/ui/monitor-sources/monitor-dataflow.png)

Måtttabellen uppdateras till en tabell med aktiva dataflöden som motsvarar den källa du valde. Under det här steget kan du visa ytterligare information om dataflödena, inklusive deras motsvarande datauppsättning och datatyp, samt en tidsstämpel som anger när de senast var aktiva.

Om du vill inspektera ett dataflöde ytterligare väljer du filterikonen ![filter](../assets/ui/monitor-sources/filter.png) bredvid ett dataflöde.

![Dataflödestabellen i kontrollpanelen.](../assets/ui/monitor-sources/select-dataflow.png)

Därefter kommer du till ett gränssnitt som visar alla dataflödeskörningsiterationer för det dataflöde som du har valt.

Körningar av dataflöde representerar en instans av körning av dataflöde. Om ett dataflöde till exempel är schemalagt att köras varje timme kl. 9.00, 10.00 och 11.00 har du tre instanser av en flödeskörning. Flödeskörningar är specifika för just din organisation.

Om du vill inspektera mätvärden för en viss dataflödeskörning väljer du filterikonen ![filter](../assets/ui/monitor-sources/filter.png) bredvid dataflödet.

![Dataflödets körningsmåttsida.](../assets/ui/monitor-sources/dataflow-page.png)

Använd informationssidan för dataflödeskörning för att visa mått och information om den valda körningen.

![Informationssidan för dataflödeskörning.](../assets/ui/monitor-sources/dataflow-run-details.png)

| Information om dataflödeskörning | Beskrivning |
| --- | --- |
| Insamlade poster | Det totala antalet poster som har importerats från dataflödeskörningen. |
| Misslyckade poster | Det totala antalet poster som inte har importerats på grund av fel i dataflödeskörningen. |
| Totalt antal filer | Det totala antalet filer i dataflödeskörningen. |
| Storlek på data | Den totala datastorleken i dataflödeskörningen. |
| Körnings-ID för dataflöde | ID för dataflödets körningsiteration. |
| Organisations-ID | ID:t för organisationen där dataflödeskörningen skapades. |
| Status | Status för dataflödeskörningen. |
| Start för dataflödeskörning | En tidsstämpel som anger när dataflödet startades. |
| Dataflödeskörning - slut | En tidsstämpel som anger när dataflödets körning avslutades. |
| Datauppsättning | Den datauppsättning som används för att skapa dataflödet. |
| Datatyp | Den typ av data som fanns i dataflödet. |
| Delvis intag | Partiell batchförbrukning är möjligheten att importera data som innehåller fel, upp till ett visst konfigurerbart tröskelvärde. Med den här funktionen kan du importera alla korrekta data till Experience Platform, medan alla felaktiga data batchas separat med information om varför de är ogiltiga. Du kan aktivera partiell inmatning när dataflödet skapas. |
| Feldiagnostik | Feldiagnostik instruerar källan att skapa feldiagnostik som du kan referera till senare när du övervakar datauppsättningsaktiviteten och dataflödesstatusen. Du kan aktivera feldiagnostik när dataflödet skapas. |
| Sammanfattning av fel | Om ett dataflöde inte kan köras visas en felkod och en beskrivning i felsammanfattningen för att sammanfatta varför körningen misslyckades. |

{style="table-layout:auto"}

Om ditt dataflöde rapporterar fel kan du rulla nedåt till sidans nederkant med gränssnittet [!UICONTROL Dataflow run errors].

Använd avsnittet [!UICONTROL Records failed] om du vill visa mätvärden för poster som inte har importerats på grund av fel. Om du vill visa en omfattande felrapport väljer du **[!UICONTROL Preview error diagnostics]**. Om du vill hämta en kopia av feldiagnostiken och ditt filmanifest väljer du **[!UICONTROL Download]** och kopierar sedan det exempel-API-anrop som ska användas med [!DNL Data Access] API.

>[!NOTE]
>
>Du kan bara använda feldiagnostik om funktionen aktiverades när du skapade källanslutningen.

![Dataflödets felpanel körs.](../assets/ui/monitor-sources/errors.png)

## Nästa steg {#next-steps}

Genom att följa den här självstudiekursen har du övervakat inmatningsdataflödet från källnivån med hjälp av kontrollpanelen **[!UICONTROL Monitoring]**. Du har också identifierat fel som bidrog till att dataflödena misslyckades under importen. Mer information finns i följande dokument:

* [Övervakar identitetsdata](./monitor-identities.md).
* [Övervakar profildata](./monitor-profiles.md).
