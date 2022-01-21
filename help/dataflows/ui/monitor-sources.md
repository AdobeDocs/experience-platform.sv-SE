---
keywords: Experience Platform;hem;populära ämnen;övervaka konton;övervaka dataflöden;dataflöden;källor
description: I den här självstudiekursen beskrivs hur du övervakar dataflödet med hjälp av både aggregerad övervakningsvy och övervakning mellan tjänster.
solution: Experience Platform
title: Övervaka dataflöden för källor i användargränssnittet
topic-legacy: overview
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: 241deb93b3500139b79425a4da79258670e044a8
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 0%

---

# Övervaka dataflöden för källor i användargränssnittet

>[!IMPORTANT]
>
>Direktuppspelningskällor, som [HTTP-API-källa](../../sources/connectors/streaming/http.md) stöds för närvarande inte av kontrollpanelen för övervakning. För tillfället kan du bara använda kontrollpanelen för att övervaka batchkällor.

I Adobe Experience Platform hämtas data från en mängd olika källor, som analyseras i Experience Platform och aktiveras till en mängd olika destinationer. Plattformen gör processen att spåra detta potentiellt icke-linjära dataflöde enklare genom att tillhandahålla genomskinlighet med dataflöden.

Kontrollpanelen ger dig en visuell representation av resan för ett dataflöde. Du kan använda en aggregerad övervakningsvy och navigera lodrätt från källnivån, till ett dataflöde och till ett dataflöde, så att du kan visa motsvarande mått som bidrar till ett dataflödes framgång eller fel. Du kan också använda kontrollpanelens kapacitet för övervakning över flera tjänster för att övervaka ett dataflödes resa från en källa till [!DNL Identity Service]och till [!DNL Profile].

I den här självstudiekursen beskrivs hur du övervakar dataflödet med hjälp av både aggregerad övervakningsvy och övervakning mellan tjänster.

## Komma igång {#getting-started}

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Dataflöden](../home.md): Dataflöden är en representation av datajobb som flyttar data mellan plattformar. Dataflöden konfigureras över olika tjänster, vilket hjälper dig att flytta data från källanslutningar till måldatauppsättningar till [!DNL Identity] och [!DNL Profile]och till [!DNL Destinations].
   * [Dataflödeskörningar](../../sources/notifications.md): Dataflödeskörningar är återkommande schemalagda jobb som baseras på frekvenskonfigurationen för valda dataflöden.
