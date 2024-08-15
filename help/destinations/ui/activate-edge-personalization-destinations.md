---
title: Aktivera målgrupper för att kanalisera personaliseringsmål
description: Lär dig hur du kan aktivera målgrupper från Adobe Experience Platform för att kanalisera personaliseringsmål för samma sida och nästa sida.
type: Tutorial
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: 14dccb993b38ca352c6de3ed851bafe7c44ca631
workflow-type: tm+mt
source-wordcount: '1878'
ht-degree: 0%

---


# Aktivera målgrupper för att kanalisera personaliseringsmål

## Översikt {#overview}

Adobe Experience Platform använder [kantsegmentering](../../segmentation/ui/edge-segmentation.md) tillsammans med [kantmål](/help/destinations/destination-types.md#edge-personalization-destinations) för att göra det möjligt för kunder att skapa och inrikta sig på målgrupper i stor skala i realtid. Den här funktionen hjälper er att konfigurera användningen av personalisering på samma sida och nästa sida.

Exempel på kantmål är [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md)- och [anpassade personaliseringsanslutningar](../../destinations/catalog/personalization/custom-personalization.md).

>[!NOTE]
>
>När [konfigurerar Adobe Target-anslutningen](../catalog/personalization/adobe-target-connection.md) *utan* med ett datastream-ID stöds inte de användningsfall som beskrivs i den här artikeln. Endast nästa sessionspersonalisering stöds i frånvaro av ett datastream.

>[!IMPORTANT]
> 
> * Om du vill aktivera data och aktivera [mappningssteget](#mapping) för arbetsflödet behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions).
> * Om du vill aktivera data utan att gå igenom [mappningssteget](#mapping) i arbetsflödet behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Segment without Mapping]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions).
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}
> 
> Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

I den här artikeln förklaras det arbetsflöde som krävs för att aktivera målgrupper för Adobe Experience Platform edge-mål. När de används tillsammans med [kantsegmentering](../../segmentation/ui/edge-segmentation.md) och den valfria [profilattributsmappningen](#mapping) aktiverar dessa mål personalisering på samma sida och nästa sida på dina webb- och mobilegenskaper.

Se videon nedan för en kort översikt över hur du konfigurerar Adobe Target-anslutningen för kantanpassning.

>[!NOTE]
>
>Användargränssnittet i Experience Platform uppdateras ofta och kan ha ändrats sedan videon spelades in. Den senaste informationen finns i konfigurationsstegen som beskrivs i avsnitten nedan.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

Titta på videon nedan om du vill få en kort översikt över hur du delar målgrupper och profilattribut med Adobe Target och anpassade destinationer för personalisering.

>[!VIDEO](https://video.tv.adobe.com/v/3419036/?quality=12&learn=on)

## Användningsfall {#use-cases}

Använd personaliseringslösningar från Adobe, till exempel Adobe Target, eller egna partnerplattformar för personalisering (till exempel [!DNL Optimizely], [!DNL Pega]), samt egna system (till exempel intern CMS) för att skapa en djupare personaliseringsupplevelse via [anpassade Personalization](../catalog/personalization/custom-personalization.md) -destinationer. Allt detta och utnyttja även datainsamling och segmentering från Experience Platform Edge Network.

De användningsexempel som beskrivs nedan omfattar både webbplatspersonalisering och riktad webbannonsering.

För att aktivera dessa användningsfall behöver kunderna ett snabbt och smidigt sätt att hämta både målgrupps- och profilattributinformation från Experience Platform och skicka informationen till antingen [Adobe Target](../catalog/personalization/adobe-target-connection.md)- eller [anpassade Personalization](../catalog/personalization/custom-personalization.md)-anslutningar i användargränssnittet i Experience Platform.

### Personalisering på samma sida {#same-page}

En användare besöker en sida på webbplatsen. Du kan använda den aktuella sidans besöksinformation (till exempel URL, webbläsarspråk, inbäddad produktinformation) för att välja nästa åtgärd eller beslut (till exempel anpassning) med hjälp av anslutningen [Anpassad anpassning](../catalog/personalization/custom-personalization.md) för andra plattformar än Adobe (till exempel [!DNL Pega], [!DNL Optimizely] eller andra).

### Anpassa nästa sida {#next-page}

En användare besöker Sida A på din webbplats. Utifrån denna interaktion har användaren kvalificerat sig för en uppsättning målgrupper. Användaren klickar sedan på en länk som tar dem från sida A till sida B. De målgrupper som användaren har varit berättigad till under den föregående interaktionen på sida A, tillsammans med de profiluppdateringar som bestäms av det aktuella webbplatsbesöket, kommer att användas för att driva nästa åtgärd eller beslut (t.ex. vilken annonsbanderoll som ska visas för besökaren eller, vid A/B-testning, vilken version av sidan som ska visas).

### Anpassa nästa session {#next-session}

En användare besöker flera sidor på webbplatsen. Utifrån dessa interaktioner har användaren kvalificerat sig för en uppsättning målgrupper. Användaren avbryter sedan den aktuella webbläsarsessionen.

Följande dag kommer användaren tillbaka till samma kundwebbplats. De målgrupper de hade kvalificerat sig för under den tidigare interaktionen med alla besökta webbplatser, tillsammans med de profiluppdateringar som bestäms av det aktuella webbplatsbesöket, kommer att användas för att välja nästa åtgärd/beslut (t.ex. vilken annonsbanderoll som ska visas för besökaren eller, vid A/B-testning, vilken version av sidan som ska visas).

### Anpassa en banner för hemsidor {#home-page-banner}

Ett uthyrnings- och säljföretag vill personalisera sin hemsida med en banderoll utifrån målgruppskvalifikationer i Adobe Experience Platform. Företaget kan välja vilka målgrupper som ska få en personaliserad upplevelse och skicka dessa målgrupper till Adobe Target som målinriktningskriterier för deras Target-erbjudande.

## Förhandskrav {#prerequisites}

### Konfigurera ett datastream i användargränssnittet för datainsamling {#configure-datastream}

Det första steget för att konfigurera ditt personaliseringsmål är att konfigurera ett datastream för Experience Platform Web SDK. Detta görs i användargränssnittet för datainsamling.

När du konfigurerar datastream ska du under **[!UICONTROL Adobe Experience Platform]** kontrollera att både **[!UICONTROL Edge Segmentation]** och **[!UICONTROL Personalization Destinations]** är markerade.

>[!TIP]
>
>Från och med versionen från april 2024 behöver du inte markera kryssrutan Edge Segmentation när du [konfigurerar anslutningen till Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md). I det här fallet är [nästa sessionspersonalisering](#next-session) det enda tillgängliga användningsexemplet för personalisering.

![Dataströmskonfiguration med Edge Segmentering och Personalization Destinations markerade!](../assets/ui/activate-edge-personalization-destinations/datastream-config.png)

Mer information om hur du konfigurerar ett dataflöde finns i anvisningarna i [Platform Web SDK-dokumentationen](../../datastreams/configure.md#aep).

### Skapa en [!DNL Active-On-Edge]-sammanslagningsprincip {#create-merge-policy}

När du har skapat målanslutningen måste du skapa en [!DNL Active-On-Edge]-sammanfogningsprincip. Sammanslagningsprincipen [!DNL Active-On-Edge] säkerställer att målgrupperna hela tiden utvärderas [ vid sidan ](../../segmentation/ui/edge-segmentation.md) och är tillgängliga för användning av personalisering i realtid och på nästa sida.

>[!IMPORTANT]
>
>För närvarande stöder kantmål endast aktivering av målgrupper som använder [Active-on-Edge Merge Policy](../../segmentation/ui/segment-builder.md#merge-policies) inställd som standard. Om du mappar målgrupper som använder en annan sammanfogningsprincip till kantmål utvärderas inte dessa målgrupper.

Följ instruktionerna på [skapa en sammanfogningsprincip](../../profile/merge-policies/ui-guide.md#create-a-merge-policy) och se till att aktivera alternativet **[!UICONTROL Active-On-Edge Merge Policy]**.

### Skapa en ny publik i Platform {#create-audience}

När du har skapat sammanfogningsprincipen [!DNL Active-On-Edge] måste du skapa en ny publik i Platform.

Följ guiden [målgruppsbyggaren](../../segmentation/ui/segment-builder.md) för att skapa din nya målgrupp och se till att [tilldela den](../../segmentation/ui/segment-builder.md#merge-policies) den [!DNL Active-On-Edge] sammanslagningsprincip som du skapade i föregående steg.

### Skapa en målanslutning {#connect-destination}

När du har konfigurerat dataströmmen kan du börja konfigurera ditt personaliseringsmål.

Följ självstudiekursen [för att skapa en målanslutning](../ui/connect-destination.md) om du vill ha mer information om hur du skapar en ny målanslutning.

Beroende på vilket mål du konfigurerar kan du läsa följande artiklar för att få information om målspecifika krav och relaterad information:

* [Adobe Target](../catalog/personalization/adobe-target-connection.md#parameters)
* [Anpassad personaliseringsanslutning](../catalog/personalization/custom-personalization.md#parameters)

## Välj mål {#select-destination}

När du är klar med kraven kan du nu välja vilket mål för kantanpassning som ska användas för personalisering på samma sida och nästa sida.

1. Gå till **[!UICONTROL Connections > Destinations]** och välj fliken **[!UICONTROL Catalog]**.

   ![Fliken Målkatalog markerad i användargränssnittet för Experience Platform.](../assets/ui/activate-edge-personalization-destinations/catalog-tab.png)

1. Välj **[!UICONTROL Activate audiences]** på det kort som motsvarar det anpassningsmål där du vill aktivera målgrupperna, vilket visas i bilden nedan.

   ![Aktivera målgruppskontroll som är markerad på ett målkort i katalogen.](../assets/ui/activate-edge-personalization-destinations/activate-audiences-button.png)

1. Markera målanslutningen som du vill använda för att aktivera målgrupperna och välj sedan **[!UICONTROL Next]**.

   ![Välj målsteg i aktiveringsarbetsflödet.](../assets/ui/activate-edge-personalization-destinations/select-destination.png)

1. Gå till nästa avsnitt för att [välja dina målgrupper](#select-audiences).

## Välj målgrupper {#select-audiences}

Använd kryssrutorna till vänster om målgruppsnamnen för att välja de målgrupper som du vill aktivera för målet och välj sedan **[!UICONTROL Next]**.

Om du vill välja vilka målgrupper du vill aktivera för målet använder du kryssrutorna till vänster om målgruppsnamnen och väljer sedan **[!UICONTROL Next]**.

Du kan välja mellan flera typer av målgrupper, beroende på deras ursprung:

* **[!UICONTROL Segmentation Service]**: Publiker som genererats i Experience Platform av segmenteringstjänsten. Mer information finns i [segmenteringsdokumentationen](../../segmentation/ui/overview.md).
* **[!UICONTROL Custom upload]**: Publiker som genererats utanför Experience Platform och överförts till Platform som CSV-filer. Mer information om externa målgrupper finns i dokumentationen om att [importera en målgrupp](../../segmentation/ui/audience-portal.md#import-audience).
* Andra typer av målgrupper som kommer från andra Adobe-lösningar, till exempel [!DNL Audience Manager].

![Välj målgruppssteg i aktiveringsarbetsflödet med flera målgrupper markerade.](../assets/ui/activate-edge-personalization-destinations/select-audiences.png)

## Mappningsattribut {#mapping}

>[!IMPORTANT]
>
>Profilattribut kan innehålla känsliga data. För att skydda dessa data kräver målet **[!UICONTROL Custom Personalization]** att du använder [Edge Network Server-API](../../server-api/overview.md) när du konfigurerar målet för attributbaserad personalisering. Alla Server-API-anrop måste göras i en [autentiserad kontext](../../server-api/authentication.md).
>
><br>Om du redan använder Web SDK eller Mobile SDK för din integrering kan du hämta attribut via Server-API:t genom att lägga till en integration på serversidan.
>
><br>Om du inte uppfyller kraven ovan baseras personaliseringen endast på målgruppsmedlemskap.

Välj de attribut baserat på vilka du vill aktivera användningsfall för personalisering för dina användare. Det innebär att om värdet för ett attribut ändras eller om ett attribut läggs till i en profil, kommer den profilen att bli medlem i målgruppen och aktiveras för personaliseringsmålet.

Det är valfritt att lägga till attribut och du kan fortsätta till nästa steg och aktivera anpassning av samma sida och nästa sida utan att välja attribut. Om du inte lägger till några attribut i det här steget sker fortfarande personalisering baserat på målgruppsmedlemskap och identitetskarta för profiler.

![Bild som visar mappningssteget med ett markerat attribut.](../assets/ui/activate-edge-personalization-destinations/mapping-step.png)

### Välj källattribut {#select-source-attributes}

Om du vill lägga till källattribut väljer du kontrollen **[!UICONTROL Add new field]** i kolumnen **[!UICONTROL Source field]** och söker efter eller navigerar till det önskade XDM-attributfältet, vilket visas nedan.

![Skärminspelning som visar hur du väljer ett målattribut i mappningssteget.](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-attribute.gif)

### Välj målattribut {#select-target-attributes}

Om du vill lägga till målattribut markerar du kontrollen **[!UICONTROL Add new field]** i kolumnen **[!UICONTROL Target field]** och skriver in det anpassade attributnamnet som du vill mappa källattributet till.

>[!NOTE]
>
>Markeringen av målattribut gäller endast för aktiveringsarbetsflödet [Anpassad Personalization](../catalog/personalization/custom-personalization.md), för att ge stöd för fältmappning med egna namn på målplattformen.

![Skärminspelning som visar hur du väljer ett XDM-attribut i mappningssteget](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-target-attribute.gif)

## Schemalägg målgruppsexport {#scheduling}

Som standard visar sidan [!UICONTROL Audience schedule] bara de nyvalda målgrupperna som du valde i det aktuella aktiveringsflödet.

Om du vill se alla målgrupper som aktiveras till ditt mål använder du filtreringsalternativet och inaktiverar filtret **[!UICONTROL Show new audiences only]**.

![Alla målgrupper har markerats.](../assets/ui/activate-edge-personalization-destinations/all-audiences.png)

På sidan **[!UICONTROL Audience schedule]** väljer du varje målgrupp och använder sedan väljarna **[!UICONTROL Start date]** och **[!UICONTROL End date]** för att konfigurera tidsintervallet för att skicka data till målet.

![Målgruppssteget i aktiveringsarbetsflödet med start- och slutdatumet markerat.](../assets/ui/activate-edge-personalization-destinations/audience-schedule.png)

Välj **[!UICONTROL Next]** om du vill gå till sidan [!UICONTROL Review].

## Granska {#review}

På sidan **[!UICONTROL Review]** kan du se en sammanfattning av ditt val. Välj **[!UICONTROL Cancel]** om du vill dela upp flödet, **[!UICONTROL Back]** om du vill ändra inställningarna eller **[!UICONTROL Finish]** om du vill bekräfta ditt val och börja skicka data till målet.

![Markeringssammanfattning i granskningssteget.](../assets/ui/activate-edge-personalization-destinations/review.png)

### Principutvärdering av samtycke {#consent-policy-evaluation}

Om din organisation har köpt **Adobe Healthcare Shield** eller **Adobe Privacy &amp; Security Shield** väljer du **[!UICONTROL View applicable consent policies]** för att se vilka medgivandepolicyer som tillämpas och hur många profiler som inkluderas i aktiveringen som ett resultat av dem. Läs mer om [utvärdering av medgivandeprincip](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation).

### Kontroller av policyer för dataanvändning {#data-usage-policy-checks}

I steget **[!UICONTROL Review]** söker Experience Platform även efter överträdelser av dataanvändningsprinciper. Nedan visas ett exempel där en princip överträds. Du kan inte slutföra arbetsflödet för målgruppsaktivering förrän du har löst överträdelsen. Mer information om hur du löser policyöverträdelser finns i [brott mot dataanvändningsprinciper](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) i dokumentationsavsnittet för datastyrning.

![Ett exempel på en dataprincipöverträdelse.](../assets/common/data-policy-violation.png)

### Filtrera målgrupper {#filter-audiences}

I det här steget kan du använda de tillgängliga filtren på sidan för att endast visa målgrupper vars schema eller mappning har uppdaterats som en del av det här arbetsflödet. Du kan också växla vilka tabellkolumner som du vill se.

![Skärminspelning som visar tillgängliga målgruppsfilter i granskningssteget.](../assets/ui/activate-edge-personalization-destinations/filter-audiences-review-step.gif)

Om du är nöjd med ditt val och inga principöverträdelser har identifierats, markerar du **[!UICONTROL Finish]** för att bekräfta ditt val och börja skicka data till målet.

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify audience activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->
