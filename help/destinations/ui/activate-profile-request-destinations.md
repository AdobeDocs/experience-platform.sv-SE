---
keywords: aktivera mål för profilbegäran;aktivera data;mål för profilbegäran
title: Aktivera målgruppsdata för att profilera mål för begäran
type: Tutorial
seo-title: Activate audience data to profile request destinations
description: Lär dig hur du aktiverar målgruppsdata i Adobe Experience Platform genom att mappa segment till profilförfrågningar.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by mapping segments to profile request destinations.
source-git-commit: caccd096c9165139d9b966bbfcb311456276192a
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# Aktivera målgruppsdata för att profilera mål för begäran (beta)

## Översikt {#overview}

>[!IMPORTANT]
>
>Destinationer för profilförfrågningar i Adobe Experience Platform är för närvarande i Beta. Dokumentationen och funktionerna kan komma att ändras.

I den här artikeln förklaras det arbetsflöde som krävs för att aktivera målgruppsdata i Adobe Experience Platform-profilförfrågningar. Exempel på mål för profilbegäran är [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) och [Anpassad personalisering](../../destinations/catalog/personalization/custom-personalization.md)-anslutningar.

## Förutsättningar {#prerequisites}

Om du vill aktivera data till mål måste du ha [anslutit till ett mål](./connect-destination.md). Om du inte redan har gjort det går du till [målkatalogen](../catalog/overview.md), bläddrar bland de mål som stöds och konfigurerar det mål som du vill använda.

### Sammanslagningsprincip för segment {#merge-policy}

Målen för profilbegäran stöder för närvarande endast aktivering av segment som använder standardprincipen för sammanfogning. Om du försöker aktivera segment med en annan sammanfogningsprincip uppstår ett fel på [[!UICONTROL Review]](#review)-sidan.

## Välj mål {#select-destination}

1. Gå till **[!UICONTROL Connections > Destinations]** och välj fliken **[!UICONTROL Catalog]**.

   ![Fliken Målkatalog](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Välj **[!UICONTROL Activate segments]** på kortet som motsvarar målet där du vill aktivera dina segment, vilket visas i bilden nedan.

   ![Aktivera knappar](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. Markera målanslutningen som du vill använda för att aktivera dina segment och välj sedan **[!UICONTROL Next]**.

   ![Välj mål](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. Gå till nästa avsnitt för att [markera dina segment](#select-segments).

## Välj segment {#select-segments}

Använd kryssrutorna till vänster om segmentnamnen för att markera de segment som du vill aktivera för målet och välj sedan **[!UICONTROL Next]**.

![Markera segment](../assets/ui/activate-profile-request-destinations/select-segments.png)

## Schemalägg segmentexport {#scheduling}

Som standard visar sidan [!UICONTROL Segment schedule] bara de segment som du nyligen har valt i det aktuella aktiveringsflödet.

![Nya segment](../assets/ui/activate-profile-request-destinations/new-segments.png)

Om du vill se alla segment som aktiveras till målet använder du filteralternativet och inaktiverar filtret **[!UICONTROL Show new segments only]**.

![Alla segment](../assets/ui/activate-profile-request-destinations/all-segments.png)

På sidan **[!UICONTROL Segment schedule]** markerar du varje segment och använder sedan väljarna **[!UICONTROL Start date]** och **[!UICONTROL End date]** för att konfigurera tidsintervallet för att skicka data till målet.

![Segmentschema](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

Välj **[!UICONTROL Next]** om du vill gå till sidan [!UICONTROL Review].

## Granska {#review}

På sidan **[!UICONTROL Review]** visas en sammanfattning av ditt val. Välj **[!UICONTROL Cancel]** om du vill dela upp flödet, **[!UICONTROL Back]** om du vill ändra inställningarna eller **[!UICONTROL Finish]** om du vill bekräfta valet och börja skicka data till målet.

>[!IMPORTANT]
>
>I det här steget söker Adobe Experience Platform efter brott mot dataanvändningspolicyn. Nedan visas ett exempel där en princip överträds. Du kan inte slutföra arbetsflödet för segmentaktivering förrän du har löst konflikten. Mer information om hur du löser policyöverträdelser finns i [Politiska åtgärder](../../rtcdp/privacy/data-governance-overview.md#enforcement) i dokumentationsavsnittet för datastyrning.

![dataprincipöverträdelse](../assets/common/data-policy-violation.png)

Om inga principöverträdelser har identifierats markerar du **[!UICONTROL Finish]** för att bekräfta ditt val och börja skicka data till målet.

![Granska](../assets/ui/activate-profile-request-destinations/review.png)

## Verifiera segmentaktivering {#verify}

Läs [dokumentationen för målövervakning](../../dataflows/ui/monitor-destinations.md) om du vill ha mer information om hur du övervakar dataflödet till dina mål.