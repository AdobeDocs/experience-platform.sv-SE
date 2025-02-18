---
description: Lär dig hur du kan övervaka dataflöden för dina mål med hjälp av Experience Platform användargränssnitt.
solution: Experience Platform
title: Övervaka dataflöden för mål i användargränssnittet
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: b814becaed88ce23527dc58f7ec056c05a48379f
workflow-type: tm+mt
source-wordcount: '3468'
ht-degree: 1%

---

# Övervaka dataflöden för mål i användargränssnittet

Använd de olika destinationerna i Experience Platform-katalogen för att aktivera data från Platform till ett oändligt antal externa partner. Plattformen gör det enklare att spåra dataflödet till destinationerna genom att tillhandahålla genomskinlighet med dataflöden.

Kontrollpanelen ger dig en visuell representation av ett dataflödes resa, inklusive målet som data aktiveras till, vilken typ av data du visar, exporterade data per dataflöde och mycket annat.

I den här självstudiekursen får du anvisningar om hur du antingen kan övervaka dataflöden direkt på arbetsytan för mål eller använda kontrollpanelen för att övervaka dataflöden för dina mål med hjälp av Experience Platform användargränssnitt.

## Komma igång {#getting-started}

Handboken kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Dataflöden](../home.md): Dataflöden är en representation av datajobb som flyttar data mellan plattformar. Dataflöden är konfigurerade för olika tjänster, vilket hjälper dig att flytta data från källanslutningar till måldatauppsättningar, till [!DNL Identity] och [!DNL Profile] samt till [!DNL Destinations].
   - [Dataflöden körs](../../sources/notifications.md): Dataflöden är återkommande schemalagda jobb som baseras på frekvenskonfigurationen för valda dataflöden.
