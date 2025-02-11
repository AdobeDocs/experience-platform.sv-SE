---
title: Publiceringsflöde
description: Lär dig hur du skapar bibliotek, testar byggen och godkänner dem för produktion i Adobe Experience Platform.
exl-id: 4885f60b-6401-4ec7-aa1a-29c135087847
source-git-commit: 2d71eafb00098d958c8cff9350caa27bd3f0260d
workflow-type: tm+mt
source-wordcount: '1407'
ht-degree: 3%

---

# Publiceringsflöde {#publishing-flow}

>[!CONTEXTUALHELP]
>id="platform_tags_publishing_flow"
>title="Publiceringsflöde"
>abstract="Förstå nivåerna på de användarbehörigheter som krävs för publiceringsflödet, inklusive Utveckla, Godkänn och Publicera."

>[!NOTE]
>
>Adobe Experience Platform Launch har omprofilerats till en serie tekniker för datainsamling i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar genomförts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens av terminologiändringarna.

Taggpubliceringsflödet i Adobe Experience Platform avser processen att skapa bibliotek, testa byggen och godkänna dem för produktion.

Vilka åtgärder du kan utföra i ett bibliotek beror på bibliotekets tillstånd och vilken behörighetsnivå du har. Dessutom påverkar ett biblioteks tillstånd även de resurser som det innehåller (regler, dataelement och tillägg) beroende på vad som är uppströms i publiceringsflödet.

Avsnitten nedan innehåller information om behörigheter, bibliotekstillstånd och det överordnade flödet när det gäller publiceringsflödet.

## Behörigheter {#permissions}

Det finns olika nivåer av användarbehörigheter som är viktiga för publiceringsflödet, särskilt egenskapsrättigheterna [!UICONTROL Develop], [!UICONTROL Approve] och [!UICONTROL Publish]:

* **[!UICONTROL Develop]**: Innehåller möjlighet att skapa bibliotek, bygga för utveckling och skicka för godkännande.
* **[!UICONTROL Approve]**: Inkluderar möjligheten att skapa för mellanlagring och godkänna mellanlagrade byggen.
* **[!UICONTROL Publish]**: Inkluderar möjligheten att publicera ett godkänt bibliotek.

Dessa rättigheter är inte inkluderande. För att en person ska kunna utföra arbetsflödet från början till slut måste den personen beviljas alla tre rättigheterna inom en viss egenskap.

Mer information om hur du hanterar behörigheter för taggar finns i [användarbehörighetshandboken](../administration/user-permissions.md).

## Biblioteksläge {#state}

När det gäller publiceringsflödet finns det fyra grundläggande lägen för ett bibliotek:

