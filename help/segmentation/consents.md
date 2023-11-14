---
solution: Experience Platform
title: Hedra samtycke i segment
description: Lär dig hur du respekterar kundernas önskemål om samtycke vid insamling och delning av personuppgifter i segmentåtgärder.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# Följa samtycke i segment

>[!NOTE]
>
>I den här guiden beskrivs hur du respekterar innehåll i **segmentdefinitioner**.

Lagliga sekretessregler som [!DNL California Consumer Privacy Act] (CCPA) ger konsumenterna rätt att avstå från att få sina personuppgifter insamlade eller delade med tredje part. Adobe Experience Platform tillhandahåller XDM-komponenter (Experience Data Model) som är avsedda att fånga upp kundernas önskemål om samtycke i realtidsdata för kundprofiler.

Om en kund har återkallat eller vägrat samtycke för att få sina personuppgifter delade är det viktigt att organisationen respekterar detta när den genererar målgrupper för marknadsföringsaktiviteter. I det här dokumentet beskrivs hur du integrerar värden för kundsamtycke i dina segmentdefinitioner med användargränssnittet i Experience Platform.

## Komma igång

Att värna om kundens samtycke kräver en förståelse för de olika [!DNL Adobe Experience Platform] berörda tjänster. Innan du startar den här självstudiekursen bör du kontrollera följande tjänster:

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): Tillhandahåller en enhetlig kundprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Används för att bygga målgrupper utifrån [!DNL Real-Time Customer Profile] data.

## Schemafält för samtycke

För att tillgodose kundernas önskemål och önskemål är ett av scheman som ingår i [!UICONTROL XDM Individual Profile] union-schemat måste innehålla standardfältgruppen **[!UICONTROL Consents and Preferences]**.

Mer information om struktur och avsedd användning för varje attribut som tillhandahålls av fältgruppen finns i [referenshandbok för innehåll och inställningar](../xdm/field-groups/profile/consents.md). Stegvisa instruktioner om hur du lägger till en fältgrupp i ett schema finns i [Användargränssnittshandbok för XDM](../xdm/ui/resources/schemas.md#add-field-groups).

När fältgruppen har lagts till i en [Profilaktiverat schema](../xdm/ui/resources/schemas.md#profile) och dess fält har använts för att hämta medgivandedata från ditt upplevelseprogram, kan du använda de insamlade medgivandeattributen i dina segmentregler.

## Hantera samtycke vid segmentering

För att säkerställa att bortfallsprofiler inte inkluderas i segmentdefinitionerna måste specialfält läggas till i befintliga segmentdefinitioner och inkluderas när nya segmentdefinitioner skapas.

Stegen nedan visar hur du lägger till lämpliga fält för två typer av avanmälningsflaggor:

1. [!UICONTROL Data Collection]
1. [!UICONTROL Share Data]

>[!NOTE]
>
>Den här guiden fokuserar på de två avanmälningsflaggorna ovan, men du kan konfigurera dina segmentdefinitioner så att de även innehåller ytterligare godkännandesignaler. The [referenshandbok för innehåll och inställningar](../xdm/field-groups/profile/consents.md) innehåller mer information om dessa alternativ och de användningsfall de är avsedda för.

När en segmentdefinition skapas i användargränssnittet, under **[!UICONTROL Attributes]**, navigera till **[!UICONTROL XDM Individual Profile]** väljer **[!UICONTROL Consents and Preferences]**. Här kan du se alternativen för **[!UICONTROL Data Collection]** och **[!UICONTROL Share Data]**.

![](./images/opt-outs/consents.png)

Börja med att välja **[!UICONTROL Data Collection]** kategori och dra sedan **[!UICONTROL Choice Value]** i segmentbyggaren. När du lägger till attributet i segmentdefinitionen kan du ange [medgivandevärden](../xdm/field-groups/profile/consents.md#choice-values) som måste inkluderas eller uteslutas.

![](./images/opt-outs/consent-values.png)

Ett sätt är att utesluta kunder som har valt att inte låta sina data samlas in. Om du vill göra det ställer du in operatorn på **[!UICONTROL does not equal]** och välj följande värden:

* **[!UICONTROL No (opt-out)]**
* **[!UICONTROL Default of No (opt-out)]**
* **[!UICONTROL Unknown]** (om samtycke antas utebli om inte annat är känt)

![](./images/opt-outs/collect.png)

Under **[!UICONTROL Attributes]** i den vänstra listen, gå tillbaka till **[!UICONTROL Consents and Preferences]** väljer du **[!UICONTROL Share Data]**. Dra i motsvarande **[!UICONTROL Choice Value]** på arbetsytan och välj samma värden som för [!UICONTROL Data Collection] alternativvärde. Se till att **[!UICONTROL Or]** förhållandet mellan de två attributen har fastställts.

![](./images/opt-outs/share.png)

Med båda **[!UICONTROL Data Collection]** och **[!UICONTROL Share Data]** Medgivandevärden som läggs till i segmentdefinitionen, kommer alla kunder som har valt att inte använda sina data att uteslutas från den slutliga målgruppen. Här kan du fortsätta att anpassa segmentdefinitionen innan du väljer **[!UICONTROL Save]** för att slutföra processen.

## Nästa steg

Genom att följa den här självstudiekursen bör du nu få en bättre förståelse för hur du respekterar kundens samtycke och önskemål när du skapar segmentdefinitioner i Experience Platform.

Mer information om att hantera samtycke i Platform finns i följande dokumentation:

* [Samtyckesbearbetning med Adobe-standard](../landing/governance-privacy-security/consent/adobe/overview.md)
* [Samtyckesbearbetning med IAB TCF 2.0-standarden](../landing/governance-privacy-security/consent/iab/overview.md)