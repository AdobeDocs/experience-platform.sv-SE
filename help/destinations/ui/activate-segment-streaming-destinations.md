---
keywords: aktivera mål för segmentströmning;aktivera mål för segmentströmning;aktivera data
title: Aktivera målgruppsdata för att direktuppspela segmentexportmål
type: Tutorial
description: Lär dig hur du aktiverar målgruppsdata i Adobe Experience Platform genom att mappa segment till mål för segmentdirektuppspelning.
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: 546758c419670746cf55de35cbb33131d4457cb9
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 0%

---

# Aktivera målgruppsdata för att direktuppspela segmentexportmål

>[!IMPORTANT]
> 
> * Aktivera data och aktivera [mappningssteg](#mapping) i arbetsflödet behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions).
> * Aktivera data utan att gå igenom [mappningssteg](#mapping) i arbetsflödet behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Segment without Mapping]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions).
> 
> Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

## Översikt {#overview}

I den här artikeln förklaras det arbetsflöde som krävs för att aktivera målgruppsdata i Adobe Experience Platform segmentdirektuppspelningsmål.

## Förutsättningar {#prerequisites}

Du måste ha aktiverat data till destinationer [ansluten till ett mål](./connect-destination.md). Om du inte redan har gjort det går du till [målkatalog](../catalog/overview.md), bläddra bland de mål som stöds och konfigurera det mål som du vill använda.

## Välj mål {#select-destination}

1. Gå till **[!UICONTROL Connections > Destinations]** och väljer **[!UICONTROL Catalog]** -fliken.

   ![Fliken Målkatalog](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Välj **[!UICONTROL Activate segments]** på kortet som motsvarar destinationen där du vill aktivera dina segment, vilket visas i bilden nedan.

   ![Aktivera knappar](../assets/ui/activate-segment-streaming-destinations/activate-segments-button.png)

1. Markera målanslutningen som du vill använda för att aktivera dina segment och välj sedan **[!UICONTROL Next]**.

   ![Välj mål](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. Gå till nästa avsnitt till [markera segment](#select-segments).

## Välj segment {#select-segments}

Använd kryssrutorna till vänster om segmentnamnen för att markera de segment som du vill aktivera för målet och markera sedan **[!UICONTROL Next]**.

![Markera segment](../assets/ui/activate-segment-streaming-destinations/select-segments.png)

## Mappa attribut och identiteter {#mapping}

>[!IMPORTANT]
>
>Det här steget gäller endast vissa mål för segmentdirektuppspelning. Om målet inte har en **[!UICONTROL Mapping]** steg, hoppa till [Schemalägg segmentexport](#scheduling).

Vissa mål för segmentdirektuppspelning kräver att du väljer källattribut eller identitetsnamnutrymmen som ska mappas som målidentiteter i målet.

1. I **[!UICONTROL Mapping]** sida, markera **[!UICONTROL Add new mapping]**.

   ![Lägg till ny mappning](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. Markera pilen till höger om **[!UICONTROL Source field]** post.

   ![Välj källfält](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. I **[!UICONTROL Select source field]** sidan använder du **[!UICONTROL Select attributes]** eller **[!UICONTROL Select identity namespace]** för att växla mellan de två kategorierna med tillgängliga källfält. Från tillgängliga [!DNL XDM] profilattribut och identitetsnamnutrymmen, markera de som du vill mappa till målet och välj sedan **[!UICONTROL Select]**.

   ![Välj källfältssida](../assets/ui/activate-segment-streaming-destinations/source-field-page.png)

1. Markera knappen till höger om **[!UICONTROL Target field]** post.

   ![Välj målfält](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. I **[!UICONTROL Select target field]** väljer du det målidentitetsnamnutrymme som du vill mappa källfältet till och väljer **[!UICONTROL Select]**.

   ![Välj målfältssida](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. Om du vill lägga till fler mappningar upprepar du steg 1 till 5.

### Använd omformning {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Använd omformning"
>abstract="Markera det här alternativet om du vill att Adobe Experience Platform automatiskt ska hash-koda dem vid aktiveringen när du använder ohashed-källfält."

När du mappar ohashade källattribut till målattribut som målet förväntar sig ska hash-kodas (till exempel: `email_lc_sha256` eller `phone_sha256`), kontrollera **Använd omformning** att Adobe Experience Platform automatiskt ska hash-koda källattributen vid aktiveringen.

![Identitetsmappning](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Schemalägg segmentexport {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_enddate"
>title="Slutdatum"
>abstract="Det går inte att lägga till ett slutdatum för segmentschema."

Som standard är [!UICONTROL Segment schedule] visas endast de nyligen valda segmenten som du valde i det aktuella aktiveringsflödet.

![Nya segment](../assets/ui/activate-segment-streaming-destinations/new-segments.png)

Om du vill se alla segment som aktiveras till målet använder du filteralternativet och inaktiverar **[!UICONTROL Show new segments only]** filter.

![Alla segment](../assets/ui/activate-segment-streaming-destinations/all-segments.png)

1. På **[!UICONTROL Segment schedule]** markerar du varje segment och använder sedan **[!UICONTROL Start date]** och **[!UICONTROL End date]** väljare för att konfigurera tidsintervallet för att skicka data till målet.

   ![Segmentschema](../assets/ui/activate-segment-streaming-destinations/segment-schedule.png)

   * Vissa mål kräver att du väljer **[!UICONTROL Origin of audience]** för varje segment med hjälp av listrutan under kalenderväljarna. Om målet inte innehåller den här väljaren hoppar du över det här steget.

      ![Mappnings-ID](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * Vissa mål kräver att du mappar manuellt [!DNL Platform] segment till deras motsvarighet i måldestinationen. Om du vill göra det markerar du varje segment och anger sedan motsvarande segment-ID från målplattformen i dialogrutan **[!UICONTROL Mapping ID]** fält. Om målet inte innehåller det här fältet hoppar du över det här steget.

      ![Mappnings-ID](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * Vissa mål kräver att du anger en **[!UICONTROL App ID]** vid aktivering [!DNL IDFA] eller [!DNL GAID] segment. Om målet inte innehåller det här fältet hoppar du över det här steget.

      ![Program-ID](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. Välj **[!UICONTROL Next]** för att gå till [!UICONTROL Review] sida.

## Granska {#review}

På **[!UICONTROL Review]** kan du se en sammanfattning av markeringen. Välj **[!UICONTROL Cancel]** för att bryta upp flödet, **[!UICONTROL Back]** för att ändra dina inställningar, eller **[!UICONTROL Finish]** för att bekräfta ditt val och börja skicka data till målet.

![Markeringssammanfattning i granskningssteget.](/help/destinations/assets/ui/activate-segment-streaming-destinations/review.png)

### Principutvärdering av samtycke {#consent-policy-evaluation}

Om din organisation har köpt **Adobe Healthcare Shield** eller **Adobe Privacy &amp; Security Shield**, markera **[!UICONTROL View applicable consent policies]** för att se vilka regler för samtycke som tillämpas och hur många profiler som inkluderas i aktiveringen till följd av dessa. Läs om [utvärdering av godkännandepolicy](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) för mer information.

### Kontroller av policyer för dataanvändning {#data-usage-policy-checks}

I **[!UICONTROL Review]** Experience Platform kontrollerar också om dataanvändningspolicyn har överträtts. Nedan visas ett exempel där en princip överträds. Du kan inte slutföra arbetsflödet för segmentaktivering förrän du har löst konflikten. Mer information om hur du löser policyöverträdelser finns i [brott mot dataanvändningsprinciper](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) i dokumentationsavsnittet för datastyrning.

![dataprincipöverträdelse](../assets/common/data-policy-violation.png)

### Filtrera segment {#filter-segments}

I det här steget kan du även använda de tillgängliga filtren på sidan för att endast visa segment vars schema eller mappning har uppdaterats som en del av det här arbetsflödet. Du kan också växla vilka tabellkolumner som du vill se.

![Skärminspelning som visar tillgängliga segmentfilter i granskningssteget.](/help/destinations/assets/ui/activate-segment-streaming-destinations/filter-segments-review-step.gif)

Om du är nöjd med ditt val och inga policyöverträdelser har identifierats väljer du **[!UICONTROL Finish]** för att bekräfta ditt val och börja skicka data till målet.

## Verifiera segmentaktivering {#verify}

Kontrollera [dokumentation för målövervakning](../../dataflows/ui/monitor-destinations.md) om du vill ha detaljerad information om hur du övervakar dataflödet till dina destinationer.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segment membership in the audience would be added and removed as users are qualified or disqualified for the activated segments.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical segment qualifications are sent to [!DNL Facebook] when you activate the segments to the destination.
-->
