---
keywords: Experience Platform;hem;populära ämnen;Segmenteringstjänst;segmenteringstjänst;segmenteringstjänst;användarguide;ui guide;målgrupper ui guide;målgruppsbyggare;målgrupper;målgrupper ui guide;
solution: Experience Platform
title: Användargränssnittshandbok för målgrupper
description: Audience Builder i Adobe Experience Platform UI har en omfattande arbetsyta som du kan använda för att interagera med profildataelement. Arbetsytan innehåller intuitiva kontroller för att skapa och redigera målgrupper för din organisation.
hide: true
hidefromtoc: true
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# Användargränssnittshandbok för Audience Builder

>[!IMPORTANT]
>
>Audience Builder är för närvarande i betaversion och är inte tillgängligt för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

I Audience Builder finns en arbetsyta där du kan skapa och redigera målgrupper med hjälp av block som används för att representera olika åtgärder.

![Användargränssnittet i Audience Builder.](../images/ui/audience-builder/audience-builder.png)

Målgruppens arbetsyta består av fem olika typer av block: **[[!UICONTROL Audience]](#audience-block)**, **[[!UICONTROL Exclude]](#exclude-block)**, **[[!UICONTROL Join]](#join-block)**, **[[!UICONTROL Rank]](#rank-block)** och **[[!UICONTROL Split]](#split-block)**.

## [!UICONTROL Audience] {#audience-block}

The **[!UICONTROL Audience]** Med blocktyp kan ni lägga till de undermålgrupper som ni vill skapa en ny större publik. Som standard är **[!UICONTROL Audience]** -blocket inkluderas högst upp på kompositionens arbetsyta.

När du väljer **[!UICONTROL Audience]** höger räl visar kontroller för etikettering och tillägg av målgrupper i blocket.

![Information om målgruppsblock visas.](../images/ui/audience-builder/select-audience.png)

Efter markering **[!UICONTROL Add Audience]** visas en lista med målgrupper. Välj vilka målgrupper du vill inkludera, följt av **[!UICONTROL Add]** för att lägga in dem i era målgruppsblock.

![En lista över målgrupper visas. Du kan välja vilken målgrupp du vill lägga till i den här dialogrutan.](../images/ui/audience-builder/select-audience.png)

De valda målgrupperna visas nu i rätt spår när **[!UICONTROL Audience]** -block är markerat. Härifrån kan du ändra sammanfogningstypen för de kombinerade målgrupperna.

![Möjliga sammanfogningstyper för målgrupper markeras.](../images/ui/audience-builder/merge-types.png)

| Sammanfoga typ | Beskrivning |
| ---------- | ----------- |
| [!UICONTROL Union] | Målgrupperna samlas i en och samma målgrupp. Detta motsvarar en OR-åtgärd. |
| [!UICONTROL Intersection] | Målgrupperna kombineras med endast de målgrupper som delas i **alla** av dem som läggs till. Detta motsvarar en AND-åtgärd. |
| [!UICONTROL Exclude overlap] | Målgrupperna kombineras med endast de målgrupper som delas i **en, men inte alla** av dem som läggs till. Detta motsvarar en XOR-åtgärd. |

## [!UICONTROL Exclude] {#exclude-block}

The **[!UICONTROL Exclude]** Med blocktyp kan du utesluta angivna undergrupper eller attribut från din nya större publik.

Lägga till en **[!UICONTROL Exclude]** markerar du **+** ikon, följt av **[!UICONTROL Exclude]**.

![Alternativet Uteslut är valt.](../images/ui/audience-builder/add-exclude-block.png)

The **[!UICONTROL Exclude]** -block läggs till. När det här blocket är markerat visas information om undantaget i den högra listen. Detta inkluderar blockets etikett och undantagstyp. Du kan utesluta [per målgrupp](#exclude-audience) eller [efter attribut](#exclude-attribute).

![Uteslut-blocket, som markerar de två olika exkluderingstyperna som är tillgängliga.](../images/ui/audience-builder/exclude.png)

### Exkludera efter målgrupp {#exclude-audience}

Om du utesluter utifrån målgrupp kan du välja vilka målgrupper du vill utesluta genom att välja **[!UICONTROL Add Audience]**.

![Knappen Lägg till målgrupp är markerad, med vilken du kan välja vilken målgrupp du vill utesluta.](../images/ui/audience-builder/add-excluded-audience.png)

En lista över målgrupper visas. Välj **[!UICONTROL Add]** för att lägga till de målgrupper du vill utesluta i exkluderingsblocket.

![En lista över målgrupper visas. Du kan välja vilken målgrupp du vill lägga till i den här dialogrutan.](../images/ui/audience-builder/select-audience.png)

### Exkludera efter attribut {#exclude-attribute}

Om du utelämnar efter attribut kan du välja vilka attribut du vill utesluta genom att välja ![filter](../images/ui/audience-builder/filter-attribute.png) -ikonen i **[!UICONTROL Exclusion rule]** -avsnitt.

![Attributavsnittet är markerat och visar var du ska välja vilket attribut som ska uteslutas.](../images/ui/audience-builder/exclude-attribute.png)

En lista med profilattribut visas. Välj den attributtyp som du vill exkludera, följt av **[!UICONTROL Select]** för att lägga till dem i exkluderingsblocket.

![En lista med attribut visas.](../images/ui/audience-builder/select-attribute.png)

## [!UICONTROL Join] {#join-block}

The **[!UICONTROL Join]** blocktyp gör att du kan lägga till externa målgrupper från datauppsättningar som ännu inte har bearbetats av Adobe Experience Platform.

Lägga till en **[!UICONTROL Join]** markerar du **+** ikon, följt av **[!UICONTROL Join]**.

![Alternativet Förena är valt.](../images/ui/audience-builder/add-join-block.png)

När du markerar blocket visas information om kopplingen i den högra listen, inklusive blockets etikett och möjligheten att lägga till målgrupper i datauppsättningen för anrikning.

![Kopplingsblocket markeras, inklusive information om kopplingsblocket.](../images/ui/audience-builder/join.png)

Efter markering **[!UICONTROL Add Audience]** visas en lista med målgrupper. Välj vilka målgrupper du vill inkludera, följt av **[!UICONTROL Add]** för att lägga till dem i ditt kopplingsblock.

![En lista över målgrupper visas. Du kan välja vilken målgrupp du vill lägga till i den här dialogrutan.](../images/ui/audience-builder/select-audience.png)

De valda målgrupperna visas nu i rätt spår när **[!UICONTROL Join]** -block är markerat.

![De målgrupper som lades till som en del av Förena visas.](../images/ui/audience-builder/selected-audiences.png)

## [!UICONTROL Rank] {#rank-block}

The **[!UICONTROL Rank]** Med blocktyp kan ni rangordna och sortera målgrupperna innan den nya målgruppen publiceras.

Lägga till en **[!UICONTROL Rank]** markerar du **+** ikon, följt av **[!UICONTROL Rank]**.

![Alternativet Rankning är valt.](../images/ui/audience-builder/add-rank-block.png)

När du markerar blocket visas information om rangordningen i den högra listen, inklusive blockets etikett, det attribut som ska rangordnas efter, rangordningsordningen och en växling för att begränsa antalet profiler som ska rangordnas.

![Rankningsblocket markeras, liksom detaljerna om rangblocket.](../images/ui/audience-builder/rank.png)

Om du vill välja vilket attribut som målgrupperna ska rangordnas efter väljer du ![filter](../images/ui/audience-builder/filter-attribute.png) ikon.

![Filterikonen är markerad och visar vad du ska välja för att komma åt skärmen för val av profilattribut.](../images/ui/audience-builder/select-rank-attribute.png)

En lista med profilattribut visas. I den här povern kan du välja den attributtyp som du vill rangordna målgruppen efter. Välj **[!UICONTROL Select]** för att lägga till den i ditt rangblock. Observera att det valda attributet kan **endast** vara av typen `int`.

![En lista med attribut visas.](../images/ui/audience-builder/select-attribute.png)

När du har valt attributet kan du välja den ordning som det ska rangordnas efter. Detta sker antingen i stigande ordning (från lägsta till högsta) eller i fallande ordning (från högsta till lägsta).

Dessutom kan du begränsa antalet returnerade målgrupper genom att aktivera **[!UICONTROL Add profile limit]** växla. När den här växeln är aktiverad kan du ange det maximala antalet målgrupper som returneras inom **[!UICONTROL Included profiles]** fält.

![Alternativet Lägg till profilgräns är markerat, vilket gör att du kan begränsa antalet returnerade målgrupper.](../images/ui/audience-builder/add-profile-limit.png)

## [!UICONTROL Split] {#split-block}

The **[!UICONTROL Split]** blocktyp gör att ni kan dela upp er nya målgrupp i olika undergrupper. Du kan antingen dela den här målgruppen baserat på procent eller ett attribut.

Lägga till en **[!UICONTROL Split]** markerar du **+** ikon, följt av **[!UICONTROL Split]**.

![Alternativet Dela är markerat.](../images/ui/audience-builder/add-split-block.png)

### Dela efter procent {#split-percentage}

Vid uppdelning efter procent delas målgrupperna slumpmässigt, baserat på antalet banor och procentandelar.

Du kan t.ex. ha tre banor med olika procentandelar av profiler.

![Uppdelningen av antal sparade målgrupper och procentandelar visas.](../images/ui/audience-builder/percentages.png)

Dessutom kan du markera en av de delade målgrupperna som kontrollgrupp.

![Kontrollgruppens växlingsknapp är aktiverad. På så sätt kan du markera en av de delade målgrupperna som en kontrollgrupp.](../images/ui/audience-builder/control-group.png)

### Dela efter attribut {#split-attribute}

Vid uppdelning efter attribut delas målgrupperna upp utifrån de angivna attributen. Markera attributet som ska delas med **[!UICONTROL Split]** -block, följt av ![filter](../images/ui/audience-builder/filter-attribute.png) ikon.

![Filterknappen är markerad och visar hur du filtrerar efter attribut.](../images/ui/audience-builder/select-attribute-split.png)

En lista med profilattribut visas. Välj attributtyp, följt av **[!UICONTROL Select]** för att lägga till den i det delade blocket.

![En lista med attribut visas.](../images/ui/audience-builder/select-attribute.png)

När du har valt attributet kan du välja vilka profiler som ska tillhöra vilka undermålgrupper genom att lägga till värdena i **[!UICONTROL Values]** fält.

![De värden som du vill dela attributen med läggs till.](../images/ui/audience-builder/attribute-split-values.png)

Dessutom kan du aktivera **[!UICONTROL Other profiles]** för att skapa en undermålgrupp som består av alla profiler som inte är markerade.

![Alternativet Andra profiler är markerat.](../images/ui/audience-builder/attribute-split-other-profiles.png)

## Publicera era målgrupper

När ni har komponerat målgruppen kan ni spara och publicera den genom att välja **[!UICONTROL Publish]**.

![Knappen Publicera är markerad och visar hur du sparar och publicerar din publik.](../images/ui/audience-builder/publish-audience.png)

Om det uppstår fel när målgruppen skapas visas ett varningsmeddelande som talar om hur du löser problemet.

![Knappen Publicera är markerad och visar hur du sparar och publicerar din publik.](../images/ui/audience-builder/audience-alert.png)

## Nästa steg

Audience Builder har ett omfattande arbetsflöde där du kan skapa målgrupper från olika blocktyper. Läs mer om andra delar av segmenteringstjänstens gränssnitt i [Användarhandbok för segmenteringstjänsten](./overview.md).
