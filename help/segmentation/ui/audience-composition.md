---
solution: Experience Platform
title: Användargränssnittshandbok för målgrupper
description: Audience Composition i Adobe Experience Platform UI har en omfattande arbetsyta där du kan interagera med profildataelement. Arbetsytan innehåller intuitiva kontroller för att skapa och redigera målgrupper för din organisation.
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 65a3b5b904a9dfc6a2fbc09ab869e5642e088363
workflow-type: tm+mt
source-wordcount: '2258'
ht-degree: 0%

---

# Användargränssnittsguide för målgruppskomposition

>[!AVAILABILITY]
>
>Om du vill använda den här funktionen måste du ha följande behörigheter:
>
>- Hantera segment
>- Hantera profiler
>- Hantera kopplingsprofiler
>
>Mer information om behörigheter i Experience Platform finns i [åtkomstkontrollsöversikten](../../access-control/home.md#permissions).

>[!NOTE]
>
>Den här guiden förklarar hur du skapar målgrupper med Audience Composition. Om du vill lära dig hur du skapar målgrupper med hjälp av segmentdefinitioner med hjälp av segmentverktyget läser du [gränssnittshandboken för segmentbyggaren](./segment-builder.md).

Audience Composition har en arbetsyta för att bygga och redigera målgrupper med hjälp av block som används för att representera olika åtgärder.

![Gränssnittet för målkomposition.](../images/ui/audience-composition/audience-composition.png)

Om du vill ändra detaljer för kompositionen, inklusive rubrik och beskrivning, väljer du knappen ![reglage](/help/images/icons/properties.png) .

**[!UICONTROL Composition properties]**-pekaren visas. Du kan infoga information om din komposition, inklusive rubriken och beskrivningen här.

![Kompositionsegenskapsdrivrutinen visas.](../images/ui/audience-composition/composition-properties.png)

>[!NOTE]
>
>Om du **inte** ger kompositionen en titel får den titeln &quot;Disposition&quot; följt av datum och tid när den skapades som standard. Dessutom måste varje disposition **måste** ha ett eget unikt namn.

När du har uppdaterat dispositionsinformationen väljer du **[!UICONTROL Save]** för att bekräfta uppdateringarna. Målgruppsarbetsytan visas igen.

Målgruppens kompositionsyta består av fyra olika typer av block: **[[!UICONTROL Audience]](#audience-block)**, **[[!UICONTROL Exclude]](#exclude-block)**, **[[!UICONTROL Rank]](#rank-block)** och **[[!UICONTROL Split]](#split-block)**.

## [!UICONTROL Audience] {#audience-block}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_audience"
>title="Målgrupp"
>abstract="Med Audience-blocket kan ni lägga till de undermålgrupper som ni vill använda för att sätta samman er nya målgrupp."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_merge_types"
>title="Sammanfoga typer"
>abstract="Sammanslagningstyperna avgör hur de valda undermålgrupperna kombineras. Värden som stöds är överlappning mellan Union, Intersection och Exclude."

Med blocktypen **[!UICONTROL Audience]** kan du lägga till de undermålgrupper som du vill använda för att skapa din nya större publik. Som standard inkluderas ett **[!UICONTROL Audience]**-block högst upp på kompositionens arbetsyta.

När du markerar **[!UICONTROL Audience]**-blocket visas kontroller för att märka målgruppen, lägga till målgrupper i blocket samt skapa anpassade regler för målgruppsblocket i den högra listen.

>[!NOTE]
>
>Du kan antingen lägga till målgrupper **eller** för att skapa en anpassad regel. De här två funktionerna **kan inte** användas tillsammans.

![Information om målgruppsblock visas.](../images/ui/audience-composition/audience-block.png)

### [!UICONTROL Add audience] {#add-audience}

Lägga till målgrupper i Audience-blocket. välj **[!UICONTROL Add Audience]**.

![Knappen Lägg till målgrupp är markerad.](../images/ui/audience-composition/select-add-audience.png)

>[!IMPORTANT]
>
>Observera att **endast** målgrupper som definierats med standardprincipen för sammanslagning visas.
>
>Dessutom kan bara **publicerade** målgrupper som skapats med Segment Builder användas. Publiker som skapats med Audience Composition och externt genererade målgrupper är **inte** tillgängliga.

En lista över målgrupper visas. Välj de målgrupper som du vill inkludera, följt av **[!UICONTROL Add]**, för att lägga till dem i ditt målgruppsblock.

![En lista över målgrupper visas. Du kan välja vilken målgrupp du vill lägga till i den här dialogrutan.](../images/ui/audience-composition/select-audience.png)

De valda målgrupperna visas nu i den högra listen när **[!UICONTROL Audience]**-blocket är markerat. Härifrån kan du ändra sammanfogningstypen för de kombinerade målgrupperna.

![Möjliga sammanfogningstyper för målgrupper är markerade.](../images/ui/audience-composition/merge-types.png)

| Sammanfoga typ | Beskrivning |
| ---------- | ----------- |
| [!UICONTROL Union] | Målgrupperna samlas i en och samma målgrupp. Detta motsvarar en OR-åtgärd. |
| [!UICONTROL Intersection] | Målgrupperna kombineras med endast de målgrupper som delas i **alla** av dem som läggs till. Detta motsvarar en AND-åtgärd. |
| [!UICONTROL Exclude overlap] | Målgrupperna kombineras med endast de målgrupper som delas i **en, men inte alla** av dem. Detta motsvarar en XOR-åtgärd. |

### [!UICONTROL Build rule] {#build-rule}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_rule_builder"
>title="Segment Builder"
>abstract="Du kan använda Segment Builder för att lägga till en anpassad regel för din komposition."

Om du vill lägga till en anpassad regel i målgruppsblocket väljer du **[!UICONTROL Build rule]**.

![Knappen Bygg regel är markerad.](../images/ui/audience-composition/select-build-rule.png)

Segmentbyggaren visas. Du kan använda Segment Builder för att skapa en anpassad regel som målgruppen ska följa. Mer information om hur du använder Segment Builder finns i [guiden för segmentbyggaren](./segment-builder.md).

![Gränssnittet för segmentbyggaren visas.](../images/ui/audience-composition/segment-builder.png)

När du har lagt till en anpassad regel väljer du **[!UICONTROL Save]** för att lägga till regeln till din målgrupp.

![](../images/ui/audience-composition/custom-rule.png)

## [!UICONTROL Exclude] {#exclude-block}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_exclude"
>title="Exkludera block"
>abstract="Med blocket Uteslut kan du utesluta angivna målgrupper eller attribut från din komposition."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_exclude_type"
>title="Uteslut typ"
>abstract="Du kan antingen exkludera profiler som tillhör en viss målgrupp (Exkludera efter målgrupp) eller exkludera profiler baserat på ett visst attribut (Exkludera efter attribut)."

Blocktypen **[!UICONTROL Exclude]** gör att du kan exkludera en angiven underpublik eller attribut från din nya större publik.

Om du vill lägga till ett **[!UICONTROL Exclude]**-block väljer du ikonen **+** följt av **[!UICONTROL Exclude]**.

![Alternativet Uteslut är valt.](../images/ui/audience-composition/add-exclude-block.png)

Blocket **[!UICONTROL Exclude]** har lagts till. När det här blocket är markerat visas information om undantaget i den högra listen. Detta inkluderar blockets etikett och undantagstyp. Du kan exkludera [efter målgrupp](#exclude-audience) eller [efter attribut](#exclude-attribute).

![Uteslut-blocket, som markerar de två olika exkluderingstyperna som är tillgängliga.](../images/ui/audience-composition/exclude.png)

### Exkludera efter målgrupp {#exclude-audience}

Om du exkluderar utifrån målgrupp kan du välja vilken målgrupp du vill utesluta genom att välja **[!UICONTROL Add Audience]**.

![Knappen [!UICONTROL Add audience] är markerad, vilket gör att du kan välja vilken målgrupp du vill utesluta.](../images/ui/audience-composition/add-excluded-audience.png)

>[!IMPORTANT]
>
>Endast **publicerade** målgrupper som skapats med Segment Builder kan användas. Publiker som skapats med Audience Composition och externt genererade målgrupper är **inte** tillgängliga.

En lista över målgrupper visas. Välj **[!UICONTROL Add]** om du vill lägga till målgruppen som du vill utesluta i exkluderingsblocket.

![En lista över målgrupper visas. Du kan välja vilken målgrupp du vill lägga till i den här dialogrutan.](../images/ui/audience-composition/select-audience.png)

### Exkludera efter attribut {#exclude-attribute}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_exclude_attribute"
>title="Exkludera efter attribut"
>abstract="När du exkluderar efter attribut kan du utesluta vissa profiler från att visas i kompositionen baserat på de valda attributen."

Om du utelämnar efter attribut kan du välja vilka attribut du vill utesluta genom att markera ikonen ![filter](/help/images/icons/project-edit.png) i avsnittet **[!UICONTROL Exclusion rule]**. Genom att exkludera attributet kan du utesluta profiler som innehåller det här attributet från den slutliga målgruppen.

![Attributavsnittet är markerat och visar var du ska välja vilket attribut som ska uteslutas.](../images/ui/audience-composition/exclude-attribute.png)

En lista med profilattribut visas. Välj den attributtyp som du vill exkludera, följt av **[!UICONTROL Select]**, för att lägga till dem i exkluderingsblocket.

![En lista över attribut visas.](../images/ui/audience-composition/select-attribute-exclude.png)

>[!IMPORTANT]
>
>När du exkluderar efter attribut kan du bara ange **ett**-värde som ska exkluderas. Om du använder någon form av avgränsare, som ett komma eller semikolon, utesluts bara det exakta värdet. Om du till exempel anger värdet som `red, blue` utesluts termen `red, blue` från attributet, men **inte** leder till att varken termen `red` eller `blue` utesluts.

## [!UICONTROL Enrich] {#enrich-block}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_enrich"
>title="Förstärk block"
>abstract="Med Enrich-blocket kan ni berika er målgrupp med ytterligare attribut från Adobe Experience Platform datamängder."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_dataset"
>title="Datauppsättning för berikning"
>abstract="Anrikningsdatauppsättningen innehåller de data som du vill associera med kompositionen."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_enrich_criteria"
>title="Anrikningskriterier"
>abstract="Anrikningsvillkoren innehåller Source-anslutningsnyckeln och sammanfogningsnyckeln för datauppsättningen Enrichment. Dessa två nycklar matchar källdatauppsättningen och anrikningsdatauppsättningen."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_enrich_attributes"
>title="Attribut för berikning"
>abstract="Berikeringsattributen är de attribut som du vill associera med kompositionen."

>[!IMPORTANT]
>
>Vid den här tidpunkten kan anrikningsattribut **endast** användas i Adobe Journey Optimizer-scenarier längre fram i kedjan.

Med blocktypen **[!UICONTROL Enrich]** kan du berika din målgrupp med ytterligare attribut från en datauppsättning. Du kan använda dessa attribut i användningsfall för personalisering.

Om du vill lägga till ett **[!UICONTROL Enrich]**-block väljer du ikonen **+** följt av **[!UICONTROL Enrich]**.

![Alternativet [!UICONTROL Enrich] är markerat.](../images/ui/audience-composition/add-enrich-block.png)

Blocket **[!UICONTROL Enrich]** har lagts till. När det här blocket är markerat visas information om anrikningen i den högra listen. Detta inkluderar blockets etikett och datauppsättningen för anrikning.

Om du vill välja den datauppsättning som ska berika målgruppen med väljer du ikonen ![filter](/help/images/icons/project-edit.png) .

![Filterknappen är markerad. Om du väljer det här leder det dig till [!UICONTROL Select dataset]-porten.](../images/ui/audience-composition/enrich-select-dataset.png)

**[!UICONTROL Select dataset]**-pekaren visas. Välj den datauppsättning som du vill lägga till för berikning, följt av **[!UICONTROL Select]**, för att lägga till datauppsättningen för anrikning.

![Den valda datauppsättningen har valts.](../images/ui/audience-composition/select-dataset.png)

>[!IMPORTANT]
>
>Den valda datauppsättningen **måste** uppfylla följande villkor:
>
>- Datauppsättningen **måste** vara av posttyp.
>   - Datauppsättningen **kan inte** vara av händelsetyp, systemgenereras eller markeras som Profil.
>- Datauppsättningen **måste** vara 1 GB eller mindre.

Avsnittet **[!UICONTROL Enrichment criteria]** visas nu till höger. I det här avsnittet kan du välja **[!UICONTROL Source join key]** och **[!UICONTROL Enrichment dataset join key]**, vilket gör att du kan länka anrikningsdatauppsättningen till målgruppen som du försöker skapa.

![Området [!UICONTROL Enrichment criteria] är markerat.](../images/ui/audience-composition/enrichment-criteria.png)

Om du vill markera **[!UICONTROL Source join key]** väljer du ikonen ![filter](/help/images/icons/project-edit.png) .

**[!UICONTROL Select a profile attribute]**-pekaren visas. Välj det profilattribut som du vill använda som källkopplingsnyckel, följt av **[!UICONTROL Select]**, för att välja det attributet som källkopplingsnyckel.

![Attributet som du vill använda som källanslutningsnyckel är markerat.](../images/ui/audience-composition/select-source-join-key.png)

Om du vill markera **[!UICONTROL Enrichment dataset join key]** väljer du ikonen ![filter](/help/images/icons/project-edit.png) .

**[!UICONTROL Enrichment attributes]**-pekaren visas. Välj det attribut som du vill använda som kopplingsnyckel för anrikningsdatauppsättningen, följt av **[!UICONTROL Select]**, för att välja det attributet som kopplingsnyckel för anrikningsdatauppsättningen.

![Attributet som du vill använda som kopplingsnyckel för anrikningsdatauppsättningen är markerat.](../images/ui/audience-composition/select-enrichment-dataset-join-key.png)

Nu när du har lagt till båda dina kopplingsnycklar visas avsnittet **[!UICONTROL Enrichment attributes]**. Nu kan du lägga till det attribut du vill förbättra din publik med. Om du vill lägga till dessa attribut väljer du **[!UICONTROL Add attribute]**.

**[!UICONTROL Enrichment attributes]**-pekaren visas. Du kan välja de attribut från datauppsättningen som ska berika din målgrupp med, följt av **[!UICONTROL Select]**, för att lägga till attributen till din målgrupp.

![De anrikningsattribut du vill lägga till är markerade.](../images/ui/audience-composition/select-enrichment-attribute.png)

<!-- ## [!UICONTROL Join] {#join-block}

The **[!UICONTROL Join]** block type allows you to add in external audiences from datasets that have not yet been processed by Adobe Experience Platform.

To add a **[!UICONTROL Join]** block, select the **+** icon, followed by **[!UICONTROL Join]**.

![The Join option is selected.](../images/ui/audience-composition/add-join-block.png)

When you select the block, details about the join are shown in the right rail, including the block's label and the option to add audiences to the enrichment dataset.

![The join block is highlighted, including details about the join block.](../images/ui/audience-composition/join.png)

After selecting **[!UICONTROL Add Audience]**, a list of audiences appears. Select the audiences you want to include, followed by **[!UICONTROL Add]** to add them to your join block.

![A list of audiences appears. You can select which audience you want to add from this dialog.](../images/ui/audience-composition/select-audience.png)

Your selected audiences now appear within the right rail when the **[!UICONTROL Join]** block is selected. 

![The audiences that were added as part of the Join are shown.](../images/ui/audience-composition/selected-audiences.png) -->

## [!UICONTROL Rank] {#rank-block}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_ranking"
>title="Rankningsblock"
>abstract="Med Rank-blocket kan du rangordna profiler baserat på ett specifikt attribut och inkludera dem i din komposition."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_rank_profilelimit_text"
>title="Lägg till profilgräns"
>abstract="Med alternativet Lägg till profilgräns kan du ange ett maximalt antal profiler som ska ingå i rankningsprocessen."

Blocktypen **[!UICONTROL Rank]** gör att du kan rangordna och sortera profiler baserat på ett angivet attribut och inkludera de rankade profilerna i din komposition.

Om du vill lägga till ett **[!UICONTROL Rank]**-block väljer du ikonen **+** följt av **[!UICONTROL Rank]**.

![Rankningsalternativet är markerat.](../images/ui/audience-composition/add-rank-block.png)

När du markerar blocket visas information om rangordningen i den högra listen, inklusive blockets etikett, det attribut som ska rangordnas efter, rangordningsordningen och en växling för att begränsa antalet profiler som ska rangordnas.

![Rankningsblocket är markerat, liksom informationen om rankningsblocket.](../images/ui/audience-composition/rank.png)

Välj ikonen ![filter](/help/images/icons/project-edit.png) om du vill välja vilket attribut som målgrupperna ska rangordnas efter.

![Filterikonen är markerad och visar vad du ska välja för att få åtkomst till skärmen för val av profilattribut.](../images/ui/audience-composition/select-rank-attribute.png)

En lista med profilattribut visas. I den här povern kan du välja den attributtyp som du vill rangordna målgruppen efter. Välj **[!UICONTROL Select]** om du vill lägga till den i rangblocket. Observera att det markerade attributet kan **endast** vara tal.

![En lista över attribut visas.](../images/ui/audience-composition/rank-attribute.png)

När du har valt attributet kan du välja den ordning som det ska rangordnas efter. Detta sker antingen i stigande ordning (från lägsta till högsta) eller i fallande ordning (från högsta till lägsta).

Dessutom kan du begränsa antalet profiler som returneras genom att aktivera växlingsknappen **[!UICONTROL Add profile limit]**. När den här växlingen är aktiverad kan du ange det maximala antalet profiler som returneras i fältet **[!UICONTROL Included profiles]**.

![Växeln Lägg till profilgräns är markerad, vilket gör att du kan begränsa antalet returnerade profiler.](../images/ui/audience-composition/add-profile-limit-rank.png)

## [!UICONTROL Split] {#split-block}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_split"
>title="Delat block"
>abstract="Med det delade blocket kan du dela upp kompositionen i flera banor."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_split_type"
>title="Delad text"
>abstract="Du kan dela upp kompositionen genom att dela procent eller dela attribut. Procentandel delar slumpmässigt upp profiler i flera banor. Med attributdelning kan du dela profiler baserat på ett angivet attribut."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_split_otherprofiles_text"
>title="Andra profiler"
>abstract="Med alternativet Andra profiler kan du skapa ytterligare en sökväg med de återstående profilerna som inte matchar något av de andra sökvägarnas angivna villkor."

>[!NOTE]
>
>För att du ska kunna använda **[!UICONTROL Split]**-blocket måste **måste** ha minst 10 profiler i din målgrupp.

Med blocktypen **[!UICONTROL Split]** kan du dela upp din nya målgrupp i olika undermålgrupper. Du kan antingen dela den här målgruppen baserat på procent eller ett attribut.

Om du vill lägga till ett **[!UICONTROL Split]**-block väljer du ikonen **+** följt av **[!UICONTROL Split]**.

![Alternativet Dela är markerat.](../images/ui/audience-composition/add-split-block.png)

När ni delar er målgrupp kan ni antingen dela efter procent eller dela efter attribut.

### Dela efter procent {#split-percentage}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_split_percentage"
>title="Dela efter procent"
>abstract="Ni kan slumpmässigt dela upp målgruppen i flera målgrupper baserat på antalet banor och procentandelar."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_split_persistent"
>title="Beständig delning"
>abstract="Du kan göra procentandelen beständig genom att aktivera det här alternativet och välja ett identitetsnamnutrymme."

Vid uppdelning efter procent delas målgrupperna slumpmässigt, baserat på antalet banor och procentandelar.

![Procentdelningen är markerad.](../images/ui/audience-composition/split-by-percentage.png)

Du kan också ange en identitet, vilket gör att den procentuella delningen blir bestående. Tillgängliga identitetstyper omfattar alla identitetsnamnutrymmen som är tillgängliga i din organisation.

![Kryssrutan Dela efter identitet är markerad. Dessutom är listrutan som du kan använda för att välja med identitet att dela efter markerad.](../images/ui/audience-composition/split-by-identity.png)

### Dela efter attribut {#split-attribute}

Vid uppdelning efter attribut delas målgrupperna upp utifrån de angivna attributen. Om du vill markera attributet som ska delas med markerar du **[!UICONTROL Split]**-blocket följt av ikonen ![filter](/help/images/icons/project-edit.png) .

![Filterknappen är markerad och visar hur du filtrerar efter attribut.](../images/ui/audience-composition/split-by-attribute.png)

En lista med profilattribut visas. Markera attributtypen, följt av **[!UICONTROL Select]**, för att lägga till den i det delade blocket.

![En lista över attribut visas.](../images/ui/audience-composition/select-attribute.png)

När du har valt attributet kan du välja vilka profiler som ska tillhöra vilka undermålgrupper genom att lägga till värdena i fältet **[!UICONTROL Values]**.

![De värden som du vill dela attributen med läggs till.](../images/ui/audience-composition/attribute-split-values.png)

Dessutom kan du aktivera växlingsknappen **[!UICONTROL Other profiles]** för att skapa en undermålgrupp som består av alla profiler som inte är markerade.

![Växlingsknappen Andra profiler är markerad.](../images/ui/audience-composition/split-other-profiles.png)

## Publicera era målgrupper {#publish}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_publish"
>title="Publicera"
>abstract="Du kan publicera din komposition för att skapa den eller de målgrupper som blir resultatet i Adobe Experience Platform."

>[!IMPORTANT]
>
>Observera att det kan ta upp till 48 timmar innan publikationen publiceras att utvärderas och aktiveras för användning i tjänster som Real-Time CDP eller Adobe Journey Optimizer.

När du har skapat kompositionen kan du spara och publicera den genom att välja **[!UICONTROL Publish]**.

![Knappen Publicera är markerad och visar hur du sparar och publicerar kompositionen.](../images/ui/audience-composition/publish.png)

Om det uppstår fel när målgruppen skapas visas ett varningsmeddelande som talar om hur du löser problemet.

![Knappen Publicera är markerad och visar hur du sparar och publicerar kompositionen.](../images/ui/audience-composition/audience-alert.png)

## Nästa steg

Audience Composition har ett omfattande arbetsflöde där du kan skapa kompositioner från olika blocktyper. Om du vill veta mer om andra delar av segmenteringstjänstens gränssnitt kan du läsa användarhandboken för [segmenteringstjänsten](./overview.md).
