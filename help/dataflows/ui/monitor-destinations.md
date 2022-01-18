---
keywords: Experience Platform;hem;populära ämnen;övervakningskonton;övervaka dataflöden;dataflöden;mål
description: Med destinationer kan ni aktivera data från Adobe Experience Platform för ett oändligt antal externa partner. I den här självstudiekursen finns anvisningar om hur du kan övervaka dataflöden för dina mål med hjälp av användargränssnittet i Experience Platform.
solution: Experience Platform
title: Övervaka dataflöden för mål i användargränssnittet
topic-legacy: overview
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: 567cfd5ecec23d35317a46a3126a608cc4792a73
workflow-type: tm+mt
source-wordcount: '1799'
ht-degree: 0%

---

# Övervaka dataflöden för mål i användargränssnittet

Med destinationer kan ni aktivera data från Adobe Experience Platform för ett oändligt antal externa partner. Plattformen gör det enklare att spåra dataflödet till destinationerna genom att tillhandahålla genomskinlighet med dataflöden.

Kontrollpanelen ger dig en visuell representation av resan för ett dataflöde, inklusive målet som data aktiveras till. I den här självstudiekursen finns anvisningar om hur du antingen kan övervaka dataflöden direkt på arbetsytan för mål eller använda kontrollpanelen för övervakning för att övervaka dataflöden för dina mål med hjälp av användargränssnittet i Experience Platform.

## Komma igång

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Dataflöden](../home.md): Dataflöden är en representation av datajobb som flyttar data mellan plattformar. Dataflöden konfigureras över olika tjänster, vilket hjälper dig att flytta data från källanslutningar till måldatauppsättningar till [!DNL Identity] och [!DNL Profile]och till [!DNL Destinations].
   - [Dataflödeskörningar](../../sources/notifications.md): Dataflödeskörningar är återkommande schemalagda jobb som baseras på frekvenskonfigurationen för valda dataflöden.
