---
keywords: Experience Platform;hem;populära ämnen;Segmenteringstjänst;segmenteringstjänst;segmenteringstjänst;användarguide;ui guide;segmenteringsguide;segmentbyggare;segmentbyggare;realiserad;befintlig;avslutar;
solution: Experience Platform
title: Användargränssnittshandbok för segmenteringstjänst
description: Adobe Experience Platform segmenteringstjänst innehåller ett användargränssnitt för att skapa och hantera segmentdefinitioner.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '2566'
ht-degree: 0%

---

# Användargränssnittsguide för segmenteringstjänst

[!DNL Adobe Experience Platform Segmentation Service] innehåller ett användargränssnitt för att skapa och hantera segmentdefinitioner.

## Komma igång

Att arbeta med segmentdefinitioner kräver en förståelse för de olika [!DNL Experience Platform] tjänster som rör segmentering. Innan du läser den här användarhandboken bör du läsa dokumentationen för följande tjänster:

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] kan du dela upp data som lagras i [!DNL Experience Platform] som rör individer (t.ex. kunder, prospects, användare eller organisationer) i mindre grupper.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Gör det möjligt att skapa kundprofiler genom att överbrygga identiteter från olika datakällor som hämtas in i [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som [!DNL Platform] organiserar kundupplevelsedata. För att utnyttja segmenteringen på bästa sätt bör du se till att dina data är inmatade som profiler och händelser enligt [bästa praxis för datamodellering](../../xdm/schema/best-practices.md).

Det är också viktigt att känna till två nyckeltermer som används i det här dokumentet och förstå skillnaden mellan dem:
- **Segmentdefinition**: Den regeluppsättning som används för att beskriva nyckelegenskaper eller beteenden för en målgrupp.
- **Målgrupp**: Den resulterande uppsättningen profiler som uppfyller villkoren för en segmentdefinition. Detta kan antingen skapas via Adobe Experience Platform (plattformsgenererad publik) eller från en extern källa (externt genererad publik).

## Översikt

I användargränssnittet för Experience Platform väljer du **[!UICONTROL Segments]** i den vänstra navigeringen för att öppna **[!UICONTROL Overview]** flik som visar [!UICONTROL Segments] kontrollpanel.

>[!NOTE]
>
>Om din organisation inte har använt Platform tidigare och ännu inte har några aktiva profildatauppsättningar eller sammanfogningsprinciper har skapats kan [!UICONTROL Segments] Kontrollpanelen visas inte. I stället [!UICONTROL Overview] På fliken visas länkar och dokumentation som hjälper dig att komma igång med segment.

### [!UICONTROL Segments] kontrollpanel {#segments-dashboard}

The **[!UICONTROL Segments]** Instrumentpanelen sammanfattar nyckeltal relaterade till organisationens segmentdata.

Mer information finns på [instrumentpanelsguide för segment](../../dashboards/guides/segments.md).

![Segmentkontrollpanelen visas. Den visar olika widgetar, inklusive målgruppsstorlek, profiler efter identitet, identitetsövertäckning och trenden för storleksändring för målgrupper.](../../dashboards/images/segments/dashboard-overview.png)

## Bläddra {#browse}

>[!CONTEXTUALHELP]
>id="platform_segments_browse_churncolumnname"
>title="Churn"
>abstract="Kurvan anger den procentandel profiler som ändras inom en segmentdefinition jämfört med den senaste gången segmentjobbet kördes."

>[!CONTEXTUALHELP]
>id="platform_segments_browse_evaluationmethodcolumnname"
>title="Utvärderingsmetod"
>abstract="Utvärderingsmetoder för segment är batch, streaming och edge."

>[!CONTEXTUALHELP]
>id="platform_segments_browse_addallsegmentstoschedule"
>title="Lägg till alla segment i schemat"
>abstract="Aktivera det här alternativet om du vill inkludera alla grupputvärderingssegment i den dagliga schemalagda uppdateringen. Inaktivera borttagning av alla segment från den schemalagda uppdateringen."

Välj **[!UICONTROL Browse]** om du vill visa en lista med alla segmentdefinitioner för din organisation.

![Skärmen för att bläddra bland segment visas. En lista över alla segment som tillhör organisationen visas.](../images/ui/overview/segment-browse-all.png)

I den här vyn visas information om segmentdefinitionen, inklusive antal profiler, datum när de skapades och senaste ändringsdatum.

Du kan lägga till fler fält till den här visningen genom att välja ![filterattributsikonen](../images/ui/overview/filter-attribute.png). Dessa ytterligare fält innehåller information om fördelning, urn, utvärderingsmetod och jobb-ID.

Om du väljer nedbrytning visas ett stolpdiagram som visar procentandelen profiler som tillhör följande lägen: [!UICONTROL Realized], [!UICONTROL Existing]och [!UICONTROL Exiting]. Dessutom visas uppdelningen på [!UICONTROL Browse] är den mest exakta uppdelningen av segmentets status. Om det här talet skiljer sig från vad som anges på [!UICONTROL Overview] använder du siffrorna på fliken [!UICONTROL Browse] -fliken som rätt informationskälla, eftersom [!UICONTROL Overview] bara uppdateras en gång om dagen.

| Status | Beskrivning |
| ------ | ----------- |
| Realiserad | En ny profil inom segmentet. |
| Befintlig | En befintlig profil som finns kvar inom segmentet. |
| Avslutar | En befintlig profil som lämnar segmentet. |

Kurvan anger hur många procent av profilerna som ändras inom en segmentdefinition jämfört med den senaste gången segmentjobbet kördes, medan antalet profiler representerar det totala antalet profiler som kvalificerar sig för segmentet.

Utvärderingsmetoden kan antingen vara direktuppspelning, batch eller kant. Direktuppspelningssegment utvärderas ständigt när data kommer in i systemet. Gruppsegmenten utvärderas enligt ett angivet schema. Kantsegment utvärderas i realtid, vilket möjliggör användning av samma sida och nästa sida vid personalisering.

![Segmenten på segmentets bläddringssida markeras.](../images/ui/overview/segment-browse-segments.png)

Överst på sidan finns alternativ för att lägga till alla segment i ett schema och för att skapa ett nytt segment.

Växlar **[!UICONTROL Add all segments to schedule]** möjliggör schemalagd segmentering. Mer information om schemalagd segmentering finns i [avsnittet med schemalagd segmentering i den här användarhandboken](#scheduled-segmentation).

Markera **[!UICONTROL Create segment]** tar dig till segmentbyggaren. Läs mer om hur du skapar segment i avsnittet om [skapa ett segment i användarhandboken](#create-segment).

![Det övre navigeringsfältet på segmentets bläddringssida är markerat. Det här fältet innehåller en växlingsknapp för att lägga till alla segment i ett schema och en knapp för att skapa ett segment.](../images/ui/overview/segment-browse-top.png)

Den högra sidopanelen innehåller information om alla segment i organisationen, med en lista över det totala antalet segment, det sista utvärderingsdatumet, nästa utvärderingsdatum samt en uppdelning av segmenten efter värderingsmetod.

![Den högra sidofältet på segmentets bläddringssida är markerat. Information om segmenten i organisationen visas. Detta inkluderar information som totalt antal segment, senaste utvärderade tid, nästa utvärderade tid samt en uppdelning av de olika segmenttyperna.](../images/ui/overview/segment-browse-segment-info.png)

Om du markerar segmentdefinitionens rad får du en sammanfattning av segmentdefinitionen, inklusive alternativ för att antingen redigera eller ta bort segmentet, aktivera segmentet till ett mål, kvalificerad målgrupp för segmentet, total målgruppsstorlek, utöver segmentets namn, beskrivning, bedömningsmetod, skapad den och senaste ändringsdatum.

>[!NOTE]
>
> Du kommer att **not** kan ta bort ett segment som används i en målaktivering.

![Information om det valda segmentet visas. Detta innehåller uppgifter om antalet kvalificerade profiler, den procentuella fördelningen av kvalificerade jämfört med totala profiler, senaste utvärderingsdatum.](../images/ui/overview/segment-browse-details.png)

## Segmentdefinitionsinformation {#segment-details}

Om du vill visa mer information om en viss segmentdefinition markerar du ett segmentnamn i **[!UICONTROL Browse]** -fliken.

Sidan med segmentinformation visas. Överst finns en sammanfattning av segmentdefinitionen, information om den kvalificerade målgruppsstorleken samt vilka mål som segmentet är aktiverat för.

![Sidan med segmentdefinitionsinformation visas. Segmentsammanfattningen, den totala målgruppen i segmentet och aktiverade destinationskort markeras.](../images/ui/overview/segment-details-summary.png)

### Segmentsammanfattning {#segment-summary}

The **[!UICONTROL Segment summary]** -avsnittet innehåller information om attribut, till exempel ID, namn, beskrivning och detaljer.

Dessutom kan du antingen aktivera segmentet till ett mål eller redigera segmentet. Markera **[!UICONTROL Activate to destination]** Med kan du aktivera segmentet till ett mål. Mer information om hur du aktiverar ett segment till ett mål finns i [aktiveringsöversikt](../../destinations/ui/activation-overview.md).

![Knappen Aktivera till mål är markerad.](../images/ui/overview/segment-details-activate.png)

Markera **[!UICONTROL Edit segment]** kommer att ta dig till [!DNL Segment Builder]. Mer detaljerad information om hur du använder [!DNL Segment Builder] arbetsytan, läs [[!DNL Segment Builder] användarhandbok](./segment-builder.md).

![](../images/ui/overview/segment-details-edit-segment.png)

### Total publik i segmentet

The **[!UICONTROL Total audience in segment]** visar det totala antalet profiler som är kvalificerade för segmentet.

Uppskattningar genereras med en provstorlek för den aktuella dagens exempeldata. Om det finns mindre än 1 miljon enheter i din profilbutik används hela datauppsättningen. För mellan 1 och 20 miljoner enheter används 1 miljon enheter. och för över 20 miljoner enheter används 5 % av det totala antalet enheter. Mer information om hur du genererar segmentuppskattningar finns i [uppskattningsgenereringsavsnitt](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) av självstudiekursen för att skapa segment.

### Aktiverade destinationer

The **[!UICONTROL Activated destinations]** visas de mål som det här segmentet är aktiverat för.

>[!NOTE]
>
> Destinationer är en funktion som är tillgänglig med [!DNL Adobe Real-Time Customer Data Platform]och gör att du kan exportera data till externa plattformar. Mer information om destinationer finns i [destinationer, översikt](../../destinations/home.md). Mer information om hur du aktiverar ett segment till ett mål finns i [aktiveringsöversikt](../../destinations/ui/activation-overview.md).

### Profilexempel

Under finns ett urval profiler som är kvalificerade för segmentet, med detaljerad information, inklusive [!DNL Profile] ID, förnamn, efternamn och personlig e-post.

Det sätt på vilket datainsamling utlöses beror på metoden för intag.

För batchimport skannas profilarkivet automatiskt var 15:e minut för att se om en ny batch har importerats sedan den senaste samplingsjobbet kördes. Om så är fallet genomsöks sedan profilarkivet för att se om det har skett minst 5 procents ändring av antalet poster. Om dessa villkor uppfylls utlöses ett nytt samplingsjobb.

För direktuppspelningsinläsning genomsöks profilarkivet automatiskt varje timme för att se om det har skett minst 5 procents ändring av antalet poster. Om det här villkoret är uppfyllt utlöses ett nytt samplingsjobb.

Exempelstorleken för genomsökningen beror på det totala antalet enheter i din profilbutik. De här exempelstorlekarna visas i följande tabell:

| Enheter i profilarkivet | Samplingsstorlek |
| ------------------------- | ----------- |
| Mindre än 1 miljon | Fullständig datauppsättning |
| 1 till 20 miljoner | 1 miljon |
| Över 20 miljoner | 5 % av det totala |

Mer detaljerad information om varje [!DNL Profile] kan du se genom att välja [!DNL Profile] ID. Mer information om en profils detaljer finns i [[!DNL Real-Time Customer Profile] användarhandbok](../../profile/ui/user-guide.md#profile-detail).

![Exempelprofilerna för segmentdefinitionen markeras. Exempelprofilinformationen innehåller profil-ID, förnamn, efternamn och personens e-postadress.](../images/ui/overview/segment-details-profiles.png)

## Skapa ett segment {#create-segment}

Markera **[!UICONTROL Create segment]** i det övre högra hörnet öppnas [!DNL Segment Builder] arbetsyta där du kan börja skapa en segmentdefinition.

![Knappen Skapa segment är markerad på sidan Segmentbläddring.](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] arbetsyta

[!DNL Segment Builder] innehåller en omfattande arbetsyta som du kan använda för att interagera med [!DNL Profile] dataelement. Arbetsytan innehåller intuitiva kontroller för att skapa och redigera regler, till exempel dra-och-släpp-paneler som används för att representera dataegenskaper.

Mer detaljerad information om hur du använder [!DNL Segment Builder] arbetsytan, läs [[!DNL Segment Builder] användarhandbok](./segment-builder.md).

![Arbetsytan Segment Builder visas.](../images/ui/overview/segment-builder.png)

## Schemalagd segmentering {#scheduled-segmentation}

När segmentdefinitionerna har skapats kan du utvärdera dem vid behov eller genom en schemalagd (kontinuerlig) utvärdering. Utvärdering innebär att flytta [!DNL Real-Time Customer Profile] data genom segmentdefinitioner för att producera motsvarande målgrupper. När målgrupperna har skapats sparas och lagras de så att de kan exporteras med [!DNL Experience Platform] API:er.

I On-demand-utvärderingen ingår att använda API:t för att utvärdera och bygga målgrupper efter behov, medan schemalagd utvärdering (även kallat schemalagd segmentering) gör att du kan skapa ett återkommande schema för att utvärdera segmentdefinitioner vid en viss tidpunkt (högst en gång om dagen).

### Aktivera schemalagd segmentering {#enable-scheduled-segmentation}

Du kan aktivera dina segmentdefinitioner för schemalagd utvärdering med hjälp av gränssnittet eller API:t. I användargränssnittet går du tillbaka till **[!UICONTROL Browse]** tabba i **[!UICONTROL Segments]** och aktivera **[!UICONTROL Add all segments to schedule]**. Detta gör att alla segment utvärderas baserat på det schema som angetts av organisationen.

>[!NOTE]
>
>Schemalagd utvärdering kan aktiveras för sandlådor med högst fem (5) sammanfogningsprinciper för [!DNL XDM Individual Profile]. Om din organisation har fler än fem samkörningspolicyer för [!DNL XDM Individual Profile] i en enda sandlådemiljö kommer du inte att kunna använda schemalagd utvärdering.

Scheman kan för närvarande bara skapas med API:t. Följ självstudiekursen för att utvärdera och komma åt segmentresultaten, särskilt avsnittet om hur du skapar, redigerar och arbetar med scheman med API:t. [schemalagd utvärdering med API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![Alternativet för att lägga till alla segment i ett schema är markerat på sidan Bläddra efter segment.](../images/ui/overview/segment-browse-scheduled.png)

## Målgrupper {#audiences}

>[!IMPORTANT]
>
>Målgruppsfunktionen är för närvarande i begränsad betaversion och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

Välj **[!UICONTROL Audiences]** om du vill se en lista över alla målgrupper för din organisation.

![En lista över målgrupper för organisationen.](../images/ui/overview/list-audiences.png)

Som standard visas information om målgrupperna inklusive namn, antal profiler, ursprung, datum när de skapades och senaste ändringsdatum.

Du kan välja ![Anpassa tabell](../images/ui/overview/customize-table.png) om du vill ändra vilka fält som visas.

![Knappen Anpassa tabell är markerad. Om du väljer den här knappen kan du anpassa fälten som visas på publikens webbsida.](../images/ui/overview/select-customize-table.png)

En pover visas med en lista över alla fält som kan visas i tabellen.

![De attribut som kan visas för avsnittet Bläddra bland målgrupper.](../images/ui/overview/customize-table-attributes.png)

| Fält | Beskrivning |
| ----- | ----------- | 
| [!UICONTROL Name] | Publiken. |
| [!UICONTROL Profile count] | Det totala antalet profiler som är kvalificerade för målgruppen. |
| [!UICONTROL Origin] | Målgruppens ursprung. Om den här målgruppen genererades av en plattform har den sin ursprung i segmenteringstjänsten. |
| [!UICONTROL Lifecycle status] | Status för målgruppen. Möjliga värden för det här fältet är `Draft`, `Published`och `Archived`. |
| [!UICONTROL Update frequency] | Ett värde som anger hur ofta målgruppens data uppdateras. Möjliga värden för det här fältet är `On Demand`, `Scheduled`och `Continuous`. |
| [!UICONTROL Last updated by] | Namnet på den person som senast uppdaterade målgruppen. |
| [!UICONTROL Created] | Tid och datum då målgruppen skapades. |
| [!UICONTROL Last updated] | Tid och datum då målgruppen senast skapades. |
| [!UICONTROL Access labels] | Åtkomstetiketterna för målgruppen. Med åtkomstetiketter kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Dessa etiketter kan användas när som helst, vilket ger flexibilitet i hur du vill styra data. Mer information om åtkomstetiketter finns i dokumentationen om [hantera etiketter](../../access-control/abac/ui/labels.md). |

Du kan välja **[!UICONTROL Create Audience]** för att skapa en publik.

![Knappen Skapa målgrupp är markerad och visar var du ska välja för att skapa en målgrupp.](../images/ui/overview/create-audience.png)

En pover visas där du kan välja mellan att sätta ihop en målgrupp eller skapa regler.

![En pover som visar de två typer av målgrupper du kan skapa.](../images/ui/overview/create-audience-type.png)

Markera **[!UICONTROL Compose Audiences]** tar dig till Audience Builder. Läs mer om hur du skapar målgrupper i [Guiden Audience Builder](./audience-builder.md).

Markera **[!UICONTROL Build Rule]** tar dig till segmentbyggaren. Läs mer om hur du skapar segment i [Segment Builder Guide](./segment-builder.md)

## Målgruppsinformation {#audience-details}

Om du vill ha mer information om en viss målgrupp väljer du en målgrupps namn i [!UICONTROL Audiences] -fliken.

Sidan med målgruppsinformation visas. Den här sidan skiljer sig åt i detaljer beroende på om målgruppen skapades med Adobe Experience Platform eller från en extern källa som Audience Orchestration.

### Plattformsgenererad publik

Mer information om plattformsgenererade målgrupper finns i [segmentsammanfattningsavsnitt](#segment-summary).

### Externt genererad publik

Ovanför sidan med målgruppsinformation finns en sammanfattning av målgruppen och detaljer om den datauppsättning som målgruppen sparas i.

![Den angivna informationen för en externt genererad publik.](../images/ui/overview/externally-generated-audience.png)

The **[!UICONTROL Audience summary]** -avsnittet innehåller information om attribut, till exempel ID, namn, beskrivning och detaljer.

The **[!UICONTROL Dataset details]** -avsnittet innehåller information som namn, beskrivning, tabellnamn, källa och schema. Du kan välja **[!UICONTROL View dataset]** om du vill ha mer information om datauppsättningen.

| Fält | Beskrivning |
| ----- | ----------- |
| [!UICONTROL Name] | Datauppsättningens namn. |
| [!UICONTROL Description] | Beskrivning av datauppsättningen. |
| [!UICONTROL Table name] | Datauppsättningens tabellnamn. |
| [!UICONTROL Source] | Datamängdens källa. För externt genererade målgrupper kommer det här värdet att **Schema**. |
| [!UICONTROL Schema] | Den typ av XDM-schema som datauppsättningen motsvarar. |

Läs mer om datauppsättningar i [datauppsättningsöversikt](../../catalog/datasets/overview.md).

## Direktuppspelningssegmentering {#streaming-segmentation}

Direktuppspelningssegmentering är möjligheten att segmentera på [!DNL Platform] i nära realtid, samtidigt som datamöjligheter fokuseras. Med direktuppspelningssegmentering sker nu segmentkvalificeringen när data når [!DNL Platform], vilket minskar behovet av att schemalägga och köra segmenteringsjobb.

Mer information om direktuppspelningssegmentering finns i [användarhandbok för direktuppspelningssegmentering](./streaming-segmentation.md).

>[!NOTE]
>
>För att direktuppspelningssegmenteringen ska fungera måste du aktivera schemalagd segmentering för organisationen. Mer information om att aktivera schemalagd segmentering finns i [avsnittet om direktuppspelningssegmentering i den här användarhandboken](#scheduled-segmentation).

## Kantsegmentering {#edge-segmentation}

Kantsegmentering är möjligheten att utvärdera segment i plattformen direkt, vilket möjliggör användning av samma sida och nästa sida.

Mer information om kantsegmentering finns i [gränssnittsguide för kantsegmentering](./edge-segmentation.md)

## Policyöverträdelser

>[!NOTE]
>
>Policyöverträdelser gäller bara om du skapar ett segment som har tilldelats ett mål.

När du är klar med segmentet analyseras segmentet av Adobe Experience Platform Data Governance för att säkerställa att det inte förekommer några överträdelser av policyer inom segmentet. Se [Datastyrning - översikt](../../data-governance/home.md) för mer information.

![Policyöverträdelser för segmentet visas.](../images/ui/overview/segment-dule-policy-violations.png)

## Nästa steg och ytterligare resurser {#next-steps}

The [!DNL Segmentation Service] Gränssnittet innehåller ett omfattande arbetsflöde som gör det möjligt att isolera marknadsmässiga målgrupper från [!DNL Real-Time Customer Profile] data.

Mer information om [!DNL Segmentation Service], fortsätt att läsa dokumentationen. Så här använder du [!DNL Segmentation Service] API, läs [[!DNL Segmentation Service] utvecklarhandbok](../api/overview.md).
