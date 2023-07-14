---
title: Aktivera målgrupper för att kanalisera personaliseringsmål
description: Lär dig hur du kan aktivera målgrupper från Adobe Experience Platform för att kanalisera personaliseringsmål för samma sida och nästa sida.
type: Tutorial
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: 37819b5a6480923686d327e30b1111ea29ae71da
workflow-type: tm+mt
source-wordcount: '1757'
ht-degree: 0%

---


# Aktivera målgrupper för att kanalisera personaliseringsmål

## Översikt {#overview}

Adobe Experience Platform använder [kantsegmentering](../../segmentation/ui/edge-segmentation.md) tillsammans med edge-mål för att kunderna ska kunna skapa och inrikta sig på målgrupper i stor skala, i realtid. Den här funktionen hjälper er att konfigurera användningen av personalisering på samma sida och nästa sida.

Exempel på kantmål är [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) och [Anpassad personalisering](../../destinations/catalog/personalization/custom-personalization.md) anslutningar.

>[!NOTE]
>
>När [konfigurera Adobe Target-anslutningen](../catalog/personalization/adobe-target-connection.md) de användningsfall som beskrivs i den här artikeln stöds inte utan ett datastream-ID. Endast nästa sessionspersonalisering stöds i frånvaro av ett datastream.

