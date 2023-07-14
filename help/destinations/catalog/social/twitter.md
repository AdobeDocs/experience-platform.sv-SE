---
title: Twitter Custom Auditions connection
description: Rikta er till era befintliga följare och kunder i Twitter och skapa relevanta återmarknadsföringskampanjer genom att aktivera era målgrupper som skapats i Adobe Experience Platform
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 1%

---

# [!DNL Twitter Custom Audiences] anslutning

## Översikt {#overview}

Rikta er till era befintliga följare och kunder i Twitter och skapa relevanta återmarknadsföringskampanjer genom att aktivera era målgrupper som skapats inom Adobe Experience Platform.

## Förutsättningar {#prerequisites}

Innan du konfigurerar [!DNL Twitter Custom Audiences] ska du kontrollera att du uppfyller följande krav för Twitter.

1. Dina [!DNL Twitter Ads] kontot måste vara reklamberättigat. Nytt [!DNL Twitter Ads] Konton är inte berättigade till reklam under de första två veckorna efter att de har skapats.
2. Ditt Twitter-användarkonto som du har auktoriserat åtkomst till i [!DNL Twitter Audience Manager] måste ha *[!DNL Partner Audience Manager]* behörighet aktiverad.

## Identiteter som stöds {#supported-identities}

[!DNL Twitter Custom Audiences] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Google Advertising ID (GAID) och Apple ID for Advertisers (IDFA) stöds i Adobe Experience Platform. Mappa dessa namnutrymmen och/eller attribut från källschemat i enlighet med [mappningssteg](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) av arbetsflödet för målaktivering. |
| e-post | E-postadress(er) för användaren | Mappa dina e-postadresser med oformaterad text och dina SHA256-hashed-e-postadresser till det här fältet. När källfältet innehåller ohash-kodade attribut markerar du **[!UICONTROL Apply transformation]** alternativ, att ha [!DNL Platform] automatiskt hash-koda data vid aktiveringen. Om du hash-kodar dina kunders e-postadresser innan du överför dem till Adobe Experience Platform måste dessa identiteter hash-kodas med SHA256, utan något salt. |

{style="table-layout:auto"}

## Målgrupper som stöds {#supported-audiences}

I det här avsnittet beskrivs alla målgrupper som du kan exportera till det här målet.

Alla destinationer stöder aktivering av målgrupper som genererats via Experience Platform [Segmenteringstjänst](../../../segmentation/home.md).

Dessutom stöder denna destination även aktivering av de målgrupper som beskrivs i tabellen nedan.

| Målgruppstyp | Beskrivning |
---------|----------|
| Anpassade överföringar | Målgrupper som importerats till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Du exporterar alla medlemmar i en målgrupp med de identifierare som används i Twitter Custom Audiences-målet. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Användningsexempel {#use-cases}

För att du bättre ska förstå hur och när du ska använda [!DNL Twitter Custom Audiences] mål, här är exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.

### Användningsfall 1

Rikta er till era befintliga följare och kunder i Twitter och skapa relevanta återmarknadsföringskampanjer genom att aktivera era målgrupper som skapats inom Adobe Experience Platform som [!DNL List Custom Audiences] i Twitter.

## Anslut till mål {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

1. Hitta [!DNL Twitter Custom Audiences] mål i målkatalogen och välj **[!UICONTROL Set Up]**.
2. Välj **[!UICONTROL Connect to destination]**.
   ![Autentisera till LinkedIn](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. Ange dina Twitter-uppgifter och välj **Logga in**.

### Fyll i målinformation {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="Konto-ID"
>abstract="Ditt Twitter Ads-konto-ID. Detta finns i dina Twitter Ads-inställningar."

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: Dina [!DNL Twitter Ads] konto-ID. Det finns i [!DNL Twitter Ads] inställningar.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera profiler och målgrupper för att strömma målgruppernas exportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Ytterligare resurser {#additional-resources}

När du mappar målgrupper till Twitter måste du se till att följande krav på publiknamngivning uppfylls:

1. Ge målgruppsmappningsnamn som kan läsas av människor. Vi rekommenderar att du använder samma namn som du använde för Experience Platform-segmenten.
2. Använd inte specialtecken (+ &amp; , % : ; @ / = ? $) i publikens och målgruppens mappningsnamn. Om målgruppsnamnet för Experience Platform innehåller dessa tecken tar du bort dem innan du mappar målgruppen till ett Twitter-mål.

Mer information om [!DNL List Custom Audiences] i Twitter finns i [Twitter-dokumentation](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
