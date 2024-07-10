---
title: Översikt över målportalen
description: Lär dig hur du använder Audience Portal för att visa, hantera och skapa målgrupper i Adobe Experience Platform.
source-git-commit: 531bee643c14ad407a1207cca9093e210e5227a5
workflow-type: tm+mt
source-wordcount: '3478'
ht-degree: 0%

---


# Översikt över målgruppsportalen

Audience Portal är ett centralt nav i Adobe Experience Platform som gör att ni kan visa, hantera och skapa målgrupper.

I Audience Portal kan du utföra följande uppgifter:

- [Visa en lista över era målgrupper](#audience-list)
   - [Använd snabba åtgärder på era målgrupper](#quick-actions)
   - [Anpassa egenskaperna som visas i din lista över målgrupper](#customize)
   - [Använd filter, mappar och taggar för att ordna era målgrupper](#manage-audiences)
- [Visa information om er målgrupp](#audience-details)
   - [Se en sammanfattning om er målgrupp](#audience-summary)
- [Aktivera era målgrupper för schemalagd segmentering](#scheduled-segmentation)
- [Skapa en målgrupp](#create-audience)
   - [Använd Segment Builder för att skapa en målgrupp](#segment-builder)
   - [Använd Audience Composition för att skapa en målgrupp](#audience-composition)
- [Importera externt genererade målgrupper](#import-audience)

Om du vill öppna målportalen väljer du **[!UICONTROL Browse]** -fliken i segmenteringssektionen.

## Målgruppslista {#list}

>[!CONTEXTUALHELP]
>id="platform_segments_browse_churncolumnname"
>title="Churn"
>abstract="Förändringen representerar den procentandel profiler som ändras inom en målgrupp jämfört med den senaste gången segmentjobbet kördes."

>[!CONTEXTUALHELP]
>id="platform_segments_browse_evaluationmethodcolumnname"
>title="Utvärderingsmetod"
>abstract="Utvärderingsmetoder för målgrupper är bland annat batch, strömning och edge."

Som standard visar Audience Portal en lista över alla målgrupper i din organisation och sandlåda, inklusive antal profiler, ursprung, skapat datum, senaste ändringsdatum, taggar och uppdelning.

![Bläddringsskärmen visas. En lista över alla målgrupper som tillhör organisationen visas.](../images/ui/audience-portal/audience-browse.png)

### Snabbåtgärder {#quick-actions}

Bredvid varje publik finns en ellips-ikon. Om du väljer det här alternativet visas en lista med tillgängliga snabbåtgärder för målgruppen. Listan med åtgärder skiljer sig åt beroende på målgruppens ursprung.

![Listan med snabbåtgärder visas för målgrupper med ursprung i [!UICONTROL Audience composition].](../images/ui/audience-portal/browse-audience-composition-details.png)

| Åtgärd | Original | Beskrivning |
| ------ | ------- | ----------- |
| [!UICONTROL Edit] | Segmenteringstjänst | Öppnar segmentbyggaren för att redigera målgruppen. Observera att om målgruppen skapades via API:t kommer du att **not** kan redigera den med hjälp av segmentbyggaren. Mer information om hur du använder Segment Builder finns i [Användargränssnittsguide för segmentbyggare](./segment-builder.md). |
| [!UICONTROL Open composition] | Målgruppskomposition | Öppnar Audience-kompositionen för att se er målgrupp. Mer information om publikens sammansättning finns i [gränssnittsguide för målgruppskomposition](./audience-composition.md). |
| [!UICONTROL Activate to destination] | Segmenteringstjänst | Aktiverar målgruppen till ett mål. Mer information om hur man aktiverar en målgrupp finns i [aktiveringsöversikt](../../destinations/ui/activation-overview.md). |
| [!UICONTROL Share with partners] | Målgruppskomposition, anpassad överföring, segmenteringstjänst | Delar er målgrupp med andra plattformsanvändare. Mer information om den här funktionen finns i [Översikt över segmentmatchning](./segment-match/overview.md). |
| [!UICONTROL Manage tags] | Målgruppskomposition, anpassad överföring, segmenteringstjänst | Hanterar de användardefinierade taggar som tillhör målgruppen. Mer information om funktionen finns i avsnittet om [filtrering och taggning](#manage-audiences). |
| [!UICONTROL Move to folder] | Målgruppskomposition, anpassad överföring, segmenteringstjänst | Hanterar den mapp som målgruppen tillhör. Mer information om funktionen finns i avsnittet om [filtrering och taggning](#manage-audiences). |
| [!UICONTROL Copy] | Segmenteringstjänst | Duplicerar den valda målgruppen. Mer information om den här funktionen finns i [Vanliga frågor om segmentering](../faq.md#copy). |
| [!UICONTROL Apply access labels] | Målgruppskomposition, anpassad överföring, segmenteringstjänst | Hanterar de åtkomstetiketter som tillhör målgruppen. Mer information om åtkomstetiketter finns i dokumentationen om [hantera etiketter](../../access-control/abac/ui/labels.md). |
| [!UICONTROL Publish] | Anpassad överföring, segmenteringstjänst | Publicerar den valda målgruppen. Mer information om hantering av livscykelstatus finns i [livscykelstatusavsnittet i Vanliga frågor om segmentering](../faq.md#lifecycle-states). |
| [!UICONTROL Deactivate] | Anpassad överföring, segmenteringstjänst | Inaktiverar den valda målgruppen. Mer information om hantering av livscykelstatus finns i [livscykelstatusavsnittet i Vanliga frågor om segmentering](../faq.md#lifecycle-states). |
| [!UICONTROL Delete] | Målgruppskomposition, anpassad överföring, segmenteringstjänst | Tar bort den valda målgruppen. Målgrupper som används i senare led eller som är beroende i andra målgrupper **inte** tas bort. Mer information om borttagning av målgrupper finns i [segmentering - frågor och svar](../faq.md#lifecycle-states). |
| [!UICONTROL Add to package] | Målgruppskomposition, anpassad överföring, segmenteringstjänst | Flyttar publiken mellan sandlådor. Mer information om den här funktionen finns i [verktygshandbok för sandlådor](../../sandboxes/ui/sandbox-tooling.md). |

>[!IMPORTANT]
>
>Innan du tar bort målgruppen bör du kontrollera att målgruppen **not** används som en komponent i en kontobaserad målgrupp eller används i Adobe Journey Optimizer.

Överst på sidan finns alternativ för att lägga till alla målgrupper i ett schema, importera en målgrupp, skapa en ny målgrupp och visa en sammanfattning av målgruppsutvärderingen.

Växlar **[!UICONTROL Schedule all audiences]** möjliggör schemalagd segmentering. Mer information om schemalagd segmentering finns i [avsnittet med schemalagd segmentering i den här användarhandboken](#scheduled-segmentation).

Markera **[!UICONTROL Import audience]** kan du importera en externt genererad publik. Läs mer om att importera målgrupper i avsnittet om [importera en målgrupp i användarhandboken](#import-audience).

Markera **[!UICONTROL Create audience]** kan ni skapa en målgrupp. Läs mer om hur du skapar målgrupper i avsnittet om [skapa en målgrupp i användarhandboken](#create-audience).

![Det övre navigeringsfältet på målgruppens webbsida är markerat. Det här fältet innehåller en knapp för att skapa en målgrupp och en knapp för att importera en målgrupp.](../images/ui/audience-portal/browse-audiences-top.png)

Du kan välja **[!UICONTROL Evaluation summary]** för att visa ett cirkeldiagram som visar en sammanfattning av publikens utvärderingar.

![Knappen Utvärderingssammanfattning är markerad.](../images/ui/audience-portal/browse-audience-evaluation-summary.png)

Cirkeldiagrammet visas med en uppdelning av målgrupperna efter målgruppsutvärdering. Diagrammet visar det totala antalet målgrupper i mitten och den dagliga batchutvärderingstiden i UTC längst ned. Om du hovrar över de olika delarna av publiken visas antalet målgrupper som tillhör varje uppdateringsfrekvenstyp.

![Pajerdiagrammet för målgruppsutvärdering är markerat och utvärderingstiden för gruppsegmentering visas också.](../images/ui/audience-portal/evaluation-summary.png)

### Anpassa {#customize}

Du kan lägga till ytterligare fält i målportalen genom att välja ![filterattributsikonen](../images/ui/audience-portal/filter-attribute.png). Dessa ytterligare fält innehåller livscykelstatus, uppdateringsfrekvens, senast uppdaterad av, beskrivning, skapad av och åtkomstetiketter.

| Fält | Beskrivning |
| ----- | ----------- |
| [!UICONTROL Name] | Namnet på publiken. |
| [!UICONTROL Profile count] | Det totala antalet profiler som är kvalificerade för målgruppen. |
| [!UICONTROL Origin] | Målgruppens ursprung. Det är här som publiken kommer ifrån. Möjliga värden är Segmenteringstjänst, Anpassad överföring, Målgruppskomposition och Audience Manager. |
| [!UICONTROL Lifecycle status] | Publiken. Möjliga värden för det här fältet är `Draft`, `Inactive`och `Published`. Mer information om livscykelstadier, inklusive vad de olika stadierna innebär och hur du flyttar målgrupper till olika livscykeltillstånd finns i [livscykelstatusavsnittet i Frågor och svar om segmentering](../faq.md#lifecycle-status). |
| [!UICONTROL Update frequency] | Ett värde som anger hur ofta målgruppens data uppdateras. Möjliga värden för det här fältet är [!UICONTROL Batch], [!UICONTROL Streaming], [!UICONTROL Edge]och [!UICONTROL Not Scheduled]. |
| [!UICONTROL Last updated by] | Namnet på den person som senast uppdaterade målgruppen. |
| [!UICONTROL Created] | Datum och tid, i UTC, då målgruppen skapades. |
| [!UICONTROL Last updated] | Datum och tid, i UTC, då målgruppen senast uppdaterades. |
| [!UICONTROL Tags] | De användardefinierade taggar som tillhör målgruppen. Mer information om de här taggarna finns i [avsnitt om taggar](#tags). |
| [!UICONTROL Description] | Beskrivning av målgruppen. |
| [!UICONTROL Created by] | Namnet på den person som skapade målgruppen. |
| [!UICONTROL Access labels] | Åtkomstetiketterna för målgruppen. Med åtkomstetiketter kan du kategorisera datauppsättningar och fält enligt de användarprofiler som gäller för dessa data. Dessa etiketter kan användas när som helst, vilket ger flexibilitet i hur du vill styra data. Mer information om åtkomstetiketter finns i dokumentationen om [hantera etiketter](../../access-control/abac/ui/labels.md). |
| [!UICONTROL Breakdown] | Uppdelning av profilstatus för målgruppen. En mer detaljerad beskrivning av den här profilstatusuppdelningen finns nedan. |

Om nedbrytning är markerat visas ett stolpdiagram som visar procentandelen profiler som tillhör följande beräknade profilstatusar: [!UICONTROL Realized], [!UICONTROL Existing]och [!UICONTROL Exiting]. Dessutom visas uppdelningen på [!UICONTROL Browse] tab är den mest exakta uppdelningen av segmentdefinitionsstatusen. Om det här talet skiljer sig från vad som anges på [!UICONTROL Overview] använder du siffrorna på fliken [!UICONTROL Browse] -fliken som rätt informationskälla, eftersom [!UICONTROL Overview] bara uppdateras en gång om dagen.

| Status | Beskrivning |
| ------ | ----------- |
| [!UICONTROL Realized] | Antalet profiler som **kvalificerad** för segmentet de senaste 24 timmarna sedan det senaste batchsegmentjobbet kördes. |
| [!UICONTROL Existing] | Antal profiler som **finns kvar** i segmentet de senaste 24 timmarna sedan det senaste batchsegmentjobbet kördes. |
| [!UICONTROL Exiting] | Antal profiler som **avslutad** segmentet de senaste 24 timmarna sedan det senaste batchsegmentjobbet kördes. |

När du har markerat de fält som du vill visa kan du även ändra storlek på de visade kolumnernas bredd. Du kan antingen göra detta genom att dra området mellan kolumnerna eller genom att markera ![pilikon](../images/ui/audience-portal/arrow-icon.png) i kolumnen som du vill ändra storlek på, följt av **[!UICONTROL Resize column]**.

![Kolumnknappen Ändra storlek är markerad.](../images/ui/audience-portal/browse-audience-resize-column.png)

### Filtrering, mappar och taggning {#manage-audiences}

För att effektivisera arbetet kan du söka efter befintliga målgrupper, lägga till användardefinierade taggar till målgrupper, placera målgrupper i mappar och filtrera de visade målgrupperna.

#### Sök {#search}

Du kan söka bland befintliga målgrupper på upp till 9 olika språk med [!DNL Unified Search].

Används [!DNL Unified Search]lägger du till den term du vill söka efter i det markerade sökfältet.

![Sökfältet är markerat.](../images/ui/audience-portal/browse-audience-search.png)

Mer information om [!DNL Unified Search], inklusive funktioner som stöds, läs [Enhetlig sökdokumentation](https://experienceleague.adobe.com/docs/core-services/interface/services/search-experience-cloud.html).

#### Taggar {#tags}

Du kan lägga till användardefinierade taggar för att bättre beskriva, hitta och hantera era målgrupper.

Om du vill lägga till en tagg väljer du **[!UICONTROL Manage tags]** på den målgrupp du vill tagga.

![The [!UICONTROL Manage tags] knappen är markerad för en angiven målgrupp.](../images/ui/audience-portal/browse-manage-tags.png)

The **[!UICONTROL Manage tags]** popover visas. I den här drivrutinen kan du antingen välja en kategoriserad tagg eller en okategoriserad tagg.

| Tagg type | Beskrivning |
| -------- | ----------- |
| Kategoriserad | En tagg som skapas och hanteras av organisationens administratörer. |
| Okategoriserad | En tagg som skapas i [!UICONTROL Manage tags] popover. Vem som helst kan skapa eller hantera de här taggtyperna. |

![The [!UICONTROL Manage tags] popover visas. Alternativen för att välja en kategoriserad eller okategoriserad markeras.](../images/ui/audience-portal/create-tag.png)

När du har lagt till alla taggar som du vill bifoga till målgruppen väljer du **[!UICONTROL Save]**.

![På [!UICONTROL Manage tags] pover markeras de tillagda taggarna.](../images/ui/audience-portal/created-tags.png)

Mer information om hur du skapar och hanterar taggar finns i [Hantera taggar, guide](../../administrative-tags/ui/managing-tags.md).

#### Mappar {#folders}

Ni kan placera målgrupper i mappar för bättre målgruppshantering.

Om du vill flytta en målgrupp till en mapp väljer du **[!UICONTROL Move to folder]** på den målgrupp ni vill flytta.

![The [!UICONTROL Move to folder] knappen är markerad för en viss målgrupp.](../images/ui/audience-portal/browse-move-to-folder.png)

The **Flytta målgrupp till mapp** popover visas. Markera mappen som du vill flytta målgruppen till och välj sedan **[!UICONTROL Save]**.

![Flyttar målgruppen till mappposeringen visas. Mappen som målgruppen ska flyttas till markeras.](../images/ui/audience-portal/move-to-folder.png)

När målgruppen finns i en mapp kan du välja att bara visa målgrupper som tillhör en viss mapp.

![Publiker som tillhör en viss mapp visas.](../images/ui/audience-portal/browse-folders.png)

#### Filter {#filter}

Du kan även filtrera dina målgrupper baserat på en mängd olika inställningar.

Om du vill filtrera de tillgängliga målgrupperna väljer du ![filterikon](../images/ui/audience-portal/filter-icon.png).

![Sidan Bläddra bland målgrupper visas med filterikonen markerad.](../images/ui/audience-portal/browse-select-filter.png)

Listan med tillgängliga filter visas.

| Filter | Beskrivning |
| ------ | ----------- |
| [!UICONTROL Origin] | Gör att du kan filtrera baserat på målgruppens ursprung. De tillgängliga alternativen är Segmenteringstjänst, Anpassad överföring, Målgruppskomposition och Audience Manager. |
| [!UICONTROL Has any tag] | Gör att du kan filtrera efter taggar. Du kan välja mellan **[!UICONTROL Has any tag]** och **[!UICONTROL Has all tags]**. När **[!UICONTROL Has any tag]** är markerat kommer de filtrerade målgrupperna att inkludera **alla** av de taggar som du har lagt till. När **[!UICONTROL Has all tags]** är markerat måste de filtrerade målgrupperna innehålla **alla** av de taggar som du har lagt till. |
| [!UICONTROL Lifecycle status] | Gör att du kan filtrera baserat på målgruppens livscykelstatus. Tillgängliga alternativ inkluderar [!UICONTROL Deleted], [!UICONTROL Draft], [!UICONTROL Inactive]och [!UICONTROL Published]. |
| [!UICONTROL Update frequency] | Gör att du kan filtrera baserat på målgruppens uppdateringsfrekvens (utvärderingsmetod). Tillgängliga alternativ inkluderar [!UICONTROL Scheduled], [!UICONTROL Continuous]och [!UICONTROL On Demand]. |
| [!UICONTROL Created by] | Gör att du kan filtrera baserat på den person som skapade målgruppen. |
| [!UICONTROL Creation date] | Gör att du kan filtrera baserat på målgruppens skapandedatum. Du kan välja ett datumintervall att filtrera när målgruppen skapades. |
| [!UICONTROL Modified date] | Gör att du kan filtrera baserat på målgruppens senaste ändringsdatum. Du kan välja ett datumintervall som ska filtreras när målgruppen senast ändrades. |

![De tillgängliga filtren visas och markeras på sidan Bläddra bland målgrupper.](../images/ui/audience-portal/filter-audiences.png)

#### Massåtgärder {#bulk-actions}

Dessutom kan ni välja upp till 25 olika målgrupper och utföra olika åtgärder på dessa målgrupper. Dessa åtgärder omfattar [flytta till en mapp](#folders), [redigera eller använda en tagg](#tags), [använda åtkomstetiketter](../../access-control/abac/ui/labels.md)och [ta bort](#browse).

![De tillgängliga alternativen för gruppåtgärder är markerade.](../images/ui/audience-portal/bulk-actions.png)

När du tillämpar gruppåtgärder på dessa målgrupper gäller följande villkor:

- Du **kan** välj målgrupper från olika sidor.
- Du **inte** ta bort en målgrupp som används i en målaktivering.
- Om du väljer ett filter, de valda målgrupperna **kommer** återställ.

## Målgruppsinformation {#audience-details}

Om du vill ha mer information om en viss målgrupp väljer du en målgrupps namn i **[!UICONTROL Browse]** -fliken.

Sidan med målgruppsinformation visas. Dessutom finns det en sammanfattning av målgruppen, information om den kvalificerade målgruppsstorleken samt destinationer som segmentet är aktiverat för.

![Sidan med målgruppsinformation visas. Målgruppssammanfattning, målgruppssumma och aktiverade destinationskort markeras.](../images/ui/audience-portal/audience-details-summary.png)

### Målgruppssammanfattning {#audience-summary}

The **[!UICONTROL Audience summary]** -avsnittet innehåller information som ID, namn, beskrivning, ursprung och detaljer för attributen.

Dessutom får du möjlighet att aktivera målgruppen för ett mål, använda åtkomstetiketter eller redigera/uppdatera målgruppen.

Markera **[!UICONTROL Activate to destination]** Med kan du aktivera målgruppen till ett mål. Mer information om hur man aktiverar en målgrupp finns i [aktiveringsöversikt](../../destinations/ui/activation-overview.md).

![Knappen Aktivera till mål är markerad.](../images/ui/audience-portal/audience-details-activate.png)

Markera **[!UICONTROL Apply access labels]** gör att du kan hantera de åtkomstetiketter som tillhör målgruppen. Mer information om åtkomstetiketter finns i dokumentationen om [hantera etiketter](../../access-control/abac/ui/labels.md).

![Knappen Använd åtkomstetiketter är markerad.](../images/ui/audience-portal/audience-details-access-labels.png)

>[!BEGINTABS]

>[!TAB Målgruppskomposition]

![Sidan med målgruppsinformation visas med [!UICONTROL Open composition] markerad knapp.](../images/ui/audience-portal/audience-details-open-composition.png)

Markera **[!UICONTROL Open composition]** Med kan du visa målgruppen i Audience Composition. Läs mer om Audience Composition [Användargränssnittsguide för målgruppskomposition](./audience-composition.md).

>[!TAB Anpassad överföring]

![Sidan med målgruppsinformation visas med [!UICONTROL Update audience] markerad knapp.](../images/ui/audience-portal/audience-details-update-audience.png)

Markera **[!UICONTROL Update audience]** gör att du kan överföra en externt genererad publik igen. Mer information om hur du importerar en externt genererad publik finns i avsnittet om [importera en publik](#import-audience).

>[!TAB Segmenteringstjänst]

![Sidan med målgruppsinformation visas med [!UICONTROL Edit audience] markerad knapp.](../images/ui/audience-portal/audience-details-edit-audience.png)

Markera **[!UICONTROL Edit audience]** gör att du kan redigera målgruppen i Segment Builder. Mer detaljerad information om hur du använder [!DNL Segment Builder] arbetsytan, läs [[!DNL Segment Builder] användarhandbok](./segment-builder.md).

>[!ENDTABS]

Markera **[!UICONTROL Edit properties]** gör att du kan redigera grundläggande information om målgruppen, till exempel namn, beskrivning och taggar.

![](../images/ui/audience-portal/audience-details-edit-properties.png)

### Målgruppssumma {#audience-total}

The **[!UICONTROL Audience total]** visar det totala antalet profiler som är kvalificerade för målgruppen.

Uppskattningar genereras med en provstorlek för den aktuella dagens exempeldata. Om det finns mindre än 1 miljon enheter i din profilbutik används hela datauppsättningen, för mellan 1 och 20 miljoner enheter används 1 miljon enheter och för över 20 miljoner enheter används 5 % av det totala antalet enheter. Mer information om hur du genererar uppskattningar finns i [uppskattningsgenereringsavsnitt](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) av självstudiekursen för att skapa målgrupper.

### Aktiverade mål {#activated-destinations}

The **[!UICONTROL Activated destinations]** visar de mål som den här målgruppen är aktiverad för.

>[!NOTE]
>
> Destinationer är en funktion med [!DNL Adobe Real-Time Customer Data Platform]och gör att du kan exportera data till externa plattformar. Mer information om destinationer finns i [destinationer, översikt](../../destinations/home.md). Mer information om hur du aktiverar ett segment till ett mål finns i [aktiveringsöversikt](../../destinations/ui/activation-overview.md).

### Profilexempel {#profile-samples}

Under finns ett urval profiler som är kvalificerade för segmentet, med detaljerad information, inklusive [!DNL Profile] ID, förnamn, efternamn och personlig e-post.

Det sätt på vilket datainsamling utlöses beror på metoden för intag.

För batchimport skannas profilarkivet automatiskt var 15:e minut för att se om en ny batch har importerats sedan den senaste samplingsjobbet kördes. I så fall genomsöks sedan profilarkivet för att se om det har skett minst 5 % ändring av antalet poster. Om dessa villkor uppfylls utlöses ett nytt samplingsjobb.

För direktuppspelningsinläsning genomsöks profilarkivet automatiskt varje timme för att se om det har skett minst 5 procents ändring av antalet poster. Om det här villkoret är uppfyllt utlöses ett nytt samplingsjobb.

Exempelstorleken för sökningen beror på det totala antalet enheter i din profilbutik. De här exempelstorlekarna visas i följande tabell:

| Enheter i profilarkivet | Samplingsstorlek |
| ------------------------- | ----------- |
| Mindre än 1 miljon | Fullständig datauppsättning |
| 1 till 20 miljoner | 1 miljon |
| Över 20 miljoner | 5 % av det totala |

Mer detaljerad information om varje [!DNL Profile] kan du se genom att välja [!DNL Profile] ID. Mer information om en profils detaljer finns i [[!DNL Real-Time Customer Profile] användarhandbok](../../profile/ui/user-guide.md#profile-detail).

![Exempelprofilerna för målgruppen markeras. Exempelprofilinformationen innehåller profil-ID, förnamn, efternamn och personens e-postadress.](../images/ui/audience-portal/audience-details-profiles.png)

## Schemalagd segmentering {#scheduled-segmentation}

>[!CONTEXTUALHELP]
>id="platform_segments_browse_addallsegmentstoschedule"
>title="Lägg till alla målgrupper som ska schemaläggas"
>abstract="Gör det möjligt att inkludera alla målgrupper som utvärderats med batchsegmentering i den dagliga schemalagda uppdateringen. Inaktivera borttagning av alla målgrupper från den schemalagda uppdateringen."

När målgrupperna har skapats kan du sedan utvärdera dem via on-demand eller schemalagd (kontinuerlig) utvärdering. Utvärdering innebär att flytta [!DNL Real-Time Customer Profile] data genom segmentjobb för att producera motsvarande målgrupper. När målgrupperna har skapats sparas och lagras de så att de kan exporteras med [!DNL Experience Platform] API.

I On-demand-utvärderingen ingår att använda API:t för att utvärdera och bygga målgrupper efter behov, medan schemalagd utvärdering (även kallat schemalagd segmentering) gör att du kan skapa ett återkommande schema för att utvärdera målgrupper vid en viss tidpunkt (högst en gång om dagen).

### Aktivera schemalagd segmentering {#enable-scheduled-segmentation}

Du kan aktivera dina målgrupper för schemalagd utvärdering med hjälp av gränssnittet eller API:t. Gå tillbaka till användargränssnittet **[!UICONTROL Browse]** tabba i **[!UICONTROL Audiences]** och aktivera **[!UICONTROL Schedule all audiences]**. Detta gör att alla målgrupper utvärderas baserat på det schema som angetts av organisationen.

>[!NOTE]
>
>Schemalagd utvärdering kan aktiveras för sandlådor med högst fem (5) sammanfogningsprinciper för [!DNL XDM Individual Profile]. Om din organisation har fler än fem samkörningspolicyer för [!DNL XDM Individual Profile] i en enda sandlådemiljö kommer du inte att kunna använda schemalagd utvärdering.

Scheman kan för närvarande bara skapas med API:t. Följ självstudiekursen för att utvärdera och komma åt segmenteringsresultat, särskilt avsnittet om hur du skapar, redigerar och arbetar med scheman med API:t. [schemalagd utvärdering med API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![Alternativet för att schemalägga alla målgrupper är markerat på Audience Portal.](../images/ui/audience-portal/browse-audiences-scheduled.png)

## Skapa en målgrupp {#create-audience}

Du kan välja **[!UICONTROL Create audience]** för att skapa en publik.

![Knappen Skapa målgrupp är markerad på sidan Målgruppsbläddring.](../images/ui/audience-portal/browse-create-audience.png)

En pover visas där du kan välja mellan att sätta ihop en målgrupp eller skapa regler.

![En pover som visar de två typer av målgrupper du kan skapa.](../images/ui/audience-portal/create-audience-type.png)

### Målgruppssammansättning {#audience-composition}

Markera **[!UICONTROL Compose audiences]** tar dig till Audience Composition. Den här arbetsytan innehåller intuitiva kontroller för att skapa och redigera målgrupper, till exempel dra-och-släpp-paneler som används för att representera olika åtgärder. Läs mer om hur du skapar målgrupper i [Guide för målgruppssammansättning](./audience-composition.md).

![Arbetsytan för målgruppskomposition visas.](../images/ui/audience-portal/audience-composition.png)

### Segment Builder {#segment-builder}

Markera **[!UICONTROL Build rule]** tar dig till segmentbyggaren. Den här arbetsytan innehåller intuitiva kontroller för att skapa och redigera segmentdefinitioner, till exempel dra-och-släpp-paneler som används för att representera dataegenskaper. Läs mer om hur du skapar segmentdefinitioner i [Segment Builder Guide](./segment-builder.md)

![Arbetsytan Segment Builder visas.](../images/ui/audience-portal/segment-builder.png)

## Importera en målgrupp {#import-audience}

>[!IMPORTANT]
>
>Om du vill importera en externt genererad publik **måste** har följande behörigheter: [!UICONTROL View segments], [!UICONTROL Manage segments]och [!UICONTROL Import audience]. Mer information om dessa behörigheter finns i [åtkomstkontroll - översikt](../../access-control/home.md#permissions).

Du kan välja **[!UICONTROL Import audience]** för att importera en externt genererad publik.

![Knappen Importera målgrupp är markerad på sidan för målgruppsbläddring.](../images/ui/audience-portal/browse-import-audience.png)

The **[!UICONTROL Import audience CSV]** arbetsflödet visas. Du kan välja en CSV-fil som ska importeras som en externt genererad publik.

![I [!UICONTROL Import audience CSV] arbetsflöde, [!UICONTROL Drag and drop files] är markerad och visar var du kan överföra din externt genererade publik.](../images/ui/audience-portal/import-audience-csv.png)

>[!NOTE]
>
>Den externa målgruppen **måste** vara i CSV-format, har **maximum** av 25 kolumner och får vara mindre än 1 GB.

När du har valt den CSV-fil som ska importeras visas en lista med exempeldata för den externt genererade målgruppen. När du har bekräftat att exempeldata är korrekta väljer du **[!UICONTROL Next]**.

![Exempeldata för den externt genererade målgruppen visas.](../images/ui/audience-portal/import-audience-sample-data.png)

The **[!UICONTROL Audience details]** visas. Du kan lägga till information om målgruppen, inklusive namn, beskrivning, primär identitet och ID-namnutrymmesvärde.

När du importerar den externt genererade målgruppen måste du markera en av kolumnerna som primärt identitetsfält och ange namnutrymmesvärde. Observera att alla återstående fält kommer att beaktas **nyttolastattribut**. Dessa attribut beaktas **ej hållbar**, eftersom de bara kommer att kopplas till den här målgruppen för personalisering, och **not** är ansluten till profilen.

![The [!UICONTROL Audience details] visas.](../images/ui/audience-portal/import-audience-audience-details.png)

Du kan också lägga till ytterligare information till den externt genererade målgruppen, som att ge den ett ID, definiera dess sammanfogningsprincip eller redigera dess kolumndatatyp.

>[!NOTE]
>
>Om du använder ett anpassat externt målgrupps-ID måste det följa följande riktlinjer:
>
> - Den **måste** börja med en bokstav (a-z eller A-Z), ett understreck (_) eller ett dollartecken ($).
> - Alla efterföljande tecken kan vara alfanumeriska (a-z, A-Z, 0-9), understreck (_) eller dollartecken ($).

När du fyllt i målgruppsinformationen väljer du **[!UICONTROL Next]**.

![The [!UICONTROL Next] knappen är markerad på [!UICONTROL Audience details] sida.](../images/ui/audience-portal/import-audience-filled-details.png)

The **[!UICONTROL Review]** visas. Du kan granska informationen om den nyligen importerade externt genererade målgruppen.

![The [!UICONTROL Review] visas med information om den nyligen importerade externt genererade målgruppen.](../images/ui/audience-portal/import-audience-review-details.png)

När du har bekräftat att informationen är korrekt väljer du **[!UICONTROL Finish]** för att importera externt genererade målgrupper till Adobe Experience Platform.

>[!IMPORTANT]
>
>Som standard har externt genererade målgrupper en dataförfallotid på 30 dagar. Förfallodatumet för data återställs om målgruppen uppdateras eller ändras på något sätt.
>
>Om den externt genererade publiken dessutom innehåller känslig och/eller vårdrelaterad information, **måste** lägga till nödvändiga etiketter för dataanvändning innan den aktiveras för alla destinationer. Eftersom variabler från externt genererade målgrupper lagras i datasjön i stället för i kundprofilen i realtid bör du **not** inkludera medgivandedata i din CSV-fil. Mer information om användning av dataetiketter finns i dokumentationen om [hantera etiketter](../../access-control/abac/ui/labels.md).

## Nästa steg

När du har läst den här översikten bör du kunna använda Audience Portal för att hantera, skapa och importera målgrupper till Adobe Experience Platform på ett effektivt sätt.

Mer information om hur du använder gränssnittet för segmenteringstjänsten finns i [Översikt över användargränssnittet för segmenteringstjänsten](./overview.md).

Om du vill ha svar på vanliga frågor om Audience Portal kan du läsa [vanliga frågor](../faq.md).
