---
keywords: aktivera mål för profilbegäran;aktivera data;mål för profilbegäran
title: Aktivera målgruppsdata för att profilera mål för begäran
type: Tutorial
description: Lär dig hur du aktiverar målgruppsdata i Adobe Experience Platform genom att mappa segment till profilförfrågningar.
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: cda4591021c5b0a0bd6f43765d72b5867ec59aea
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---

# Aktivera målgruppsdata för att profilera mål för begäran

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

## Översikt {#overview}

I den här artikeln förklaras det arbetsflöde som krävs för att aktivera målgruppsdata i Adobe Experience Platform-profilförfrågningar. Vid användning tillsammans med [kantsegmentering](../../segmentation/ui/edge-segmentation.md)kan de här målen användas för att anpassa webbsidor efter sida och nästa sida i era webbegenskaper. Läs mer om [aktivera personalisering på samma sida och nästa sida](/help/destinations/ui/configure-personalization-destinations.md).

Exempel på mål för profilbegäran är [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) och [Anpassad personalisering](../../destinations/catalog/personalization/custom-personalization.md) anslutningar.

## Förutsättningar {#prerequisites}

Du måste ha aktiverat data till destinationer [ansluten till ett mål](./connect-destination.md). Om du inte redan har gjort det går du till [målkatalog](../catalog/overview.md), bläddra bland de anpassningsmål som stöds och konfigurera det mål som du vill använda.

### Sammanslagningsprincip för segment {#merge-policy}

För närvarande stöder profilförfrågningar endast aktivering av segment som använder [Active-on-Edge Merge Policy](../../segmentation/ui/segment-builder.md#merge-policies) anges som standard.

## Välj mål {#select-destination}

1. Gå till **[!UICONTROL Connections > Destinations]** och väljer **[!UICONTROL Catalog]** -fliken.

   ![Fliken Målkatalog](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Välj **[!UICONTROL Activate segments]** på kortet som motsvarar det personaliseringsmål där du vill aktivera dina segment, vilket visas i bilden nedan.

   ![Aktivera knappar](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. Markera målanslutningen som du vill använda för att aktivera dina segment och välj sedan **[!UICONTROL Next]**.

   ![Välj mål](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. Gå till nästa avsnitt till [markera segment](#select-segments).

## Välj segment {#select-segments}

Använd kryssrutorna till vänster om segmentnamnen för att markera de segment som du vill aktivera för målet och markera sedan **[!UICONTROL Next]**.

![Markera segment](../assets/ui/activate-profile-request-destinations/select-segments.png)

## (Beta) Mappningsattribut {#map-attributes}

>[!IMPORTANT]
>
>Mappningssteget, som möjliggör attributbaserad personalisering för [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) och [generiska personaliseringsmål](/help/destinations/catalog/personalization/custom-personalization.md), är för närvarande i betaversion och din organisation kanske inte har tillgång till den än. Dokumentationen kan komma att ändras.

Välj de attribut baserat på vilka du vill aktivera användningsfall för personalisering för dina användare. Det innebär att om värdet för ett attribut ändras eller om ett attribut läggs till i en profil, kommer den profilen att bli medlem i segmentet och aktiveras för personaliseringsmålet.

Det är valfritt att lägga till attribut och du kan fortsätta till nästa steg och aktivera anpassning av samma sida och nästa sida utan att välja attribut. Om du inte lägger till några attribut i det här steget sker fortfarande personalisering baserat på segmentmedlemskapet och identitetskartan för profiler.

![Bild som visar mappningssteget med ett markerat attribut](../assets/ui/activate-profile-request-destinations/mapping-step.png)

### Välj källattribut {#select-source-attributes}

Om du vill lägga till källattribut väljer du **[!UICONTROL Add new field]** kontroll på **[!UICONTROL Source field]** kolumn och sök eller navigera till önskat XDM-attributfält, enligt nedan.

![Skärminspelning som visar hur du väljer ett målattribut i mappningssteget](../assets/ui/activate-profile-request-destinations/mapping-step-select-attribute.gif)

### Välj målattribut {#select-target-attributes}

>[!NOTE]
>
>Vissa mål kräver att du bara väljer källattribut, medan andra kräver både käll- och målattribut.
>
>För närvarande är [Adobe Target V2](../catalog/personalization/adobe-target-connection.md) mål endast kräver källattribut, medan [Anpassad anpassning med attribut](../catalog/personalization/custom-personalization.md) kräver både käll- och målattribut.

Om du vill lägga till målattribut väljer du **[!UICONTROL Add new field]** kontroll på **[!UICONTROL Target field]** kolumn och typ i det anpassade attributnamn som du vill mappa källattributet till.

![Skärminspelning som visar hur du väljer ett XDM-attribut i mappningssteget](../assets/ui/activate-profile-request-destinations/mapping-step-select-target-attribute.gif)

## Schemalägg segmentexport {#scheduling}

Som standard är [!UICONTROL Segment schedule] visas endast de nyligen valda segmenten som du valde i det aktuella aktiveringsflödet.

![Nya segment](../assets/ui/activate-profile-request-destinations/new-segments.png)

Om du vill se alla segment som aktiveras till målet använder du filteralternativet och inaktiverar **[!UICONTROL Show new segments only]** filter.

![Alla segment](../assets/ui/activate-profile-request-destinations/all-segments.png)

På **[!UICONTROL Segment schedule]** markerar du varje segment och använder sedan **[!UICONTROL Start date]** och **[!UICONTROL End date]** väljare för att konfigurera tidsintervallet för att skicka data till målet.

![Segmentschema](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

Välj **[!UICONTROL Next]** för att gå till [!UICONTROL Review] sida.

## Granska {#review}

På **[!UICONTROL Review]** kan du se en sammanfattning av markeringen. Välj **[!UICONTROL Cancel]** för att bryta upp flödet, **[!UICONTROL Back]** för att ändra dina inställningar, eller **[!UICONTROL Finish]** för att bekräfta ditt val och börja skicka data till målet.

>[!IMPORTANT]
>
>I det här steget söker Adobe Experience Platform efter brott mot dataanvändningspolicyn. Nedan visas ett exempel där en princip överträds. Du kan inte slutföra arbetsflödet för segmentaktivering förrän du har löst konflikten. Mer information om hur du löser policyöverträdelser finns i [Politiska åtgärder](../../rtcdp/privacy/data-governance-overview.md#enforcement) i dokumentationsavsnittet för datastyrning.

![dataprincipöverträdelse](../assets/common/data-policy-violation.png)

Om inga principöverträdelser har identifierats väljer du **[!UICONTROL Finish]** för att bekräfta ditt val och börja skicka data till målet.

![Granska](../assets/ui/activate-profile-request-destinations/review.png)

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify segment activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->