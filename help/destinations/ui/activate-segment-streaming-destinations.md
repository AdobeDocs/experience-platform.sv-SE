---
keywords: aktivera mål för segmentströmning;aktivera mål för segmentströmning;aktivera data
title: Aktivera målgruppsdata för att direktuppspela segmentexportmål
type: Tutorial
seo-title: Activate audience data to streaming segment export destinations
description: Lär dig hur du aktiverar målgruppsdata i Adobe Experience Platform genom att mappa segment till mål för segmentdirektuppspelning.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by mapping segments to segment streaming destinations.
source-git-commit: f4721d3f114357b25517e4e66f1f626f82621c34
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---


# Aktivera målgruppsdata för att direktuppspela segmentexportmål

## Översikt {#overview}

I den här artikeln förklaras det arbetsflöde som krävs för att aktivera målgruppsdata i Adobe Experience Platform segmentdirektuppspelningsmål.

## Förutsättningar {#prerequisites}

Om du vill aktivera data till mål måste du ha [anslutit till ett mål](./connect-destination.md). Om du inte redan har gjort det går du till [målkatalogen](../catalog/overview.md), bläddrar bland de mål som stöds och konfigurerar det mål som du vill använda.

## Välj mål {#select-destination}

1. Gå till **[!UICONTROL Connections > Destinations]** och välj fliken **[!UICONTROL Catalog]**.

   ![Fliken Målkatalog](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Välj **[!UICONTROL Activate segments]** på kortet som motsvarar målet där du vill aktivera dina segment, vilket visas i bilden nedan.

   ![Aktivera knappar](../assets/ui/activate-segment-streaming-destinations/activate-segments-button.png)

1. Markera målanslutningen som du vill använda för att aktivera dina segment och välj sedan **[!UICONTROL Next]**.

   ![Välj mål](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. Gå till nästa avsnitt för att [markera dina segment](#select-segments).

## Välj segment {#select-segments}

Använd kryssrutorna till vänster om segmentnamnen för att markera de segment som du vill aktivera för målet och välj sedan **[!UICONTROL Next]**.

![Markera segment](../assets/ui/activate-segment-streaming-destinations/select-segments.png)

## Mappa attribut och identiteter {#mapping}

>[!IMPORTANT]
>
>Det här steget gäller endast vissa mål för segmentdirektuppspelning. Om målet inte har ett **[!UICONTROL Mapping]**-steg går du till [Schemalägg segmentexport](#scheduling).

Vissa mål för segmentdirektuppspelning kräver att du väljer källattribut eller identitetsnamnutrymmen som ska mappas som målidentiteter i målet.

1. Välj **[!UICONTROL Add new mapping]** på sidan **[!UICONTROL Mapping]**.

   ![Lägg till ny mappning](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. Markera pilen till höger om **[!UICONTROL Source field]**-posten.

   ![Välj källfält](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. På sidan **[!UICONTROL Select source field]** använder du alternativen **[!UICONTROL Select attributes]** eller **[!UICONTROL Select identity namespace]** för att växla mellan de två kategorierna med tillgängliga källfält. Välj de tillgängliga [!DNL XDM]-profilattributen och identitetsnamnutrymmena de som du vill mappa till målet och välj sedan **[!UICONTROL Select]**.

   ![Välj källfältssida](../assets/ui/activate-segment-streaming-destinations/source-field-page.png)

1. Markera knappen till höger om **[!UICONTROL Target field]**-posten.

   ![Välj målfält](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. På sidan **[!UICONTROL Select target field]** markerar du det målidentitetsnamnområde som du vill mappa källfältet till och väljer **[!UICONTROL Select]**.

   ![Välj målfältssida](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. Om du vill lägga till fler mappningar upprepar du steg 1 till 5.

### Använd omformning {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Använd omformning"
>abstract="Markera det här alternativet om du vill att Adobe Experience Platform automatiskt ska hash-koda dem vid aktiveringen när du använder ohashed-källfält."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#apply-transformation" text="Läs mer i dokumentationen"

När du mappar ohashade källattribut till målattribut som målet förväntar sig ska hash-kodas (till exempel: `email_lc_sha256` eller `phone_sha256`), markera alternativet **Använd omformning** om du vill att Adobe Experience Platform automatiskt ska hash-koda källattributen vid aktiveringen.

![Identitetsmappning](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Schemalägg segmentexport {#scheduling}

Som standard visar sidan [!UICONTROL Segment schedule] bara de segment som du nyligen har valt i det aktuella aktiveringsflödet.

![Nya segment](../assets/ui/activate-segment-streaming-destinations/new-segments.png)

Om du vill se alla segment som aktiveras till målet använder du filteralternativet och inaktiverar filtret **[!UICONTROL Show new segments only]**.

![Alla segment](../assets/ui/activate-segment-streaming-destinations/all-segments.png)

1. På sidan **[!UICONTROL Segment schedule]** markerar du varje segment och använder sedan väljarna **[!UICONTROL Start date]** och **[!UICONTROL End date]** för att konfigurera tidsintervallet för att skicka data till målet.

   ![Segmentschema](../assets/ui/activate-segment-streaming-destinations/segment-schedule.png)

   * Vissa mål kräver att du väljer **[!UICONTROL Origin of audience]** för varje segment med hjälp av den nedrullningsbara menyn under kalenderväljarna. Om målet inte innehåller den här väljaren hoppar du över det här steget.

      ![Mappnings-ID](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * Vissa mål kräver att du manuellt mappar [!DNL Platform]-segment till deras motsvarighet i måldestinationen. Det gör du genom att markera varje segment och sedan ange motsvarande segment-ID från målplattformen i fältet **[!UICONTROL Mapping ID]**. Om målet inte innehåller det här fältet hoppar du över det här steget.

      ![Mappnings-ID](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * Vissa mål kräver att du anger ett **[!UICONTROL App ID]** när du aktiverar [!DNL IDFA]- eller [!DNL GAID]-segment. Om målet inte innehåller det här fältet hoppar du över det här steget.

      ![Program-ID](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. Välj **[!UICONTROL Next]** om du vill gå till sidan [!UICONTROL Review].

## Granska {#review}

På sidan **[!UICONTROL Review]** visas en sammanfattning av ditt val. Välj **[!UICONTROL Cancel]** om du vill dela upp flödet, **[!UICONTROL Back]** om du vill ändra inställningarna eller **[!UICONTROL Finish]** om du vill bekräfta valet och börja skicka data till målet.

>[!IMPORTANT]
>
>I det här steget söker Adobe Experience Platform efter brott mot dataanvändningspolicyn. Nedan visas ett exempel där en princip överträds. Du kan inte slutföra arbetsflödet för segmentaktivering förrän du har löst konflikten. Mer information om hur du löser policyöverträdelser finns i [Politiska åtgärder](../../rtcdp/privacy/data-governance-overview.md#enforcement) i dokumentationsavsnittet för datastyrning.

![dataprincipöverträdelse](../assets/common/data-policy-violation.png)

Om inga principöverträdelser har identifierats markerar du **[!UICONTROL Finish]** för att bekräfta ditt val och börja skicka data till målet.

![Granska](../assets/ui/activate-segment-streaming-destinations/review.png)

## Verifiera segmentaktivering {#verify}

Läs [dokumentationen för målövervakning](../../dataflows/ui/monitor-destinations.md) om du vill ha mer information om hur du övervakar dataflödet till dina mål.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segment membership in the audience would be added and removed as users are qualified or disqualified for the activated segments.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical segment qualifications are sent to [!DNL Facebook] when you activate the segments to the destination.
-->