- [Destinationer](../../destinations/home.md): Destinationer är färdiga integreringar med vanliga applikationer som möjliggör smidig aktivering av data från Platform för flerkanalskampanjer, e-postkampanjer, riktad annonsering och många andra användningsfall.
- [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

## Övervaka dataflöden på arbetsytan Destinationer {#monitor-dataflows-in-the-destinations-workspace}

I **[!UICONTROL Destinations]** navigera till **[!UICONTROL Browse]** och välj namnet på ett mål som du vill visa.

![](../assets/ui/monitor-destinations/select-destination.png)

En lista över befintliga dataflöden visas. På den här sidan finns en lista med visningsbara dataflöden, inklusive information om mål, användarnamn, antal dataflöden och status.

Se följande tabell för mer information om status:

| Status | Beskrivning |
| ------ | ----------- |
| Aktiverad | The `Enabled` status anger att ett dataflöde är aktivt och exporterar data enligt det schema som det angavs. |
| Handikappade | The `Disabled` status anger att ett dataflöde är inaktivt och inte exporterar några data. |
| Bearbetar | The `Processing` status anger att ett dataflöde ännu inte är aktivt. Denna status inträffar ofta omedelbart efter att ett nytt dataflöde har skapats. |
| Fel | The `Error` status anger att aktiveringsprocessen för ett dataflöde har avbrutits. |

### Dataflödeskörningar för direktuppspelningsmål {#dataflow-runs-for-streaming-destinations}

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated"
>title="Aktiverade identiteter"
>abstract="Antalet enskilda profilidentiteter har aktiverats för det valda målet."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded"
>title="Undantagna identiteter"
>abstract="Antalet enskilda profilposter som har uteslutits från aktivering för den valda destinationen baserat på saknade attribut och godkännandefel."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesfailed"
>title="Identiteter misslyckades"
>abstract="Antalet enskilda profilidentiteter som misslyckades för det valda målet. Mer information finns i feldiagnostiken."
>additional-url="https://adobe.com/go/destinations-monitor-dataflows-batch-en" text="Läs mer i dokumentationen"

För direktuppspelningsmål finns följande [!UICONTROL Dataflow runs] tillhandahåller en timuppdatering för mätdata på dina dataflöden. Den mest framträdande statistiken är för identiteter.

Identiteter representerar olika aspekter av en profil. Om en profil till exempel innehåller både ett telefonnummer och en e-postadress har den profilen två identiteter.

En lista över enskilda körningar och deras specifika mått visas tillsammans med följande summor för identiteter:

- **[!UICONTROL Identities activated]**: Det totala antalet profilidentiteter som har skapats eller uppdaterats för aktivering.
- **[!UICONTROL Identities excluded]**: Det totala antalet profilidentiteter som har hoppats över för aktivering baserat på saknade attribut och medgivandeöverträdelse.
- **[!UICONTROL Identities failed]**: Det totala antalet profilidentiteter som inte har aktiverats till målet på grund av fel.

![](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

Varje enskild dataflödeskörning visar följande information:

- **[!UICONTROL Dataflow run start]**: Den tid som dataflödet körs vid.
- **[!UICONTROL Processing time]**: Den tid det tog för dataflödet att bearbeta.
- **[!UICONTROL Profiles received]**: Det totala antalet profiler som tagits emot i dataflödet.
- **[!UICONTROL Identities activated]**: Det totala antalet profilidentiteter som har aktiverats för det valda målet.
- **[!UICONTROL Identities excluded]**: Det totala antalet profilidentiteter som har uteslutits från aktivering baserat på saknade attribut och brott mot medgivande.
- **[!UICONTROL Identities failed]** Det totala antalet profilidentiteter som inte har aktiverats till målet på grund av fel.
- **[!UICONTROL Activation rate]**: Procentandelen mottagna identiteter som antingen har aktiverats eller hoppats över. Följande formel visar hur det här värdet beräknas:
   ![](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL Status]**: Representerar läget för dataflödet: antingen [!UICONTROL Completed] eller [!UICONTROL Processing]. [!UICONTROL Completed] betyder att alla identiteter för motsvarande dataflödeskörning exporterades inom en timma. [!UICONTROL Processing] betyder att dataflödeskörningen inte har slutförts ännu.

Om du vill visa information om ett visst dataflöde väljer du körningens starttid i listan.

Informationssidan för ett dataflöde innehåller ytterligare information, t.ex. antalet profiler som tagits emot, antalet aktiverade identiteter, antalet misslyckade identiteter och antalet utelämnade identiteter.

![](../assets/ui/monitor-destinations/dataflow-details-stream.png)

På informationssidan visas också en lista över misslyckade identiteter och identiteter som har utelämnats. Information om både misslyckade och utelämnade identiteter visas, inklusive felkod, antal identiteter och beskrivning. Som standard visas de misslyckade identiteterna i listan. Om du vill visa överhoppade identiteter väljer du **[!UICONTROL Identities excluded]** växla.

![](../assets/ui/monitor-destinations/dataflow-records-stream.png)

### Dataflödeskörningar för batchmål {#dataflow-runs-for-batch-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation"
>title="Information om dataflödeskörning"
>abstract="Körningsinformationen för måldataflödet innehåller information om segmentets aktiveringsstatus och mått som hämtats från kundprofilen i realtid för att generera unika identiteter. Mer information finns i guiden för metriska definitioner."

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received"
>title="Mottagna profiler"
>abstract="Det totala antalet profiler som tagits emot i dataflödet. Det här värdet uppdateras var 60:e minut."
>additional-url="https://adobe.com/go/destinations-monitor-dataflows-batch-en" text="Läs mer i dokumentationen"

För batchdestinationer är [!UICONTROL Dataflow runs] -fliken innehåller mätdata för dina dataflödeskörningar. En lista över enskilda körningar och deras specifika mått visas tillsammans med följande summor för identiteter:

- **[!UICONTROL Identities activated]**: Antalet enskilda profilidentiteter har aktiverats för det valda målet.
- **[!UICONTROL Identities excluded]**: Antalet individuella profilidentiteter som har uteslutits från aktivering för den valda destinationen, baserat på saknade attribut och medgivande.

![](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

Varje enskild dataflödeskörning visar följande information:

- **[!UICONTROL Dataflow run start]**: Den tid som dataflödet körs vid.
- **[!UICONTROL Processing time]**: Den tid det tog för dataflödet att bearbeta.
- **[!UICONTROL Profiles received]**: Det totala antalet profiler som tagits emot i dataflödet. Det här värdet uppdateras var 60:e minut.
- **[!UICONTROL Identities activated]**: Det totala antalet profilidentiteter som har aktiverats för det valda målet.
- **[!UICONTROL Identities excluded]**: Det totala antalet profilidentiteter som har uteslutits från aktivering baserat på saknade attribut och brott mot medgivande.
- **[!UICONTROL Status]**: Representerar det läge som dataflödet är i. Det kan vara ett av tre lägen: [!UICONTROL Success], [!UICONTROL Failed]och [!UICONTROL Processing]. [!UICONTROL Success] betyder att dataflödet är aktivt och exporterar data enligt angivet schema. [!UICONTROL Failed] innebär att aktiveringen av uppgifter har avbrutits på grund av fel. [!UICONTROL Processing] betyder att dataflödet ännu inte är aktivt och vanligtvis uppstår när ett nytt dataflöde skapas.

Om du vill visa information om ett specifikt dataflöde väljer du körningens starttid i listan.

>[!NOTE]
>
>Dataflödeskörningar genereras baserat på måldataflödets schemafrekvens. En separat dataflödeskörning görs för varje sammanfogningsprincip som tillämpas på ett segment.

På informationssidan för ett dataflöde visas mer specifik information om dataflödet, förutom informationen som visas i dataflödeslistan:

- **[!UICONTROL Size of data]**: Storleken på dataflödet som exporteras.
- **[!UICONTROL Total files]**: Det totala antalet filer som exporteras i dataflödet.
- **[!UICONTROL Last updated]**: Den tidpunkt då dataflödeskörningen senast uppdaterades.

![](../assets/ui/monitor-destinations/dataflow-batch.png)

På informationssidan visas också en lista över misslyckade identiteter och identiteter som har utelämnats. Information om både de misslyckade och exkluderade identiteterna visas, inklusive felkoden och beskrivningen. Som standard visas de misslyckade identiteterna i listan. Om du vill visa utelämnade identiteter väljer du **[!UICONTROL Identities excluded]** växla.

![](../assets/ui/monitor-destinations/dataflow-records-batch.png)

## Kontrollpanel för målplatser {#monitoring-destinations-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_activation"
>title="Aktivering"
>abstract="Målaktiveringen innehåller information om segmentets aktiveringsstatus och mått som hämtats från kundprofilen i realtid för att generera unika identiteter."

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="Segmentjobb"
>abstract="Kontrollpanelen för segmentjobb innehåller information om utvärderings- och exportjobb för alla segment."

Så här öppnar du [!UICONTROL Monitoring] kontrollpanel, välja **[!UICONTROL Monitoring]** (![övervakningsikon](../assets/ui/monitor-destinations/monitoring-icon.png)) i den vänstra navigeringen. På [!UICONTROL Monitoring] sida, markera [!UICONTROL Destinations]. The [!UICONTROL Monitoring] Kontrollpanelen innehåller mått och information om målkörningsjobb.

Mitten av kontrollpanelen är aktiveringspanelen, som innehåller mått och diagram som visar data om aktiveringshastigheten för de data som exporteras till destinationer.

![](../assets/ui/monitor-destinations/dashboard-graph.png)


Som standard innehåller de data som visas aktiveringshastigheterna från de senaste 24 timmarna. Välj **[!UICONTROL Last 24 hours]** för att justera tidsramen för de poster som visas. Tillgängliga alternativ inkluderar **[!UICONTROL Last 24 hours]**, **[!UICONTROL Last 7 days]** och **[!UICONTROL Last 30 days]**. Du kan också välja datum i kalenderns popup-fönster som visas. När du har valt datum väljer du **[!UICONTROL Apply]** för att justera tidsramen för den information som visas.

>[!NOTE]
>
>På följande skärmbild visas aktiveringshastigheten de senaste 30 dagarna i stället för de senaste 24 timmarna. Du kan justera tidsramen genom att markera **[!UICONTROL Last 30 days]**.

![](../assets/ui/monitor-destinations/dashboard-graph-change-date-range.png)

Diagrammet visas som standard och du kan inaktivera det om du vill utöka listan över mål nedan. Välj **[!UICONTROL Metrics and graphs]** om du vill inaktivera diagrammen.

The **[!UICONTROL Activation]** På panelen visas en lista med mål som innehåller minst ett befintligt konto. Den här listan innehåller även information om mottagna profiler, aktiverade profilposter, misslyckade profilposter, överhoppade profilposter, totalt antal misslyckade dataflöden samt det senaste uppdateringsdatumet för dessa mål.

![](../assets/ui/monitor-destinations/dashboard-destinations.png)

Du kan även filtrera listan över destinationer så att endast den valda destinationskategorin visas. Välj **[!UICONTROL My destinations]** och välj den måltyp som du vill filtrera till.

![](../assets/ui/monitor-destinations/dashboard-destinations-filter-dropdown.png)

Dessutom kan du ange ett mål i sökfältet för att isolera till ett enda mål. Om du vill se målets dataflöden kan du välja filtret ![filter](../assets/ui/monitor-destinations/filter.png) bredvid den och se en lista över de aktiva dataflödena.

![](../assets/ui/monitor-destinations/filtered-destinations.png)

Om du vill visa alla befintliga dataflöden för alla mål väljer du **[!UICONTROL Dataflows]**.

En lista över dataflöden visas, grupperade per mål. Du kan se ytterligare information om ett specifikt dataflöde genom att leta reda på målet som du vill övervaka och välja filtret ![filter](../assets/ui/monitor-destinations/filter.png) bredvid den och därefter välja filtret ![filter](../assets/ui/monitor-destinations/filter.png) Förutom dataflödet vill du ha mer information om.

![](../assets/ui/monitor-destinations/dashboard-dataflows.png)


På sidan för dataflöden visas information om dataflödets körningar, inklusive starttid för dataflöde, bearbetningstid, mottagna profiler, aktiverade identiteter, utelämnade identiteter, misslyckade identiteter, aktiveringsfrekvens och status. Om du vill visa mer information om en viss dataflödeskörning väljer du filtret ![filter](../assets/ui/monitor-destinations/filter.png) bredvid starttiden för dataflödet.

![](../assets/ui/monitor-destinations/dashboard-dataflows-filter.png)

På informationssidan visas mer specifik information om dataflödet, förutom informationen som visas i dataflödeslistan:

- **[!UICONTROL Dataflow run ID]**: ID för dataflödet.
- **[!UICONTROL IMS org ID]**: Den IMS-organisation som dataflödet tillhör.
- **[!UICONTROL Last updated]**: Den tidpunkt då dataflödeskörningen senast uppdaterades.

På informationssidan visas också en lista över misslyckade identiteter och identiteter som har utelämnats. Information om både misslyckade och utelämnade identiteter visas, inklusive felkod, antal identiteter och beskrivning. Som standard visas de misslyckade identiteterna i listan. Om du vill visa överhoppade identiteter väljer du **[!UICONTROL Identities excluded]** växla.

![](../assets/ui/monitor-destinations/identities-excluded.png)

## Nästa steg

Genom att följa den här guiden kan du nu övervaka dataflöden för både batch- och direktuppspelningsmål, inklusive all relevant information som bearbetningstid, aktiveringsfrekvens och status. Läs mer om dataflöden i plattformar i [dataflödesöversikt](../home.md). Läs mer om destinationer i [destinationer, översikt](../../destinations/home.md).