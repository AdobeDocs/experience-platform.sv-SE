---
keywords: Experience Platform;hem;populära ämnen;övervaka identiteter;övervaka dataflöden;dataflöden;identiteter;
description: Adobe Experience Platform identitetstjänst ger er en heltäckande bild av era kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid. I den här självstudiekursen finns anvisningar om hur du kan övervaka dataflöden med identiteter med hjälp av användargränssnittet i Experience Platform.
title: Övervaka dataflöden för identiteter i användargränssnittet
type: Tutorial
exl-id: 735b0e52-74f6-47fe-98c6-e12a633b6f57
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 0%

---

# Övervaka dataflöden för identiteter i användargränssnittet

Adobe Experience Platform identitetstjänst ger er en heltäckande bild av era kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

Kontrollpanelen ger dig en visuell representation av dataaktiviteten inom identiteter, inklusive status för dina datas identiteter. I den här självstudiekursen finns anvisningar om hur du kan använda kontrollpanelen för att övervaka dina data med hjälp av användargränssnittet i Experience Platform, så att du kan spåra status för identitetsbearbetning.

## Komma igång {#getting-started}

- [Dataflöden](../home.md): Dataflöden är en representation av datajobb som flyttar data mellan plattformar. Dataflöden konfigureras över olika tjänster, vilket hjälper dig att flytta data från källanslutningar till måldatauppsättningar till [!DNL Identity] och [!DNL Profile]och till [!DNL Destinations].
   - [Dataflödeskörningar](../../sources/notifications.md): Dataflödeskörningar är återkommande schemalagda jobb som baseras på frekvenskonfigurationen för valda dataflöden.
- [Identitetstjänst](../../identity-service/home.md): Få en bättre bild av enskilda kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system.
- [Sandlådor](../../sandboxes/home.md): [!DNL Experience Platform] innehåller virtuella sandlådor som partitionerar en enda [!DNL Platform] till separata virtuella miljöer för att utveckla och utveckla applikationer för digitala upplevelser.

## Kontrollpanel för identiteter {#identity-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_identity_processing"
>title="Identitetsbearbetning"
>abstract="I vyn Identitetsbearbetning finns information om poster som har importerats till identitetstjänsten, inklusive antalet identiteter som har lagts till, diagram som har skapats och diagram som har uppdaterats. Läs måttdefinitionsguiden om du vill veta mer om mått och diagram."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_identity"
>title="Information om dataflödeskörning"
>abstract="På sidan med information om dataflödeskörning visas mer information om Identity-dataflödets körning, inklusive dess organisations-ID och dataflödes-ID."

Så här öppnar du **[!UICONTROL Identities]** kontrollpanel, välja **[!UICONTROL Monitoring]** i den vänstra navigeringen. På **[!UICONTROL Monitoring]** väljer du **[!UICONTROL Identities]** kort.

![Identitetskortet. Information om antalet mottagna poster, antalet importerade poster och antalet lyckade försök visas.](../assets/ui/monitor-identities/focus-card.png)

På vänster sida **[!UICONTROL Identities]** kontrollpanelen, **[!UICONTROL Identities]** kortet innehåller information om det totala antalet mottagna poster, antalet importerade poster samt antalet lyckade inspelningar.

Instrumentpanelen i sig innehåller statistik om identitetsbearbetning. Instrumentpanelen visar som standard information om identitetsbearbetning för organisationens källor de senaste 24 timmarna.

![Kontrollpanelen Identiteter. Information om antalet mottagna poster per källa visas.](../assets/ui/monitor-identities/sources.png)

The [!UICONTROL Identity processing] sidan innehåller information om poster som har importerats till [!DNL Identity Service], inklusive antal tillagda identiteter, skapade diagram och uppdaterade diagram.

Följande mått är tillgängliga för den här instrumentpanelsvyn:

| Identitetsmått | Beskrivning |
| ---------------- | ----------- |
| **[!UICONTROL Records received]** | Antalet poster som tagits emot från datasjön. |
| **[!UICONTROL Records failed]** | Antalet poster som inte har importerats till plattformen på grund av datafel. |
| **[!UICONTROL Records skipped]** | Antalet poster som har importerats, men inte [!DNL Identity Service] därför att det bara fanns en identifierare i postraden. |
| **[!UICONTROL Records ingested]** | Antalet poster som inhämtats till [!DNL Identity Service]. |
| **[!UICONTROL Identities added]** | Antalet nya nettoidentifierare som lagts till i [!DNL Identity Service]. |
| **[!UICONTROL Graphs created]** | Antalet nya identitetsdiagram som skapas i [!DNL Identity Service]. |
| **[!UICONTROL Graphs updated]** | Antalet befintliga identitetsdiagram som uppdaterats med nya kanter. |
| **[!UICONTROL Total failed dataflows]** | Antalet misslyckade dataflödeskörningar. |

Du kan välja filterikonen ![Filterikon](../assets/ui/monitor-identities/filter.png) bredvid källnamnet för att se information om identitetsbearbetning för den valda källans dataflöden.

