---
title: Twitter Custom Auditions connection
description: Rikta er till era befintliga följare och kunder i Twitter och skapa relevanta återmarknadsföringskampanjer genom att aktivera era målgrupper som skapats i Adobe Experience Platform
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '781'
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

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segment export]** | Du exporterar alla medlemmar i ett segment (publik) med de identifierare som används i Twitter Custom Audiences-målet. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

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

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera profiler och segment för att direktuppspela segmentexportmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Ytterligare resurser {#additional-resources}

När du mappar målgruppssegment till Twitter måste du se till att följande krav för namngivning av segment uppfylls:

1. Ge segmentmappningsnamn som kan läsas av människor. Vi rekommenderar att du använder samma namn som du använde för Experience Platform-segmenten.
2. Använd inte specialtecken (+ &amp; , % : ; @ / = ? $) i namn på segmentmappning och segmentmappning. Om Experience Platform-segmentnamnet innehåller dessa tecken tar du bort dem innan du mappar segmentet till ett Twitter-mål.

Mer information om [!DNL List Custom Audiences] i Twitter finns i [Twitter-dokumentation](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
