---
title: Adobe Analytics per contenuti in streaming View in Assurance
description: Den här guiden förklarar hur du använder Adobe Analytics per contenuti in streaming med Adobe Experience Platform Assurance.
exl-id: 9a9c2c64-e9ed-4d58-b936-d802f1c3b7d3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# Adobe Analytics per contenuti in streaming-vy i Assurance

Tack vare integreringen mellan Adobe Analytics per contenuti in streaming och Adobe Experience Platform Assurance kan ni nu validera Media Analytics-implementeringen i mobilappen. I mediaanalysvyer visas vad som spåras i mediesessionen, till exempel:

- Starthändelse för session som innehåller allt innehåll, alla standardmetadata och anpassade metadataegenskaper samt händelser för sessionsslut och sessionsslut.
- Start- och Ad Start-händelser för annonsbrytning med alla annonsegenskaper bifogade, samt Skip- och Complete-händelser för båda.
- Kapitelstart med alla egenskaper bifogade, samt kapitelhoppa och kapitelslutförda händelser.
- Alla uppspelningsändringshändelser (uppspelning, paus, buffert, fel, ändring av bithastighet).
- Alla spårningshändelser för spelarlägesändring (start, slut).

När data har bearbetats i Analytics är status och data som efterbearbetats, till exempel hur mycket tid som har ägnats åt media och den totala paustiden, också tillgängliga i händelsedetaljvyn.

## Komma igång

Kontrollera att du har följande tjänster innan du fortsätter:

- Användargränssnittet för [Adobe Experience Platform-datainsamling](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Läs [implementeringsguiden](../tutorials/implement-assurance.md) om du vill lära dig hur du installerar Assurance i ditt program.

## Använd försäkring med Adobe Analytics per contenuti in streaming

När du har anslutit och konfigurerat din app för Adobe Analytics kan du konfigurera den för Streaming Media Analytics. Längst ned på den vänstra panelen väljer du **[!UICONTROL Configure]** för att lägga till vyn Medieanalyshändelser och **Spara** den.

![Konfigurera](./images/adobe-analytics-streaming-media/configure.png)

När du har lagt till den väljer du vyn **[!UICONTROL Media Analytics Events]** i avsnittet **[!UICONTROL Adobe Analytics]** för att validera sessionsspårningen.

![Välj](./images/adobe-analytics-streaming-media/select.png)

I vyn **[!UICONTROL Media Analytics Events]** kan du söka efter och filtrera efter sessions-ID (VSID) för att visa en specifik mediesession. Om du vill visa ytterligare händelseinformation väljer du en specifik händelse.

![Mediehändelser](./images/adobe-analytics-streaming-media/media-events.png)

Om du vill få en mer koncis vy över API-anrop kan du även dölja uppdateringshändelserna för spelhuvudet genom att välja filtret **[!UICONTROL Hide Playhead Update events]**.

![Dölj spelhuvud](./images/adobe-analytics-streaming-media/hide-playhead.png)

>[!INFO]
>
>För att kunna visa efterbearbetade medieanalysdata måste du använda SDK-versionerna: Android Media 2.1.2 och iOS AEPMedia 3.0.1 (eller senare)

Om du vill visa efterbearbetade data ska du söka efter sessionens starthändelse och validera i statuskolumnen att sessionen har slutförts. Om du är klar klickar du på händelsen för att visa en sammanfattning av mediesessioner i händelsedetaljvyn. Om du vill ha mer information bläddrar du nedåt för att hitta den efterbearbetade informationen.

![Post-bearbetad vy](./images/adobe-analytics-streaming-media/post-processed-view.png)
