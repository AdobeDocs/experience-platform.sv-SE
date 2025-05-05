---
keywords: Reklam.
title: Microsoft Bing-anslutning
description: Med anslutningsmålet Microsoft Bing kan ni genomföra återannonsering och riktade digitala kampanjer för målgrupper i hela Microsoft Advertising-nätverket, inklusive webbannonsering, sökannonsering och inbyggt webbmaterial.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 1%

---

# [!DNL Microsoft Bing]-anslutning {#bing-destination}

## Översikt {#overview}

Använd målet [!DNL Microsoft Bing] för att skicka profildata till hela [!DNL Microsoft Advertising Network], inklusive [!DNL Display Advertising], [!DNL Search] och [!DNL Native].

[!DNL Microsoft Bing]-målet skapar *[!DNL Custom Audiences]* i Microsoft. Dessa finns tillgängliga både i [!DNL Microsoft Search Network] och [!DNL Audience Network] ([!DNL Native] /[!DNL Display] /[!DNL Programmatic]) enligt [Microsoft Advertising-dokumentationen](https://help.ads.microsoft.com/#apex/ads/en/56892/1-500).

Om du vill skicka profildata till [!DNL Microsoft Bing] måste du först ansluta till målet.

## Användningsfall {#use-cases}

Som marknadsförare vill jag kunna använda målgrupper som är inbyggda i [!DNL Microsoft Advertising IDs] för att rikta in användare via displayannonsering eller sökannonsering i alla [!DNL Microsoft Advertising] kanaler.

## Identiteter som stöds {#supported-identities}

[!DNL Microsoft Bing] stöder aktivering av målgrupper baserat på de identiteter som visas i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Identitet | Beskrivning |
|---|---|
| MAID | MICROSOFT ADVERTISING ID |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

**[!DNL Audience Export]** - du exporterar alla medlemmar i en publik till [!DNL Microsoft Bing]-målet.

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en publik till målet [!DNL Microsoft Bing]. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Förhandskrav {#prerequisites}

>[!IMPORTANT]
>
>Om du vill skapa ditt första mål med [!DNL Microsoft Bing] och inte har aktiverat funktionen [ID-synkronisering](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=sv-SE) i Experience Cloud ID Service tidigare (med Adobe Audience Manager eller andra program) ber vi dig kontakta Adobe Consulting eller Kundtjänst för att aktivera ID-synkronisering. Om du tidigare har konfigurerat [!DNL Microsoft Bing]-integreringar i Audience Manager överförs de ID-synkroniseringar du har konfigurerat till Experience Platform.

När du konfigurerar målet måste du ange följande information:

* [!UICONTROL Account ID]: det här är din [!DNL Bing Ads CID], i heltalsformat.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md).

### Fyll i målinformation {#parameters}

När [konfigurerar](../../ui/connect-destination.md) för det här målet måste du ange följande information:

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: Din [!DNL Bing Ads Customer ID] (CID). Ditt CID är ett heltal som finns i URL:en när du loggar in på [!DNL Microsoft Advertising].

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="Mappnings-ID"
>abstract="Ange det numeriska Bing-målgrupps-ID som du vill mappa det markerade segmentet till. Om den angivna [!UICONTROL Mapping ID] inte motsvarar ett målgrupps-ID i Bing-målet, kommer du inte att se förväntade målgruppsdata i ditt Bing-konto."

>[!IMPORTANT]
> 
>För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Se [Aktivera målgruppsdata för att direktuppspela målgruppsexportmål](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

I steget [Målgruppsschema](../../ui/activate-segment-streaming-destinations.md#scheduling) måste du manuellt mappa målgruppsnamnet i fältet [!UICONTROL Mapping ID]. Detta garanterar att målgruppsmetadata skickas korrekt till [!DNL Bing].

![Gränssnittsbild som visar målgruppsfönstret med ett exempel på hur målgruppsnamnet mappas till Bing Mapping-ID.](../../assets/catalog/advertising/bing/mapping-id.png)

## Exporterade data {#exported-data}

Kontrollera ditt [!DNL Microsoft Bing Ads]-konto om du vill verifiera om data har exporterats till målet [!DNL Microsoft Bing]. Om aktiveringen lyckades fylls målgrupperna i ditt konto.
