---
title: Twitter-anslutning för anpassade målgrupper
description: Rikta er till era befintliga följare och kunder på Twitter och skapa relevanta återmarknadsföringskampanjer genom att aktivera era målgrupper som skapats i Adobe Experience Platform
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: ba9b59a24079b61a0f5d6076f3acfd83fc8f4092
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 1%

---

# [!DNL Twitter Custom Audiences]-anslutning

## Översikt {#overview}

Rikta er till era befintliga följare och kunder på Twitter och skapa relevanta återmarknadsföringskampanjer genom att aktivera era målgrupper som skapats inom Adobe Experience Platform.

## Förhandskrav {#prerequisites}

Innan du konfigurerar ditt [!DNL Twitter Custom Audiences]-mål bör du kontrollera följande Twitter-krav som du måste uppfylla.

1. Ditt [!DNL Twitter Ads]-konto måste kunna annonseras. Nya [!DNL Twitter Ads]-konton är inte berättigade till reklam under de första två veckorna efter att de har skapats.
2. Ditt Twitter-användarkonto som du har auktoriserat åtkomst för i [!DNL Twitter Audience Manager] måste ha behörigheten *[!DNL Partner Audience Manager]* aktiverad.

## Identiteter som stöds {#supported-identities}

[!DNL Twitter Custom Audiences] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Google Advertising ID (GAID) och Apple ID for Advertisers (IDFA) stöds i Adobe Experience Platform. Mappa dessa namnutrymmen och/eller attribut från källschemat i [mappningssteget](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) i arbetsflödet för målaktivering. |
| e-post | E-postadress(er) för användaren | Mappa dina e-postadresser med oformaterad text och dina SHA256-hash-adresser till det här fältet. Om källfältet innehåller ohashade attribut bör du kontrollera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Platform] automatiskt hash-kodar data vid aktiveringen. Om du hash-kodar dina kunders e-postadresser innan du överför dem till Adobe Experience Platform måste dessa identiteter hash-kodas med SHA256, utan något salt-värde. |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med de identifierare som används i Twitters anpassade målgrupper. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL Twitter Custom Audiences] finns det exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda det här målet.

### Användningsfall 1

Rikta in er befintliga följare och kunder på Twitter och skapa relevanta återmarknadsföringskampanjer genom att aktivera era målgrupper som skapats i Adobe Experience Platform som [!DNL List Custom Audiences] i Twitter.

## Anslut till mål {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

1. Hitta [!DNL Twitter Custom Audiences]-målet i målkatalogen och välj **[!UICONTROL Set Up]**.
2. Välj **[!UICONTROL Connect to destination]**.
   ![Autentisera till LinkedIn](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. Ange dina Twitter-inloggningsuppgifter och välj **Logga in**.

### Fyll i målinformation {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="Konto-ID"
>abstract="Ditt Twitter Ads-konto-ID. Detta finns i dina Twitter-annonsinställningar."

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: Ditt konto-ID för [!DNL Twitter Ads]. Detta finns i dina [!DNL Twitter Ads]-inställningar.

>[!IMPORTANT]
>
>Använd inte specialtecken (+ &amp; , % : ; @ / = ? $ \n) i namn på målgrupper, beskrivning och målgruppsmappning. Om målgruppsnamnet i Experience Platform innehåller dessa tecken tar du bort dem innan du mappar målgruppen till ett Twitter-mål.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att direktuppspela målgruppsexportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappningsöverväganden {#mapping-considerations}

När du mappar målgrupper till Twitter ska du ge målgruppsmappningsnamn som kan läsas av människor. Vi rekommenderar att du använder samma namn som du använde för Experience Platform-segmenten.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Datastyrningsöversikten](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Ytterligare resurser {#additional-resources}

Mer information om [!DNL List Custom Audiences] i Twitter finns i [Twitter-dokumentationen](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