* [[!UICONTROL Development]](#development)
* [[!UICONTROL Submitted]](#submitted)
* [[!UICONTROL Approved]](#approved)
* [[!UICONTROL Published]](#published)

Dessa fyra lägen representeras som kolumner på fliken **[!UICONTROL Publishing Flow]**.

![](./images/approval-workflow/flow-ui.png)

Specifika åtgärder måste vidtas för att flytta ett bibliotek mellan dessa lägen. I följande diagram visas varje åtgärd som flyttar ett bibliotek mellan lägen:

![](./images/approval-workflow/library-state.png)

### [!UICONTROL Development] {#development}

När nya bibliotek skapas börjar de i läget [!UICONTROL Development]. Alla ändringar i ett bibliotek måste göras medan biblioteket finns i [!UICONTROL Development]. När utveckling och testning är slutförda kan biblioteket skickas för godkännande.

I följande tabell visas de tillgängliga åtgärderna för ett bibliotek i läget [!UICONTROL Development]:

| Åtgärd | Beskrivning |
| --- | --- |
| [!UICONTROL Edit] | Använd skärmen [!UICONTROL Edit Library] för att lägga till eller ta bort komponenter från biblioteket. |
| [!UICONTROL Build to Development] | Skapa ett bygge för biblioteket. Bygget kompileras och distribueras till den miljö som biblioteket är tilldelat. Det här steget misslyckas om biblioteket inte har tilldelats en miljö eller innehåller en ändring som redan har definierats i det överordnade flödet. |
| [!UICONTROL Submit for Approval] | Ta bort tilldelningen av biblioteket från utvecklingsmiljön och flytta biblioteket till kolumnen [!UICONTROL Submitted] för en användare med godkännandebehörighet att arbeta med. Den senaste versionen av biblioteket måste slutföras för att det här alternativet ska kunna aktiveras. |
| [!UICONTROL Submit & Build to Staging] | Detta kan bara utföras av en användare med både utvecklings- och godkännanderättigheter. Den här åtgärden tar bort tilldelningen av biblioteket från utvecklingsmiljön, flyttar biblioteket till tillståndet [!UICONTROL Submitted] och skapar biblioteket till mellanlagringsmiljön. Den senaste versionen av biblioteket måste slutföras för att det här alternativet ska kunna aktiveras. |
| [!UICONTROL Approve for Publishing] | Detta kan bara utföras av en användare med både utvecklings- och godkännanderättigheter. Den här åtgärden tar bort tilldelningen av biblioteket från utvecklingsmiljön och flyttar det till läget [!UICONTROL Approved], vilket innebär att mellanlagringsmiljön och läget [!UICONTROL Submitted] hoppas över helt. Den senaste versionen av biblioteket måste slutföras för att det här alternativet ska kunna aktiveras. |
| [!UICONTROL Approve & Publish to Production] | Detta kan bara utföras av en användare med behörigheterna Framkalla, Godkänn och Publicera. Den här åtgärden frigör biblioteket från utvecklingsmiljön, flyttar det till tillståndet [!UICONTROL Approved] och publicerar det i produktion. När produktionsbygget har slutförts flyttas biblioteket till tillståndet [!UICONTROL Published]. Den senaste versionen av biblioteket måste slutföras för att det här alternativet ska kunna aktiveras. |
| [!UICONTROL Delete] | Ta bort biblioteket från systemet. Detta tar inte bort bygget från miljön. |

### [!UICONTROL Submitted] {#submitted}

När ett bibliotek är i läget [!UICONTROL Submitted] kan en användare med godkännandebehörighet testa biblioteket i mellanlagringsmiljön. När testningen är klar kan biblioteket godkännas eller avvisas. Avvisade byggen återgår till [!UICONTROL Development] så att ytterligare ändringar kan göras innan publiceringsflödet startas om.

I följande tabell visas de tillgängliga åtgärderna för ett bibliotek i läget [!UICONTROL Submitted]:

| Åtgärd | Beskrivning |
| --- | --- |
| [!UICONTROL Open] | Visa innehållet i biblioteket. Ändringar tillåts inte för bibliotek utanför kolumnen [!UICONTROL Development]. Om ändringar behövs bör biblioteket avvisas så ändringar kan göras i [!UICONTROL Development]. |
| [!UICONTROL Build for Staging] | Bygg biblioteket i testmiljön för distribution. |
| [!UICONTROL Approve for Publishing] | Flytta biblioteket till kolumnen [!UICONTROL Approved] för en användare med publiceringsbehörigheter att arbeta med. |
| [!UICONTROL Approve & Publish to Production] | Detta kan bara utföras av en användare med både behörigheten Godkänn och Publicera. Den här åtgärden frigör biblioteket från mellanlagringsmiljön, flyttar det till tillståndet [!UICONTROL Approved] och publicerar det i produktion. När produktionsbygget har slutförts flyttas biblioteket till tillståndet [!UICONTROL Published]. Detta kan utföras med vår utan att du lyckas bygga i staging-miljön. |
| [!UICONTROL Reject] | Ta bort tilldelningen av biblioteket från mellanlagringsmiljön och flytta biblioteket tillbaka till kolumnen [!UICONTROL Development] för ytterligare ändringar. |

### [!UICONTROL Approved] {#approved}

När ett bibliotek har godkänts kan en användare med publiceringsbehörighet publicera eller avvisa biblioteket. Avvisade byggen återgår till [!UICONTROL Development] så att fler ändringar kan göras innan publiceringsflödet börjar igen.

I följande tabell visas de tillgängliga åtgärderna för ett bibliotek i läget [!UICONTROL Approved]:

| Åtgärd | Beskrivning |
| --- | --- |
| [!UICONTROL Open] | Visa innehållet i biblioteket. Ändringar tillåts inte för bibliotek utanför kolumnen [!UICONTROL Development]. Om ändringar behövs bör biblioteket avvisas så ändringar kan göras i [!UICONTROL Development]. |
| [!UICONTROL Build and Publish to Production] | Ta bort tilldelningen av biblioteket från mellanlagringsmiljön, tilldela biblioteket till produktionsmiljön och distribuera det.<br><br>**Viktigt**: När det här alternativet väljs blir ditt bibliotek levande i din produktionsmiljö. Kontrollera att biblioteket innehåller de ändringar du vill ha innan du väljer det här alternativet. |
| [!UICONTROL Reject] | Ta bort tilldelningen av biblioteket från mellanlagringsmiljön och flytta biblioteket till kolumnen [!UICONTROL Development] för ytterligare ändringar. |

### [!UICONTROL Published] {#published}

Kolumnen [!UICONTROL Published] visar vilka bibliotek som har publicerats och deras publiceringsdatum. Det publicerade biblioteket visas med en grön punkt bredvid sig. Om du inte har publicerat om ett tidigare bibliotek visas alltid biblioteket överst i kolumnen.

| Åtgärd | Beskrivning |
| --- | --- |
| [!UICONTROL Open] | Visa innehållet i biblioteket. Ändringar tillåts inte för bibliotek utanför kolumnen [!UICONTROL Development]. Om du vill ändra vad som finns i produktionsmiljön måste du skapa ett nytt bibliotek och flytta det genom hela publiceringsprocessen. |
| [!UICONTROL Republish] | Den här åtgärden är bara tillgänglig i de fem senast publicerade biblioteken och endast om produktionsmiljön (A) har konfigurerats med alternativet Arkiv inaktiverat och (b) använder en [!UICONTROL Managed by Adobe]-värd vid tidpunkten för bygget. |
| [!UICONTROL Download] | Den här åtgärden är bara tillgänglig i de fem senast publicerade biblioteken och endast om produktionsmiljön (A) har konfigurerats med alternativet Arkiv på och (b) använder en [!UICONTROL Managed by Adobe]-värd vid tidpunkten för bygget. |

## Uppströms {#upstream}

När du har publicerat ditt första bibliotek blir det viktigt att förstå den överordnade strömmens roll när du flyttar nyare bibliotek genom publiceringsflödet.

Om ett bibliotek finns på [!UICONTROL Development]-, [!UICONTROL Submitted]- eller [!UICONTROL Approved]-scenen ärver biblioteket reglerna, dataelementen och tilläggen för alla bibliotek som är överordnade. Dessa ärvda resurser utgör en&quot;baslinje&quot; för varje bibliotek när de rör sig genom publiceringsflödet. I grund och botten kan du tänka på varje nytt bibliotek som en serie ändringar av baslinjen som upprättas av det överordnade biblioteket. Detta garanterar att inget oväntat skrivs över från ett tidigare bibliotek när en ny upprepning publiceras.

Vad som ingår i det överordnade flödet beror på bibliotekets aktuella stadium. Bibliotek i kolumnen [!UICONTROL Approved] ärver till exempel bara resurser från biblioteket [!UICONTROL Published], medan bibliotek under [!UICONTROL Development] ärver resurser från alla andra kolumner.

![](./images/approval-workflow/upstream.png)

När du redigerar ett bibliotek i användargränssnittet visas alla resurser som ärvs från det överordnade objektet i avsnittet **[!UICONTROL Resources Upstream]**. Om du vill visa resurserna väljer du fliken Expandera under avsnittsrubriken.

![](./images/approval-workflow/upstream-collapse.png)

Avsnittet expanderas och visar de enskilda resurser som ärvs från det överordnade flödet. Du kan använda den vänstra listen för att filtrera mellan [!UICONTROL Rules], [!UICONTROL Data Elements] och [!UICONTROL Extensions], eller använda sökfältet för att söka efter en specifik resurs efter namn.

![](./images/approval-workflow/upstream-resources.png)

## Nästa steg

Den här guiden ger en översikt över publiceringsflödet för bibliotek i Adobe Experience Platform. Mer information om hur du publicerar dina bibliotek finns i [publiceringsöversikten](./overview.md).
