---
keywords: Experience Platform;hem;populära ämnen;avanmälan;Segmentering;Segmenteringstjänst;segmenteringstjänst;hedersavanmälan;avanmälan;avanmälan;avanmälan;medgivande;dela;samla;
solution: Experience Platform
title: Hedra samtycke i segment
topic-legacy: overview
description: Lär dig hur du respekterar kundernas önskemål om samtycke vid insamling och delning av personuppgifter i segmentåtgärder.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: 6d11a94d45b4a089ca6960aaf1ce78ae654ebc3f
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---

# Följa samtycke i segment

Lagliga sekretessbestämmelser som [!DNL California Consumer Privacy Act] (CCPA) ger konsumenterna rätt att välja bort att inte låta sina personuppgifter samlas in eller delas med tredje part. Adobe Experience Platform tillhandahåller XDM-komponenter (Experience Data Model) som är avsedda att fånga upp kundernas samtycke i kundprofildata i realtid.

Om en kund har återkallat eller vägrat samtycke för att få sina personuppgifter delade är det viktigt att organisationen respekterar detta när den genererar målgrupper för marknadsföringsaktiviteter. I det här dokumentet beskrivs hur du integrerar värden för kundsamtycke i dina segmentdefinitioner med användargränssnittet i Experience Platform.

## Komma igång

För att uppfylla kundens medgivandevärden krävs en förståelse för de olika [!DNL Adobe Experience Platform]-tjänsterna som är inblandade. Innan du startar den här självstudiekursen bör du kontrollera följande tjänster:

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Ger en enhetlig kundprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Gör att ni kan skapa målgruppssegment utifrån  [!DNL Real-time Customer Profile] data.

## Schemafält för samtycke

För att uppfylla kundens samtycke och önskemål måste ett av scheman som är en del av ditt [!UICONTROL XDM Individual Profile]-unionsschema innehålla standardfältgruppen **[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)]**.

Mer information om strukturen och användningsfallet för vart och ett av attributen i fältgruppen finns i [referenshandboken för ](../xdm/field-groups/profile/consents.md) för godkännande och inställningar. Stegvisa instruktioner om hur du lägger till en fältgrupp i ett schema finns i [XDM-gränssnittshandboken](../xdm/ui/resources/schemas.md#add-field-groups).

När fältgruppen har lagts till i ett [profilaktiverat schema](../xdm/ui/resources/schemas.md#profile) och dess fält har använts för att importera medgivandedata från ditt upplevelseprogram, kan du använda de insamlade medgivandeattributen i dina segmentregler.

## Hantera samtycke vid segmentering

För att säkerställa att bortfallsprofiler inte inkluderas i segment måste specialfält läggas till i befintliga segment och inkluderas när nya segment skapas.

Stegen nedan visar hur du lägger till lämpliga fält för två typer av avanmälningsflaggor:

1. [!UICONTROL Data Collection]
1. [!UICONTROL Share Data]

>[!NOTE]
>
>Den här guiden fokuserar på de två avanmälningsflaggorna ovan, men du kan konfigurera dina segment så att även ytterligare godkännandesignaler inkluderas. Referenshandboken för [godkännanden och inställningar](../xdm/field-groups/profile/consents.md) innehåller mer information om dessa alternativ och deras avsedda användningsfall.

När du skapar ett segment i användargränssnittet, under **[!UICONTROL Attributes]**, navigerar du till **[!UICONTROL XDM Individual Profile]** och väljer sedan **[!UICONTROL Consents and Preferences]**. Här kan du se alternativen för **[!UICONTROL Data Collection]** och **[!UICONTROL Share Data]**.

![](./images/opt-outs/consents.png)

Börja med att välja kategorin **[!UICONTROL Data Collection]** och dra sedan **[!UICONTROL Choice Value]** till segmentbyggaren. När du lägger till attributet till segmentet kan du ange [värdena för medgivande](../xdm/field-groups/profile/consents.md#choice-values) som måste inkluderas eller exkluderas.

![](./images/opt-outs/consent-values.png)

Ett sätt är att utesluta kunder som har valt att inte låta sina data samlas in. Det gör du genom att ange operatorn till **[!UICONTROL does not equal]** och välja följande värden:

* **[!UICONTROL No (opt-out)]**
* **[!UICONTROL Default of No (opt-out)]**
* **[!UICONTROL Unknown]** (om samtycke antas utebli om inte annat är känt)

![](./images/opt-outs/collect.png)

Gå tillbaka till avsnittet **[!UICONTROL Consents and Preferences]** under **[!UICONTROL Attributes]** i den vänstra listen och välj **[!UICONTROL Share Data]**. Dra dess motsvarande **[!UICONTROL Choice Value]** till arbetsytan och välj samma värden som för alternativvärdet [!UICONTROL Data Collection]. Kontrollera att det finns en **[!UICONTROL Or]**-relation mellan de två attributen.

![](./images/opt-outs/share.png)

När både **[!UICONTROL Data Collection]** och **[!UICONTROL Share Data]**-medgivandevärdena har lagts till i segmentet, kommer alla kunder som har valt att inte använda sina data att uteslutas från att få den slutliga målgruppen. Här kan du fortsätta att anpassa segmentdefinitionen innan du väljer **[!UICONTROL Save]** för att slutföra processen.

## Nästa steg

Genom att följa den här självstudiekursen bör du nu få en bättre förståelse för hur ni respekterar kundens samtycke och önskemål när ni bygger segment i Experience Platform.

Mer information om att hantera samtycke i Platform finns i följande dokumentation:

* [Samtyckesbearbetning med Adobe-standard](../landing/governance-privacy-security/consent/adobe/overview.md)
* [Samtyckesbearbetning med IAB TCF 2.0-standarden](../landing/governance-privacy-security/consent/iab/overview.md)