>[!IMPORTANT]
> 
> * Aktivera data och aktivera [mappningssteg](#mapping) i arbetsflödet behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions).
> * Aktivera data utan att gå igenom [mappningssteg](#mapping) i arbetsflödet behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Segment without Mapping]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions).
> 
> Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

I den här artikeln förklaras det arbetsflöde som krävs för att aktivera målgrupper i Adobe Experience Platform edge-mål. Vid användning tillsammans med [kantsegmentering](../../segmentation/ui/edge-segmentation.md) och valfria [profilattributsmappning](#mapping)kan dessa mål användas för personalisering på samma sida och nästa sida på era webb- och mobilsajter.

Se videon nedan för en kort översikt över hur du konfigurerar Adobe Target-anslutningen för kantanpassning.

>[!NOTE]
>
>Användargränssnittet i Experience Platform uppdateras ofta och kan ha ändrats sedan videon spelades in. Den senaste informationen finns i konfigurationsstegen som beskrivs i avsnitten nedan.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

Titta på videon nedan om du vill få en kort översikt över hur du delar målgrupper och profilattribut med Adobe Target och anpassade destinationer för personalisering.

>[!VIDEO](https://video.tv.adobe.com/v/3419036/?quality=12&learn=on)

## Användningsfall {#use-cases}

Med personaliseringsmål för Edge kan ni använda personaliseringslösningar från Adobe, som Adobe Target, eller egna partnerplattformar för personalisering (till exempel [!DNL Optimizely], [!DNL Pega]), liksom egna system (t.ex. intern CMS) som ger en djupare personaliseringsupplevelse via [Anpassad personalisering](../catalog/personalization/custom-personalization.md) mål. Allt detta och utnyttja även datainsamling och segmenteringsfunktioner för Experience Platform Edge Network.

De användningsexempel som beskrivs nedan omfattar både webbplatspersonalisering och riktad webbannonsering.

För att möjliggöra detta behöver kunderna ett snabbt och smidigt sätt att hämta information om både målgrupper och profilattribut från Experience Platform och skicka informationen till [Adobe Target](../catalog/personalization/adobe-target-connection.md) eller [Anpassad personalisering](../catalog/personalization/custom-personalization.md) Anslutningar i användargränssnittet i Experience Platform.

### Personalisering på samma sida {#same-page}

En användare besöker en sida på webbplatsen. Kunden kan använda den aktuella sidans besöksinformation (till exempel URL, webbläsarspråk, inbäddad produktinformation) för att välja nästa åtgärd/beslut (till exempel personalisering) med hjälp av [Anpassad personalisering](../catalog/personalization/custom-personalization.md) anslutning för andra plattformar än Adobe (t.ex. [!DNL Pega], [!DNL Optimizely], osv.).

### Anpassa nästa sida {#next-page}

En användare besöker Sida A på din webbplats. Utifrån denna interaktion har användaren kvalificerat sig för en uppsättning målgrupper. Användaren klickar sedan på en länk som tar dem från sida A till sida B. De målgrupper som användaren hade kvalificerat sig för under den föregående interaktionen på sida A, tillsammans med de profiluppdateringar som bestäms av det aktuella webbplatsbesöket, kommer att användas för att driva nästa åtgärd/beslut (t.ex. vilken annonsbanderoll som ska visas för besökaren eller, vid A/B-testning, vilken version av sidan som ska visas).

### Anpassa nästa session {#next-session}

En användare besöker flera sidor på webbplatsen. Utifrån dessa interaktioner har användaren kvalificerat sig för en uppsättning målgrupper. Användaren avbryter sedan den aktuella webbläsarsessionen.

Följande dag kommer användaren tillbaka till samma kundwebbplats. De målgrupper de hade kvalificerat sig för under den tidigare interaktionen med alla besökta webbplatser, tillsammans med de profiluppdateringar som bestäms av det aktuella webbplatsbesöket, kommer att användas för att välja nästa åtgärd/beslut (t.ex. vilken annonsbanderoll som ska visas för besökaren eller, vid A/B-testning, vilken version av sidan som ska visas).

### Anpassa en startsidesbanderoll {#home-page-banner}

Ett uthyrnings- och säljföretag vill personalisera sin hemsida med en banderoll utifrån målgruppskvalifikationer i Adobe Experience Platform. Företaget kan välja vilka målgrupper som ska få en personaliserad upplevelse och skicka dem till Adobe Target som målinriktningskriterier för sitt Target-erbjudande.

## Förutsättningar {#prerequisites}

### Konfigurera ett datastream i användargränssnittet för datainsamling {#configure-datastream}

Det första steget för att konfigurera ditt personaliseringsmål är att konfigurera ett datastream för Experience Platform Web SDK. Detta görs i användargränssnittet för datainsamling.

När datastream konfigureras, under **[!UICONTROL Adobe Experience Platform]** se till att båda **[!UICONTROL Edge Segmentation]** och **[!UICONTROL Personalization Destinations]** är markerade.

![Datastream-konfiguration](../assets/ui/activate-edge-personalization-destinations/datastream-config.png)

Mer information om hur du konfigurerar ett dataflöde finns i instruktionerna i [Dokumentation för Platform Web SDK](../../edge/datastreams/configure.md#aep).

### Skapa en [!DNL Active-On-Edge] sammanfogningsprincip {#create-merge-policy}

När du har skapat målanslutningen måste du skapa en [!DNL Active-On-Edge] sammanfogningsprincip. The [!DNL Active-On-Edge] sammanfogningspolicy säkerställer att målgrupper utvärderas kontinuerligt [på kanten](../../segmentation/ui/edge-segmentation.md) och finns tillgängliga för användning av personalisering i realtid och på nästa sida.

>[!IMPORTANT]
>
>För närvarande stöder kantdestinationer endast aktivering av målgrupper som använder [Active-on-Edge Merge Policy](../../segmentation/ui/segment-builder.md#merge-policies) anges som standard. Om du mappar målgrupper som använder en annan sammanfogningsprincip till kantmål utvärderas inte dessa målgrupper.

Följ instruktionerna på [skapa en sammanfogningsprincip](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)och se till att aktivera **[!UICONTROL Active-On-Edge Merge Policy]** växla.

### Skapa en ny publik i Platform {#create-audience}

När du har skapat [!DNL Active-On-Edge] måste ni skapa en ny publik i Platform.

Följ [målgruppsverktyg](../../segmentation/ui/segment-builder.md) skapa en ny målgrupp och se till att [tilldela den](../../segmentation/ui/segment-builder.md#merge-policies) den [!DNL Active-On-Edge] sammanfogningsprincip som du skapade i steg 3.

### Skapa en målanslutning {#connect-destination}

När du har konfigurerat dataströmmen kan du börja konfigurera ditt personaliseringsmål.

Följ [självstudiekurs om hur du skapar målanslutning](../ui/connect-destination.md) om du vill ha detaljerade anvisningar om hur du skapar en ny målanslutning.

Beroende på vilket mål du konfigurerar kan du läsa följande artiklar för att få information om målspecifika krav och relaterad information:

* [Adobe Target-anslutning](../catalog/personalization/adobe-target-connection.md#parameters)
* [Anpassad personaliseringsanslutning](../catalog/personalization/custom-personalization.md##parameters)

## Välj mål {#select-destination}

När du är klar med kraven kan du nu välja vilket mål för kantanpassning som ska användas för personalisering på samma sida och nästa sida.

1. Gå till **[!UICONTROL Connections > Destinations]** och väljer **[!UICONTROL Catalog]** -fliken.

   ![Fliken Målkatalog](../assets/ui/activate-edge-personalization-destinations/catalog-tab.png)

1. Välj **[!UICONTROL Activate audiences]** på det kort som motsvarar det personaliseringsmål där du vill aktivera målgrupperna, vilket visas i bilden nedan.

   ![Aktivera knappar](../assets/ui/activate-edge-personalization-destinations/activate-audiences-button.png)

1. Välj den målanslutning som du vill använda för att aktivera dina målgrupper och välj sedan **[!UICONTROL Next]**.

   ![Välj mål](../assets/ui/activate-edge-personalization-destinations/select-destination.png)

1. Gå till nästa avsnitt till [välj era målgrupper](#select-audiences).

## Välj målgrupper {#select-audiences}

Använd kryssrutorna till vänster om målgruppsnamnen för att välja de målgrupper som du vill aktivera för målet och markera sedan **[!UICONTROL Next]**.

Om du vill välja vilka målgrupper du vill aktivera för målet använder du kryssrutorna till vänster om målgruppsnamnen och väljer sedan **[!UICONTROL Next]**.

Du kan välja mellan flera typer av målgrupper, beroende på deras ursprung:

* **[!UICONTROL Segmentation Service]**: Målgrupper som genererats i Experience Platform av segmenteringstjänsten. Se [segmenteringsdokumentation](../../segmentation/ui/overview.md) för mer information.
* **[!UICONTROL Custom upload]**: Publiker som genererats utanför Experience Platform och överförts till Platform som CSV-filer. Mer information om externa målgrupper finns i dokumentationen om [importera en publik](../../segmentation/ui/overview.md#import-audience).
* Andra typer av målgrupper som härrör från andra Adobe-lösningar, t.ex. [!DNL Audience Manager].

![Välj målgrupper](../assets/ui/activate-edge-personalization-destinations/select-audiences.png)

## Mappningsattribut {#mapping}

>[!IMPORTANT]
>
>Profilattribut kan innehålla känsliga data. För att skydda dessa data **[!UICONTROL Custom Personalization]** mål kräver att du använder [API för Edge Network Server](../../server-api/overview.md) när målet för attributbaserad personalisering konfigureras. Alla Server-API-anrop måste göras i en [autentiserad kontext](../../server-api/authentication.md).
>
><br>Om du redan använder Web SDK eller Mobile SDK för din integrering kan du hämta attribut via Server-API:t genom att lägga till en integration på serversidan.
>
><br>Om ni inte uppfyller kraven ovan kommer personaliseringen endast att baseras på målgruppsmedlemskap.

Välj de attribut baserat på vilka du vill aktivera användningsfall för personalisering för dina användare. Det innebär att om värdet för ett attribut ändras eller om ett attribut läggs till i en profil, kommer den profilen att bli medlem i målgruppen och aktiveras för personaliseringsmålet.

Det är valfritt att lägga till attribut och du kan fortsätta till nästa steg och aktivera anpassning av samma sida och nästa sida utan att välja attribut. Om du inte lägger till några attribut i det här steget sker fortfarande personalisering baserat på målgruppsmedlemskap och identitetskarta för profiler.

![Bild som visar mappningssteget med ett markerat attribut](../assets/ui/activate-edge-personalization-destinations/mapping-step.png)

### Välj källattribut {#select-source-attributes}

Om du vill lägga till källattribut väljer du **[!UICONTROL Add new field]** kontroll på **[!UICONTROL Source field]** kolumn och sök eller navigera till önskat XDM-attributfält, enligt nedan.

![Skärminspelning som visar hur du väljer ett målattribut i mappningssteget](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-attribute.gif)

### Välj målattribut {#select-target-attributes}

Om du vill lägga till målattribut väljer du **[!UICONTROL Add new field]** kontroll på **[!UICONTROL Target field]** kolumn och typ i det anpassade attributnamn som du vill mappa källattributet till.

>[!NOTE]
>
>Markeringen av målattribut gäller bara för [Anpassad personalisering](../catalog/personalization/custom-personalization.md) aktiveringsarbetsflöde för att ge stöd för fältmappning med egna namn på målplattformen.

![Skärminspelning som visar hur du väljer ett XDM-attribut i mappningssteget](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-target-attribute.gif)

## Schemalägg målgruppsexport {#scheduling}

Som standard är [!UICONTROL Audience schedule] visas endast de nyvalda målgrupperna som du valde i det aktuella aktiveringsflödet.

Om du vill se alla målgrupper som aktiveras till destinationen använder du filteralternativet och inaktiverar **[!UICONTROL Show new audiences only]** filter.

![Alla målgrupper](../assets/ui/activate-edge-personalization-destinations/all-audiences.png)

På **[!UICONTROL Audience schedule]** väljer du varje målgrupp och använder sedan **[!UICONTROL Start date]** och **[!UICONTROL End date]** väljare för att konfigurera tidsintervallet för att skicka data till målet.

![Målgruppsschema](../assets/ui/activate-edge-personalization-destinations/audience-schedule.png)

Välj **[!UICONTROL Next]** för att gå till [!UICONTROL Review] sida.

## Granska {#review}

På **[!UICONTROL Review]** kan du se en sammanfattning av markeringen. Välj **[!UICONTROL Cancel]** för att bryta upp flödet, **[!UICONTROL Back]** för att ändra dina inställningar, eller **[!UICONTROL Finish]** för att bekräfta ditt val och börja skicka data till målet.

![Markeringssammanfattning i granskningssteget.](../assets/ui/activate-edge-personalization-destinations/review.png)

### Principutvärdering av samtycke {#consent-policy-evaluation}

Om din organisation har köpt **Adobe Healthcare Shield** eller **Adobe Privacy &amp; Security Shield**, markera **[!UICONTROL View applicable consent policies]** för att se vilka regler för samtycke som tillämpas och hur många profiler som inkluderas i aktiveringen till följd av dessa. Läs om [utvärdering av godkännandepolicy](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) för mer information.

### Kontroller av policyer för dataanvändning {#data-usage-policy-checks}

I **[!UICONTROL Review]** Experience Platform kontrollerar också om dataanvändningspolicyn har överträtts. Nedan visas ett exempel där en princip överträds. Du kan inte slutföra arbetsflödet för målgruppsaktivering förrän du har löst överträdelsen. Mer information om hur du löser policyöverträdelser finns i [brott mot dataanvändningsprinciper](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) i dokumentationsavsnittet för datastyrning.

![dataprincipöverträdelse](../assets/common/data-policy-violation.png)

### Filtrera målgrupper {#filter-audiences}

I det här steget kan du använda de tillgängliga filtren på sidan för att endast visa målgrupper vars schema eller mappning har uppdaterats som en del av det här arbetsflödet. Du kan också växla vilka tabellkolumner som du vill se.

![Skärminspelning som visar tillgängliga målgruppsfilter i granskningssteget.](../assets/ui/activate-edge-personalization-destinations/filter-audiences-review-step.gif)

Om du är nöjd med ditt val och inga policyöverträdelser har identifierats väljer du **[!UICONTROL Finish]** för att bekräfta ditt val och börja skicka data till målet.

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify audience activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->