- [Destinationer](../../destinations/home.md): Destinationer är färdiga integreringar med vanliga program som möjliggör smidig aktivering av data från Platform för flerkanalskampanjer, e-postkampanjer, riktad reklam och många andra användningsfall.
- [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enskild [!DNL Platform]-instans till separata virtuella miljöer för att hjälpa till att utveckla och utveckla program för digitala upplevelser.

## Övervaka dataflöden på arbetsytan Destinationer {#monitor-dataflows-in-the-destinations-workspace}

Gå till fliken **[!UICONTROL Browse]** på arbetsytan **[!UICONTROL Destinations]** i plattformsgränssnittet och välj namnet på det mål som du vill visa.

![Välj målvy med en målanslutning markerad](../assets/ui/monitor-destinations/select-destination.png)

En lista över befintliga dataflöden visas. På den här sidan finns en lista med visningsbara dataflöden, inklusive information om mål, användarnamn, antal dataflöden och status.

Se följande tabell för mer information om status:

| Status | Beskrivning |
| ------ | ----------- |
| Aktiverad | Statusen `Enabled` anger att ett dataflöde är aktivt och exporterar data enligt det schema som det tillhandahölls. |
| Handikappade | Statusen `Disabled` anger att ett dataflöde är inaktivt och inte exporterar några data. |
| Bearbetar | Statusen `Processing` anger att ett dataflöde ännu inte är aktivt. Denna status inträffar ofta omedelbart efter att ett nytt dataflöde har skapats. |
| Fel | Statusen `Error` indikerar att aktiveringsprocessen för ett dataflöde har avbrutits. |

### Dataflödeskörningar för direktuppspelningsmål {#dataflow-runs-for-streaming-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation_streaming"
>title="Information om dataflödeskörning"
>abstract="Körningsinformationen för måldataflödet innehåller information om aktiveringsstatus för en målgrupp och mått från kundprofilen i realtid för att generera unika identiteter. Mer information finns i guiden för metriska definitioner."

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_streaming"
>title="Mottagna profiler"
>abstract="Det totala antalet profiler som tagits emot i dataflödet. Det här värdet uppdateras var 60:e minut."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_streaming"
>title="Aktiverade identiteter"
>abstract="Antalet enskilda profilidentiteter har aktiverats för det valda målet. Det här måttet inkluderar identiteter som skapas, uppdateras och tas bort från exporterade målgrupper."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_streaming"
>title="Undantagna identiteter"
>abstract="Antalet enskilda profilposter som har uteslutits från aktivering för den valda destinationen baserat på saknade attribut och godkännandefel."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesfailed_streaming"
>title="Identiteter misslyckades"
>abstract="Antalet enskilda profilidentiteter som misslyckades för det valda målet. Mer information finns i feldiagnostiken."

För direktuppspelningsmål innehåller fliken [!UICONTROL Dataflow runs] en timuppdatering för måttdata på dataflöden. Den mest framträdande statistiken är för identiteter.

Identiteter representerar olika aspekter av en profil. Om en profil till exempel innehåller både ett telefonnummer och en e-postadress har den profilen två identiteter.

En lista över enskilda körningar och deras specifika mått visas tillsammans med följande summor för identiteter:

- **[!UICONTROL Identities activated]**: Det totala antalet profilidentiteter som aktiverats för det valda målet. Det här måttet inkluderar identiteter som skapas, uppdateras och tas bort från exporterade målgrupper.
- **[!UICONTROL Identities excluded]**: Det totala antalet profilidentiteter som hoppas över för aktivering baserat på saknade attribut och godkännandeöverträdelse.
- **[!UICONTROL Identities failed]**: Det totala antalet profilidentiteter som inte har aktiverats till målet på grund av fel.

![Dataflödet kör information för direktuppspelningsmål.](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

Varje enskild dataflödeskörning visar följande information:

- **[!UICONTROL Dataflow run start]**: Den tid då dataflödet startades. För direktuppspelande dataflöden hämtar Experience Platform mätvärden som baseras på början av dataflödet, i form av timstatistik. Det innebär att för direktuppspelande dataflöde körs, och om ett dataflöde startas t.ex. 10:30 PM, visas starttiden som 10:00 PM i gränssnittet.
- **[!UICONTROL Processing time]**: Den tid det tog för dataflödet att bearbeta.
   - För **[!UICONTROL completed]**-körningar visas alltid en timme i bearbetningstidens mått.
   - För dataflöden som fortfarande är i **[!UICONTROL processing]**-läge är fönstret för att hämta alla mått öppet i mer än en timme för att bearbeta alla mått som motsvarar dataflödeskörningen. Ett dataflöde som startades kl. 9.30 kan till exempel vara i ett bearbetningstillstånd i en timme och trettio minuter för att hämta och bearbeta alla mätvärden. När bearbetningsfönstret sedan stängs och dataflödets status uppdateras till **slutförd** ändras den visade bearbetningstiden till en timme.
- **[!UICONTROL Profiles received]**: Det totala antalet profiler som tagits emot i dataflödet.
- **[!UICONTROL Identities activated]**: Det totala antalet profilidentiteter som aktiverades till det valda målet som en del av dataflödeskörningen. Det här måttet inkluderar identiteter som skapas, uppdateras och tas bort från exporterade målgrupper.
- **[!UICONTROL Identities excluded]**: Det totala antalet profilidentiteter som har uteslutits från aktivering baserat på saknade attribut och brott mot medgivande.
- **[!UICONTROL Identities failed]** Det totala antalet profilidentiteter som inte har aktiverats till målet på grund av fel.

  >[!IMPORTANT]
  >
  > Från och med oktober 2024 lanserar Adobe en uppdatering som ökar rapporteringsnoggrannheten för strömningsmål. Den här förbättringen ger bättre anpassning mellan Experience Platform och målplattformarna.
  >
  > Före den här uppdateringen innehöll **[!UICONTROL Identities failed]** alla aktiveringsförsök. Efter den här uppdateringen inkluderas endast det senaste aktiveringsförsöket i det totala antalet.
  > 
  > Den här förbättringen gäller för närvarande för [Google kundmatchningsmålet](../../destinations/catalog/advertising/google-customer-match.md), men kommer gradvis att lanseras för andra Experience Platform-direktuppspelningsmål.
  > Efter förbättringen kan användare av [Google Customer Match-mål](../../destinations/catalog/advertising/google-customer-match.md) se färre **[!UICONTROL Identities failed]**, vilket är helt normalt.


- **[!UICONTROL Activation rate]**: Procentandel mottagna identiteter som har aktiverats. Följande formel visar hur det här värdet beräknas:
  ![Formel för aktiveringsfrekvens.](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL Status]**: Representerar det tillstånd som dataflödet är i: [!UICONTROL Completed] eller [!UICONTROL Processing]. [!UICONTROL Completed] betyder att alla identiteter för motsvarande dataflödeskörning exporterades inom en timme. [!UICONTROL Processing] betyder att dataflödeskörningen inte har slutförts än.

Om du vill visa information om en viss dataflödeskörning väljer du körningens starttid i listan.

Informationssidan för ett dataflöde innehåller ytterligare information, t.ex. antalet profiler som tagits emot, antalet aktiverade identiteter, antalet misslyckade identiteter och antalet utelämnade identiteter.

![Dataflödesinformation för direktuppspelningsmål.](../assets/ui/monitor-destinations/dataflow-details-stream.png)

På informationssidan visas också en lista över misslyckade identiteter och identiteter som har utelämnats. Information om både misslyckade och utelämnade identiteter visas, inklusive felkod, antal identiteter och beskrivning. Som standard visas de misslyckade identiteterna i listan. Om du vill visa överhoppade identiteter väljer du alternativet **[!UICONTROL Identities excluded]**.

![Dataflödesposter för direktuppspelningsmål med ett felmeddelande markerat.](../assets/ui/monitor-destinations/dataflow-records-stream.png)

#### (Beta) Körningsövervakning av dataflöde på målnivå för direktuppspelningsmål {#audience-level-dataflow-runs-for-streaming-destinations}

Du kan visa information om aktiverade, uteslutna eller misslyckade identiteter som är uppdelade på en målgruppsnivå för varje målgrupp som är en del av dataflödet.

Övervakning på målgruppsnivå för direktuppspelningsmål är för närvarande endast tillgängligt för följande mål:

- [[!DNL Google Customer Match + Display & Video 360]](/help/destinations/catalog/advertising/google-customer-match-dv360.md)
- [[!DNL Marketo Engage]](/help/destinations/catalog/adobe/marketo-engage.md)

![Övervakning på målgruppsnivå för direktuppspelningsmål.](/help/dataflows/assets/ui/monitor-destinations/audience-level-monitoring-streaming.png)

>[!NOTE]
>
>Numret **[!UICONTROL Profiles received]** på fliken **[!UICONTROL Audiences]** kanske inte alltid matchar antalet profiler som tagits emot för dataflödeskörningen. Detta beror på att en viss profil kan vara en del av mer än en målgrupp som aktiveras i dataflödeskörningen.

### Dataflödeskörningar för batchdestinationer {#dataflow-runs-for-batch-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation"
>title="Information om dataflödeskörning"
>abstract="Körningsinformationen för måldataflödet innehåller information om aktiveringsstatus för en målgrupp och mått från kundprofilen i realtid för att generera unika identiteter. Mer information finns i guiden för metriska definitioner."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dataflows/ui/monitor-destinations.html#dataflow-runs-for-streaming-destinations" text="Dataflödeskörningar för direktuppspelningsmål"

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_batch"
>title="Mottagna profiler"
>abstract="Det totala antalet profiler som tagits emot i dataflödet. Det här värdet uppdateras var 60:e minut."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_batch"
>title="Aktiverade identiteter"
>abstract="Antalet enskilda profilidentiteter har aktiverats för det valda målet. Det här måttet inkluderar identiteter som skapas, uppdateras och tas bort från exporterade målgrupper."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_batch"
>title="Undantagna identiteter"
>abstract="Antalet enskilda profilposter som har uteslutits från aktivering för den valda destinationen baserat på saknade attribut och godkännandefel."

För gruppmål innehåller fliken [!UICONTROL Dataflow runs] måttdata för dataflödets körningar. En lista över enskilda körningar och deras specifika mått visas tillsammans med följande summor för identiteter:

- **[!UICONTROL Identities activated]**: Det totala antalet profilidentiteter som aktiverats för det valda målet. Det här måttet inkluderar identiteter som skapas, uppdateras och tas bort från exporterade målgrupper.
- **[!UICONTROL Identities excluded]**: Antalet enskilda profilidentiteter som har uteslutits från aktivering för det valda målet, baserat på saknade attribut och godkännandefel.

![Dataflödet kör vy för gruppmål.](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

Varje enskild dataflödeskörning visar följande information:

- **[!UICONTROL Dataflow run start]**: Den tid då dataflödet startades.
- **[!UICONTROL Audience]**: Namnet på målgruppen som är associerad med varje dataflödeskörning.
- **[!UICONTROL Processing time]**: Den tid det tog att bearbeta dataflödet.
- **[!UICONTROL Profiles received]**: Det totala antalet profiler som tagits emot i dataflödet. Det här värdet uppdateras var 60:e minut.
- **[!UICONTROL Identities activated]**: Det totala antalet profilidentiteter som aktiverades till det valda målet som en del av dataflödeskörningen. Det här måttet inkluderar identiteter som skapas, uppdateras och tas bort från exporterade målgrupper.
- **[!UICONTROL Identities excluded]**: Det totala antalet profilidentiteter som har uteslutits från aktivering baserat på saknade attribut och brott mot medgivande.
- **[!UICONTROL Status]**: Representerar det tillstånd som dataflödet är i. Det kan vara ett av tre lägen: [!UICONTROL Success], [!UICONTROL Failed] och [!UICONTROL Processing]. [!UICONTROL Success] betyder att dataflödet är aktivt och exporterar data enligt angivet schema. [!UICONTROL Failed] betyder att aktiveringen av data har avbrutits på grund av fel. [!UICONTROL Processing] betyder att dataflödet ännu inte är aktivt och vanligtvis påträffas när ett nytt dataflöde skapas.

Om du vill visa information om ett specifikt dataflöde väljer du körningens starttid i listan.

>[!NOTE]
>
>Dataflödeskörningar genereras baserat på måldataflödets schemafrekvens. En separat dataflödeskörning görs för varje [sammanfogningsprincip](../../profile/merge-policies/overview.md) som tillämpas på en målgrupp.

På informationssidan för ett dataflöde visas mer specifik information om dataflödet, förutom informationen som visas i dataflödeslistan:

- **[!UICONTROL Size of data]**: Storleken på dataflödet som exporteras.
- **[!UICONTROL Total files]**: Det totala antalet filer som har exporterats i dataflödet.
- **[!UICONTROL Last updated]**: Den tidpunkt då dataflödeskörningen senast uppdaterades.

![Information om dataflödeskörning för batchmål.](../assets/ui/monitor-destinations/dataflow-batch.png)

På informationssidan visas också en lista över misslyckade identiteter och identiteter som har utelämnats. Information om både de misslyckade och exkluderade identiteterna visas, inklusive felkoden och beskrivningen. Som standard visas de misslyckade identiteterna i listan. Om du vill visa utelämnade identiteter väljer du alternativet **[!UICONTROL Identities excluded]**.

![Dataflödesposter för batchmål med ett felmeddelande markerat.](../assets/ui/monitor-destinations/dataflow-records-batch.png)

### Visa i övervakning {#view-in-monitoring}

Du kan också välja att visa omfattande information om ett visst dataflöde och dess dataflöde körs på kontrollpanelen. Så här visar du information om ett dataflöde på kontrollpanelen:

1. Navigera till fliken **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** > **[!UICONTROL Browse]**
2. Navigera till det dataflöde som du vill inspektera.
3. Välj ellipssymbolen och ![övervakningsikonen](/help/images/icons/monitoring.png) **[!UICONTROL View in monitoring]**.

![Välj Visa i övervakning i målarbetsflödet för att få mer information om ett dataflöde.](/help/dataflows/assets/ui/monitor-destinations/view-in-monitoring.png)

>[!SUCCESS]
>
>Nu kan du visa information om dataflödet och dess associerade dataflöde i kontrollpanelen. Läs avsnittet nedan för mer information.

## Kontrollpanel för målplatser {#monitoring-destinations-dashboard}

>[!NOTE]
>
>Funktionen för målövervakning stöds för närvarande för alla mål i Experience Platform *förutom* för [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) och [Anpassad personalisering](/help/destinations/catalog/personalization/custom-personalization.md) .

>[!CONTEXTUALHELP]
>id="platform_monitoring_activation"
>title="Aktivering"
>abstract="Målaktiveringsvyn innehåller information om aktiveringsstatus för en målgrupp och mått från kundprofilen i realtid för att generera unika identiteter."

Om du vill komma åt kontrollpanelen [!UICONTROL Monitoring] väljer du **[!UICONTROL Monitoring]** (![övervakningsikon](/help/images/icons/monitoring.png)) i den vänstra navigeringen. Välj [!UICONTROL Destinations] på sidan [!UICONTROL Monitoring]. Kontrollpanelen [!UICONTROL Monitoring] innehåller mått och information om målkörningsjobb.

Använd kontrollpanelen [!UICONTROL Destinations] för att få en övergripande uppfattning om hälsotillståndet för dina aktiveringsflöden. Börja med att få samlade insikter om alla grupper och direktuppspelningsmål och fördjupa er sedan i detaljerade vyer för dataflöden, dataflöden och aktiverade målgrupper för en djupgående genomgång av era aktiveringsdata. Skärmarna på kontrollpanelen [!UICONTROL Monitoring] innehåller åtgärdbara insikter via mått och felbeskrivningar som hjälper dig att felsöka eventuella problem som kan uppstå i dina aktiveringsscenarier.

Du kan filtrera den visade informationen efter datatyp - kunder, konton (endast för Adobe Real-Time CDP B2B edition), potentiella kunder och kontoberikning. Läs mer om de här alternativen i [guiden för kontrollpanelen](/help/dataflows/ui/monitor.md#monitoring-dashboard-overview).

![Datatypsfiltret är markerat i kontrollpanelsvyn.](/help/dataflows/assets/ui/monitor-destinations/add-data-filter.png)

Mitten av kontrollpanelen är panelen [!UICONTROL Activation], som innehåller mått och diagram som visar data om aktiveringshastigheten för de data som exporteras till direktuppspelningsdestinationer, samt om det misslyckade batchdataflödet går till batchdestinationer.

![Diagram för direktuppspelning och gruppaktivering är markerade i övervakningsvyn.](../assets/ui/monitor-destinations/dashboard-graph.png)


Som standard innehåller de data som visas aktiveringsinformationen från de senaste 24 timmarna. Välj **[!UICONTROL Last 24 hours]** om du vill justera tidsramen för de poster som visas. De tillgängliga alternativen är **[!UICONTROL Last 24 hours]**, **[!UICONTROL Last 7 days]** och **[!UICONTROL Last 30 days]**. Du kan också välja datum i kalenderns popup-fönster som visas. När du har valt datum väljer du **[!UICONTROL Apply]** för att justera tidsramen för den information som visas.

>[!NOTE]
>
>På följande skärmbild visas aktiveringshastigheten och batchdataflödet under de senaste 30 dagarna i stället för under de senaste 24 timmarna. Du kan justera tidsramen genom att välja **[!UICONTROL Last 30 days]**.

![Ändra datumintervallkontroll för sökning markerat för aktiverade mål](../assets/ui/monitor-destinations/dashboard-graph-change-date-range.png)

Använd pilikonen (![pilikon](/help/images/icons/chevron-up.png)) för att expandera eller stänga av korten högst upp på skärmen. Korten visar snabböversiktsinformation om aktiveringsdetaljer baserat på måltyp - direktuppspelning eller batch:

- **[!UICONTROL Streaming activation rate]**: Representerar procentandelen mottagna identiteter som antingen har aktiverats eller hoppats över. Formeln som används för att beräkna den här procentandelen beskrivs vidare ovan på den här sidan i avsnittet [Dataflöd för direktuppspelningsmål](#dataflow-runs-for-streaming-destinations).
- **[!UICONTROL Batch failed dataflow runs]**: Representerar antalet misslyckade dataflödeskörningar i det valda tidsintervallet.

![Visa eller ignorera kort överst på sidan.](../assets/ui/monitor-destinations/monitoring-destinations-toggle-arrow.gif)

Diagrammet **[!UICONTROL Activation]** visas som standard och du kan inaktivera det om du vill utöka listan med mål nedan. Markera växlingsknappen **[!UICONTROL Metrics and graphs]** om du vill inaktivera diagrammen.

På panelen **[!UICONTROL Activation]** visas en lista med mål som innehåller minst ett befintligt konto. Listan innehåller även information om mottagna profiler, aktiverade identiteter, misslyckade identiteter, utelämnade identiteter, aktiveringsfrekvens, totalt antal misslyckade dataflöden samt det senaste uppdateringsdatumet för dessa destinationer. Alla mått är inte tillgängliga för alla måltyper. Tabellen nedan visar vilka mätvärden och vilken information som är tillgängliga per måltyp.

| Mått | Måltyp |
|--------------------------------------|-----------------------|
| **[!UICONTROL Records received]** | Direktuppspelning och batch |
| **[!UICONTROL Records activated]** | Direktuppspelning och batch |
| **[!UICONTROL Records failed]** | Direktuppspelning |
| **[!UICONTROL Records skipped]** | Direktuppspelning och batch |
| **[!UICONTROL Data type]** | Direktuppspelning och batch |
| **[!UICONTROL Activation rate]** | Direktuppspelning |
| **[!UICONTROL Total failed dataflows]** | Grupp |
| **[!UICONTROL Last updated]** | Direktuppspelning och batch |

{style="table-layout:auto"}

![Övervaka instrumentpanel med alla aktiverade mål markerade.](../assets/ui/monitor-destinations/dashboard-destinations.png)

Du kan även filtrera listan över destinationer så att endast den valda destinationskategorin visas. Markera listrutan **[!UICONTROL My destinations]** och välj den [målkategori](/help/destinations/destination-types.md#categories) som du vill filtrera till.

![Filtrera mål med listruteväljare](../assets/ui/monitor-destinations/dashboard-destinations-filter-dropdown.png)

Dessutom kan du ange ett mål i sökfältet för att isolera till ett enda mål. Om du vill visa målets dataflöden kan du markera filtret ![filter](/help/images/icons/filter-add.png) bredvid det och visa en lista över de aktiva dataflödena.

![Filtrera mål med hjälp av sökfältet som är markerat i övervakningsvyn.](../assets/ui/monitor-destinations/filtered-destinations.png)

Om du vill visa alla befintliga dataflöden för alla mål väljer du **[!UICONTROL Dataflows]**.

En lista över dataflöden visas, sorterad efter den senaste dataflödeskörningen. Du kan se ytterligare information om ett specifikt dataflöde genom att leta upp det mål som du vill övervaka, markera filtret ![filter](/help/images/icons/filter-add.png) bredvid det och sedan välja filtret ![filter](/help/images/icons/filter-add.png) bredvid det dataflöde som du vill ha mer information om.

![Alla dataflöden är markerade på kontrollpanelen.](../assets/ui/monitor-destinations/dashboard-dataflows.png)

När du har valt ett dataflöde för vidare kontroll innehåller informationssidan för dataflöde en växlingsknapp som gör att du kan se aktiverade data i dataflödet, uppdelade efter dataflödeskörningar eller målgrupper.

### Vy för körning av dataflöde {#dataflow-runs-view}

När **[!UICONTROL Dataflow runs]** har valts kan du se en lista över dataflödeskörningar för det valda dataflödet och mer information om varje körning.

>[!INFO]
>
>För dataflöden till direktuppspelningsmål delas ett dataflöde upp i timfönster. Varje timfönster genererar ett motsvarande ID för dataflödeskörning.
>
>För dataflöden till batchdestinationer har varje målgrupp ett motsvarande dataflöde som genereras baserat på målgruppens schemalagda aktiveringsfrekvens. Om du till exempel skapar en daglig schemalagd aktivering för fem målgrupper i samma måldataflöde, genereras fem separata dataflöden varje dag.

![Dataflödet kör en panel med flera körningar markerade.](../assets/ui/monitor-destinations/dashboard-flow-runs-view.png)

Använd växlingsknappen **[!UICONTROL Show failures only]** om du bara vill visa misslyckade körningar för ett dataflöde.

![Dataflödet kör vy med endast växlingsknappen markerad för visa-fel](../assets/ui/monitor-destinations/dataflow-runs-show-failures-only.gif)

### Målgruppsvy {#segment-level-view}

När **[!UICONTROL Audiences]** är markerat visas en lista över de målgrupper som aktiverats för det valda dataflödet, inom det valda tidsintervallet. Den här skärmen innehåller information på målgruppsnivå om aktiverade poster, uteslutna poster samt status och tid för det senaste dataflödet. Genom att granska mätvärdena för poster som har uteslutits och aktiverats kan ni verifiera om en målgrupp har aktiverats eller inte.

Du aktiverar till exempel en publik som heter&quot;Lojalitetsmedlemmar i Kalifornien&quot; till Amazon S3-destinationen&quot;Lojalitetsmedlemmar i Kalifornien&quot;. Låt oss anta att det finns 100 profiler i den valda målgruppen, men endast 80 av 100 poster innehåller attribut för lojalitet-ID och du har definierat reglerna för exportmappning som `loyalty.id` krävs. I det här fallet, på målgruppsnivå, ser du 80 poster aktiverade och 20 poster uteslutna.

>[!IMPORTANT]
>
>Observera de nuvarande begränsningarna för målgruppsstatistik:
>- Vyn på målgruppsnivå är för närvarande endast tillgänglig för gruppbaserade (filbaserade) mål och målet [Google Customer Match DV 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md) för direktuppspelning. Lansering planeras för ytterligare direktuppspelningsmål.
>- För batchdestinationer registreras målgruppsvärden endast för lyckade dataflöden. De spelas inte in för misslyckade dataflödeskörningar och uteslutna poster. För dataflöden som går till direktuppspelningsmål hämtas mätvärden och visas för aktiverade och uteslutna poster.

![Publiker som är markerade på dataflödespanelen.](../assets/ui/monitor-destinations/dashboard-segments-view.png)

I målgruppsnivåvyn sammanställs mätvärdena över flera dataflöden inom det valda tidsintervallet. Om det finns flera dataflödeskörningar kan du gå nedåt från målgruppsnivån för att se detaljerna för varje dataflödeskörning, filtrerade efter den valda målgruppen.
Använd filterknappen ![filter](/help/images/icons/filter-add.png) för att gå ned i dataflödesvyn för varje målgrupp i dataflödet.

### Körningssida för dataflöde {#dataflow-runs-page}

På sidan för dataflöden visas information om dataflödets körningar, inklusive starttid för dataflöde, bearbetningstid, mottagna poster, aktiverade poster, uteslutna poster, misslyckade poster, aktiveringsfrekvens och status.

När du går ned på dataflödets körningssida från vyn [på målgruppsnivå](#segment-level-view) kan du filtrera dataflödet med följande alternativ:

- **[!UICONTROL Dataflow runs with failed records]**: För den valda målgruppen listas alla dataflödeskörningar som misslyckades för aktivering med det här alternativet. Information om varför poster i ett visst dataflöde misslyckades finns på [informationssidan för dataflödeskörning](#dataflow-run-details-page) för det dataflödet.
- **[!UICONTROL Dataflow runs with excluded records]**: För den valda målgruppen listas alla dataflöden där vissa av posterna inte var helt aktiverade och vissa profiler hoppades över. Information om varför poster i en viss dataflödeskörning hoppades över finns på [informationssidan ](#dataflow-run-details-page) för dataflödeskörningen.
- **[!UICONTROL Dataflow runs with activated records]**: För den valda målgruppen listas alla dataflödeskörningar som har poster som har aktiverats.

![Alternativknappar som visar hur du filtrerar dataflöden för målgrupper.](/help/dataflows/assets/ui/monitor-destinations/dataflow-runs-segment-filter.png)

Om du vill visa mer information om en viss dataflödeskörning väljer du filtret ![filter](/help/images/icons/filter-add.png) bredvid starttiden för dataflödeskörningen för att visa informationssidan för dataflödeskörningen.

![Dataflödet kör filter i kontrollpanelen för att utforska mer information för en viss dataflödeskörning.](../assets/ui/monitor-destinations/dataflow-runs-filter.png)

### Detaljsida för dataflödeskörning {#dataflow-run-details-page}

På sidan med information om dataflödeskörning visas mer specifik information om dataflödet, förutom informationen som visas i listan över dataflödeskörningar:

- **[!UICONTROL Dataflow run ID]**: ID:t för dataflödet.
- **[!UICONTROL IMS org ID]**: Organisationen som dataflödet tillhör.
- **[!UICONTROL Last updated]**: Den tidpunkt då dataflödeskörningen senast uppdaterades.

På informationssidan finns också en växlingsknapp för att växla mellan körningsfel och målgrupper i dataflöden. Det här alternativet är endast tillgängligt för dataflöden som körs på batchdestinationer och för [Google kundmatchningsmålet DV 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md).

I dataflödets felvy visas en lista med poster som misslyckades och poster som hoppades över. Information om både misslyckade och överhoppade poster visas, inklusive felkod, antal identiteter och beskrivning. Som standard visas de poster som misslyckades i listan. Om du vill visa överhoppade poster väljer du alternativet **[!UICONTROL Records skipped]**.

![Ingen växling av undantagna identiteter har markerats i övervakningsvyn](../assets/ui/monitor-destinations/identities-excluded.png)

När **[!UICONTROL Audiences]** är markerat visas en lista över de målgrupper som aktiverats i den valda dataflödeskörningen. Den här skärmen innehåller information på målgruppsnivå om aktiverade poster, uteslutna poster samt status och tid för det senaste dataflödet.

![Vyn Publiker i informationsfönstret för dataflödeskörning.](../assets/ui/monitor-destinations/dataflow-run-segments-view.png)

## Nästa steg {#next-steps}

Genom att följa den här guiden kan du nu övervaka dataflöden för både batch- och direktuppspelningsmål, inklusive all relevant information som bearbetningstid, aktiveringsfrekvens och status. Mer information om dataflöden i plattformen finns i [dataflödesöversikten](../home.md). Läs [målöversikten](../../destinations/home.md) om du vill veta mer om mål.