* [Källor](../../sources/home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster.
* [Identitetstjänst](../../identity-service/home.md): Få en bättre bild av enskilda kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system.
* [Kundprofil i realtid](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Sandlådor](../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

## Sammanställd övervakningsvy {#aggregated-monitoring-view}

>[!CONTEXTUALHELP]
>id="platform_monitoring_source_ingestion"
>title="Intag av källa"
>abstract="Källhanteringen innehåller information om dataaktivitetsstatus och mått i sjödatatjänsten, inklusive inmatade och misslyckade poster. Läs måttdefinitionsguiden om du vill veta mer om mått och diagram."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_ingestion"
>title="Information om dataflödeskörning"
>abstract="Källhanteringen innehåller information om dataaktivitetsstatus och mått i sjödatatjänsten, inklusive inmatade och misslyckade poster. Läs måttdefinitionsguiden om du vill veta mer om mått och diagram."
>text="Learn more in documentation"

I [Plattformsgränssnitt](https://platform.adobe.com), markera **[!UICONTROL Monitoring]** från vänster navigering för att komma åt [!UICONTROL Monitoring] kontrollpanel. The [!UICONTROL Monitoring] Instrumentpanelen innehåller mätvärden och information om alla källdata, dataflöden, inklusive insikter om datatrafikens hälsa från en källa till [!DNL Identity Service]och till [!DNL Profile].

Mitten av kontrollpanelen är [!UICONTROL Source ingestion] som innehåller mått och diagram som visar data för inmatade poster och poster misslyckades.

![monitorpanel](../assets/ui/monitor-sources/monitoring-dashboard.png)

Som standard innehåller de data som visas mängder av konsumtion från de senaste 24 timmarna. Välj **[!UICONTROL Last 24 hours]** för att justera tidsramen för de poster som visas.

![ändringsdatum](../assets/ui/monitor-sources/change-date.png)

Ett kalender-popup-fönster visas med alternativ för alternativa tidsramar för inmatning. Välj **[!UICONTROL Last 30 days]** och sedan markera **[!UICONTROL Apply]**

![adjust-time-frame](../assets/ui/monitor-sources/adjust-timeframe.png)

Diagrammen är aktiverade som standard och du kan inaktivera dem för att utöka listan med källor nedan. Välj **[!UICONTROL Metrics and graphs]** om du vill inaktivera diagrammen.

![mätvärden](../assets/ui/monitor-sources/metrics-graphs.png)

| Intag av källa | Beskrivning |
| ---------------- | ----------- |
| [!UICONTROL Records ingested ] | Det totala antalet poster som har importerats. |
| [!UICONTROL Records failed] | Det totala antalet poster som inte har importerats på grund av datafel. |
| [!UICONTROL Total failed dataflows] | Det totala antalet dataflöden med en `failed` status. |

I listan över källinmatningar visas alla källor som innehåller minst ett befintligt konto. Listan innehåller även information om varje källas intag, antalet misslyckade poster och det totala antalet misslyckade dataflöden baserat på den tidsram som du tillämpade.

![källintag](../assets/ui/monitor-sources/source-ingestion.png)

Om du vill sortera igenom listan med källor väljer du **[!UICONTROL My sources]** och välj sedan önskad kategori i listrutan. Om du till exempel vill fokusera på molnlagring väljer du  **[!UICONTROL Cloud storage]**

![sortera efter kategori](../assets/ui/monitor-sources/sort-by-category.png)

Om du vill visa alla befintliga dataflöden för alla källor väljer du **[!UICONTROL Dataflows]**.

![view-all-dataflows](../assets/ui/monitor-sources/view-all-dataflows.png)

Du kan också ange en källa i sökfältet för att isolera en källa. När du har identifierat källan väljer du filterikonen ![filter](../assets/ui/monitor-sources/filter.png) bredvid den och se en lista över de aktiva dataflödena.

![sök](../assets/ui/monitor-sources/search.png)

En lista över dataflöden visas. Om du vill begränsa listan och fokusera på dataflöden med fel väljer du **[!UICONTROL Show failures only]**.

![endast visa-fel](../assets/ui/monitor-sources/show-failures-only.png)

Leta reda på det dataflöde som du vill övervaka och välj sedan filterikonen ![filter](../assets/ui/monitor-sources/filter.png) bredvid det om du vill ha mer information om körningsstatus.

![dataflöde](../assets/ui/monitor-sources/dataflow.png)

På dataflödets körningssida visas information om startdatum, datastorlek, status samt behandlingstid för dataflödet. Markera filterikonen ![filter](../assets/ui/monitor-sources/filter.png) bredvid starttiden för dataflödet för att se information om dataflödets körning.

![dataflow-run-start](../assets/ui/monitor-sources/dataflow-run-start.png)

The [!UICONTROL Dataflow run details] på sidan visas information om dataflödets metadata, partiell inmatningsstatus och felsammanfattning. Felsammanfattningen innehåller det specifika felet på den översta nivån som visar i vilket steg som inmatningsprocessen påträffade ett fel.

Bläddra nedåt om du vill se mer specifik information om felet.

![dataflöde-run-details](../assets/ui/monitor-sources/dataflow-run-details.png)

The [!UICONTROL Dataflow run errors] visas det specifika fel- och felkoden som resulterade i att dataflödet inte kunde hämtas. I det här scenariot uppstod ett transformeringsfel för mapparen, vilket resulterade i ett fel på 24 poster.

Välj **[!UICONTROL Files]** för mer information.

![dataflow-run-errors](../assets/ui/monitor-sources/dataflow-run-errors.png)

The [!UICONTROL Files] -panelen innehåller information om filens namn och sökväg.

Välj **[!UICONTROL Preview error diagnostics]**.

![filer](../assets/ui/monitor-sources/files.png)

The [!UICONTROL Error diagnostics preview] visas och en förhandsgranskning av upp till 100 fel i dataflödet visas. Du kan välja **[!UICONTROL Download]** för att hämta ett skrivkommando, som sedan gör att du kan hämta feldiagnostiken.

När du är klar väljer du **[!UICONTROL Close]**

![feldiagnostik](../assets/ui/monitor-sources/error-diagnostics.png)

Du kan använda det synliga systemet i det övre huvudet för att navigera tillbaka till [!UICONTROL Monitoring] kontrollpanel. Välj **[!UICONTROL Run start: 2/14/2021, 9:47 PM]** för att gå tillbaka till föregående sida och sedan markera **[!UICONTROL Dataflow: Loyalty Data Ingestion Demo - Failed]** för att återgå till dataflödessidan.

![breadcrumbs](../assets/ui/monitor-sources/breadcrumbs.png)

## Övervakning över flera tjänster {#cross-service-monitoring}

Den övre delen av kontrollpanelen innehåller en representation av intagsflödet från källnivån till [!DNL Identity Service]och till [!DNL Profile]. Varje cell innehåller en punktmarkör som anger att det finns fel som inträffade vid det aktuella intaget. En grön punkt innebär ett felfritt intag, medan en röd punkt betyder att ett fel uppstod i just det steget.

![övervakning mellan tjänster](../assets/ui/monitor-sources/cross-service-monitoring.png)

Leta reda på ett lyckat dataflöde på dataflödessidan och välj filterikonen ![filter](../assets/ui/monitor-sources/filter.png) bredvid det för att se information om dataflödets körning.

![dataflöde-success](../assets/ui/monitor-sources/dataflow-success.png)

The [!UICONTROL Source ingestion] sidan innehåller information som bekräftar att dataflödet har överförts. Härifrån kan du börja övervaka ditt dataflödes resa från källnivå till [!DNL Identity Service]och sedan [!DNL Profile].

Välj **[!UICONTROL Identities]** för att se intag i [!UICONTROL Identities] stage.

![källor](../assets/ui/monitor-sources/sources.png)

### [!DNL Identity] mått {#identity-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_identity_processing"
>title="Identitetsbearbetning"
>abstract="Identitetsbearbetning innehåller information om poster som importerats till identitetstjänsten, inklusive antalet identiteter som lagts till, diagram som skapats och diagram som uppdaterats. Läs måttdefinitionsguiden om du vill veta mer om mått och diagram."
>text="Learn more in documentation"

The [!UICONTROL Identity processing] sidan innehåller information om poster som har importerats till [!DNL Identity Service], inklusive antal tillagda identiteter, skapade diagram och uppdaterade diagram.

Markera filterikonen ![filter](../assets/ui/monitor-sources/filter.png) bredvid starttiden för dataflödet för att se mer information om [!DNL Identity] dataflödeskörning.

![identiteter](../assets/ui/monitor-sources/identities.png)

| Identitetsmått | Beskrivning |
| ---------------- | ----------- |
| [!UICONTROL Records received] | Antalet poster som tagits emot från [!DNL Data Lake]. |
| [!UICONTROL Records failed] | Antalet poster som inte har importerats till plattformen på grund av datafel. |
| [!UICONTROL Records skipped] | Antalet poster som har importerats, men inte [!DNL Identity Service] därför att det bara fanns en identifierare i postraden. |
| [!UICONTROL Records ingested] | Antalet poster som inhämtats till [!DNL Identity Service]. |
| [!UICONTROL Total records] | Totalt antal poster, inklusive poster som misslyckats, poster som hoppats över. [!DNL Identities] och dubblerade poster. |
| [!UICONTROL Identities added] | Antalet nya nettoidentifierare som lagts till i [!DNL Identity Service]. |
| [!UICONTROL Graphs created] | Antalet nya identitetsdiagram som skapas i [!DNL Identity Service]. |
| [!UICONTROL Graphs updated] | Antalet befintliga identitetsdiagram som uppdaterats med nya kanter. |
| [!UICONTROL Failed dataflow runs] | Antalet misslyckade dataflödeskörningar. |
| [!UICONTROL Processing time] | Tidsstämpeln från det att du har fått in det hela till det färdiga. |
| [!UICONTROL Status] | Definierar den övergripande statusen för ett dataflöde. Möjliga statusvärden är: <ul><li>`Success`: Anger att ett dataflöde är aktivt och att data hämtas enligt det schema som det tillhandahölls.</li><li>`Failed`: Anger att aktiveringsprocessen för ett dataflöde har avbrutits på grund av fel. </li><li>`Processing`: Anger att dataflödet ännu inte är aktivt. Denna status inträffar ofta omedelbart efter att ett nytt dataflöde har skapats.</li></ul> |

The [!UICONTROL Dataflow run details] sidan visar mer information om [!DNL Identity] dataflödeskörning, inklusive dess IMS Org ID och dataflödeskörnings-ID. På den här sidan visas även motsvarande felkod och felmeddelande från [!DNL Identity Service], om det uppstår några fel i intagsprocessen.

Välj **[!UICONTROL Run start: 2/14/2021, 9:47 PM]** för att återgå till föregående sida.

![identities-dataflow-run](../assets/ui/monitor-sources/identities-dataflow-run.png)

Från [!UICONTROL Identity processing] sida, markera **[!UICONTROL Profiles]** för att se status för registrering i [!UICONTROL Profiles] stage.

![select-profiles](../assets/ui/monitor-sources/select-profiles.png)

### [!DNL Profile] mått {#profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profile_processing"
>title="Profilbearbetning"
>abstract="Profilbearbetning innehåller information om poster som importerats till profiltjänsten, inklusive antalet profilfragment som skapats, uppdaterade profilfragment och det totala antalet profilfragment."
>text="Learn more in documentation"

The [!UICONTROL Profile processing] sidan innehåller information om poster som har importerats till [!DNL Profile], inklusive antalet skapade profilfragment, uppdaterade profilfragment och det totala antalet profilfragment.

Markera filterikonen ![filter](../assets/ui/monitor-sources/filter.png) bredvid starttiden för dataflödet för att se mer information om [!DNL Profile] dataflödeskörning.

![profiler](../assets/ui/monitor-sources/profiles.png)

| Profilmått | Beskrivning |
| --------------- | ----------- |
| [!UICONTROL Records received] | Antalet poster som tagits emot från [!DNL Data Lake]. |
| [!UICONTROL Records failed ] | Antalet poster som har importerats, men inte [!DNL Profile] på grund av fel. |
| [!UICONTROL Profile fragments added] | Antalet nya netto [!DNL Profile] tillagda fragment. |
| [!UICONTROL Profile fragments updated] | Antalet befintliga [!DNL Profile] fragment har uppdaterats |
| [!UICONTROL Total Profile fragments] | Det totala antalet poster som skrivs till [!DNL Profile], inklusive alla befintliga [!DNL Profile] fragment uppdaterade och nya [!DNL Profile] skapade fragment. |
| [!UICONTROL Failed dataflow runs] | Antalet misslyckade dataflödeskörningar. |
| [!UICONTROL Processing time] | Tidsstämpeln från det att du har fått in det hela till det färdiga. |
| [!UICONTROL Status] | Definierar den övergripande statusen för ett dataflöde. Möjliga statusvärden är: <ul><li>`Success`: Anger att ett dataflöde är aktivt och att data hämtas enligt det schema som det tillhandahölls.</li><li>`Failed`: Anger att aktiveringsprocessen för ett dataflöde har avbrutits på grund av fel. </li><li>`Processing`: Anger att dataflödet ännu inte är aktivt. Denna status inträffar ofta omedelbart efter att ett nytt dataflöde har skapats.</li></ul> |

The [!UICONTROL Dataflow run details] sidan visar mer information om [!DNL Profile] dataflödeskörning, inklusive dess IMS Org ID och dataflödeskörnings-ID. På den här sidan visas även motsvarande felkod och felmeddelande från [!DNL Profile], om det uppstår några fel i intagsprocessen.

![profiles-dataflow-run](../assets/ui/monitor-sources/profiles-dataflow-run.png)

## Nästa steg {#next-steps}

Genom att följa den här självstudiekursen har du övervakat inmatningsdataflödet från källnivån till [!DNL Identity Service]och till [!DNL Profile], med **[!UICONTROL Monitoring]** kontrollpanel. Du har också identifierat fel som bidrog till att dataflödena misslyckades under importen. Mer information finns i följande dokument:

* [Översikt över kundprofiler i realtid](../../profile/home.md)
* [Översikt över arbetsytan Datavetenskap](../../data-science-workspace/home.md)