![Filterikonen är markerad. Om du väljer den här ikonen kan du visa den valda källans dataflöden.](../assets/ui/monitor-identities/sources-filter.png)

Du kan också välja **[!UICONTROL Dataflows]** på pekskärmen för att se information om identitetsbearbetning för organisationens dataflöden de senaste 24 timmarna.

![Kontrollpanelen Identiteter. Information om antalet identiteter som tas emot per dataflöde visas.](../assets/ui/monitor-identities/dataflows.png)

Följande mått är tillgängliga för den här instrumentpanelsvyn:

| Mått | Beskrivning |
| -------| ----------- |
| **[!UICONTROL Dataflow]** | Dataflödets namn. |
| **[!UICONTROL Dataset]** | Namnet på datauppsättningen som dataflödet infogas i. |
| **[!UICONTROL Source name]** | Namnet på källan som dataflödet tillhör. |
| **[!UICONTROL Records received]** | Antalet poster som tagits emot från datasjön. |
| **[!UICONTROL Records failed]** | Antalet poster som inte har importerats till plattformen på grund av datafel. |
| **[!UICONTROL Records skipped]** | Antalet poster som har importerats, men inte [!DNL Identity Service] därför att det bara fanns en identifierare i postraden. |
| **[!UICONTROL Records ingested]** | Antalet poster som inhämtats till [!DNL Identity Service]. |
| **[!UICONTROL Total records]** | Totalt antal poster, inklusive poster som misslyckats, poster som hoppats över, identiteter som lagts till och dubblerade poster. |
| **[!UICONTROL Identities added]** | Antalet nya nettoidentifierare som lagts till i [!DNL Identity Service]. |
| **[!UICONTROL Graphs created]** | Antalet nya identitetsdiagram som skapas i [!DNL Identity Service]. |
| **[!UICONTROL Graphs updated]** | Antalet befintliga identitetsdiagram som uppdaterats med nya kanter. |
| **[!UICONTROL Total failed dataflows]** | Antalet misslyckade dataflödeskörningar. |

Markera filterikonen ![filter](../assets/ui/monitor-identities/filter.png) bredvid starttiden för dataflödet för att se mer information om [!DNL Identity] dataflödeskörning.

![Filterikonen är markerad. Om du väljer den här ikonen kan du visa information om det markerade dataflödet.](../assets/ui/monitor-identities/dataflows-filter.png)

The [!UICONTROL Dataflow run details] sidan visar mer information om [!DNL Identity] Dataflödeskörning, inklusive dess organisations-ID och dataflödes-ID. På den här sidan visas även motsvarande felkod och felmeddelande från [!DNL Identity Service], om det uppstår några fel i intagsprocessen.

![En kontrollpanel med detaljerad information om det valda dataflödet visas.](../assets/ui/monitor-identities/dataflow-run-details.png)

Följande mått är tillgängliga för den här instrumentpanelsvyn:

| Mått | Beskrivning |
| -------| ----------- |
| **[!UICONTROL Records received]** | Antalet poster som tagits emot från datasjön. |
| **[!UICONTROL Records failed]** | Antalet poster som inte har importerats till plattformen på grund av datafel. |
| **[!UICONTROL Records skipped]** | Antalet poster som har importerats, men inte [!DNL Identity Service] därför att det bara fanns en identifierare i postraden. |
| **[!UICONTROL Records ingested]** | Antalet poster som inhämtats till [!DNL Identity Service]. |
| **[!UICONTROL Identities added]** | Antalet nya nettoidentifierare som lagts till i [!DNL Identity Service]. |
| **[!UICONTROL Graphs created]** | Antalet nya identitetsdiagram som skapas i [!DNL Identity Service]. |
| **[!UICONTROL Graphs updated]** | Antalet befintliga identitetsdiagram som uppdaterats med nya kanter. |
| **[!UICONTROL Status]** | Definierar den övergripande statusen för ett dataflöde. Möjliga statusvärden är: <ul><li>`Success`: Anger att ett dataflöde är aktivt och att data hämtas enligt det schema som det tillhandahölls.</li><li>`Failed`: Anger att aktiveringsprocessen för ett dataflöde har avbrutits på grund av fel. </li><li>`Processing`: Anger att dataflödet ännu inte är aktivt. Denna status inträffar ofta omedelbart efter att ett nytt dataflöde har skapats.</li></ul> |
| **[!UICONTROL Dataflow run start]** | Det datum och den tidpunkt då dataflödet började köras. |
| **[!UICONTROL Last updated]** | Datum och tid då dataflödet senast uppdaterades. |
| **[!UICONTROL Error summary]** | Om dataflödeskörningen misslyckas visas en felkod och en sammanfattning av varför dataflödeskörningen misslyckades. |
| **[!UICONTROL Dataflow run ID]** | ID:t för dataflödeskörningen. |
| **[!UICONTROL IMS org ID]** | Organisations-ID som dataflödeskörningen tillhör. |

Dessutom kan du välja att växla för att visa de poster som misslyckades eller posterna som hoppats över. Felavsnittet innehåller information om felkoden och antalet poster som misslyckades eller uteslutits.
