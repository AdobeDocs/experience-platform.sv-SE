---
title: Twitter Custom Auditions connection
description: Rikta er till era befintliga följare och kunder i Twitter och skapa relevanta återmarknadsföringskampanjer genom att aktivera era målgrupper som skapats i Adobe Experience Platform
source-git-commit: 3ea3f9ed156ba3a1fbc790153a4b8fa193d5e2da
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 1%

---


# [!DNL Twitter Custom Audiences] anslutning

## Översikt {#overview}

Rikta er till era befintliga följare och kunder i Twitter och skapa relevanta återmarknadsföringskampanjer genom att aktivera era målgrupper som skapats inom Adobe Experience Platform.

## Förutsättningar {#prerequisites}

Innan du konfigurerar ditt [!DNL Twitter Custom Audiences]-mål bör du kontrollera att du uppfyller följande krav för Twitter.

1. Ditt [!DNL Twitter Ads]-konto måste kunna annonseras. Nya [!DNL Twitter Ads]-konton är inte berättigade till reklam under de första två veckorna efter att de har skapats.
2. Ditt Twitter-användarkonto som du har auktoriserat åtkomst för i [!DNL Twitter Audience Manager] måste ha behörigheten *[!DNL Partner Audience Manager]* aktiverad.


## Identiteter som stöds {#supported-identities}

[!DNL Twitter Custom Audiences] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Google Advertising ID (GAID) och Apple ID for Advertisers (IDFA) stöds i Adobe Experience Platform. Mappa dessa namnutrymmen och/eller attribut från källschemat i [mappningssteget](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) i målaktiveringsarbetsflödet. |
| e-post | E-postadress(er) för användaren | Mappa dina e-postadresser med oformaterad text och dina SHA256-hashed-e-postadresser till det här fältet. När källfältet innehåller ohashade attribut bör du markera alternativet **[!UICONTROL Apply transformation]** så att [!DNL Platform] automatiskt hash-kodar data vid aktiveringen. Om du hash-kodar dina kunders e-postadresser innan du överför dem till Adobe Experience Platform måste dessa identiteter hash-kodas med SHA256, utan något salt. |

{style=&quot;table-layout:auto&quot;}

## Exporttyp {#export-type}

**Segmentexport**  - du exporterar alla medlemmar i ett segment (publik) med de identifierare som används i Twitter Custom Audiences-målet.

## Användningsexempel {#use-cases}

För att du bättre ska förstå hur och när du ska använda målet [!DNL Twitter Custom Audiences] finns det exempel på användningsområden som Adobe Experience Platform-kunder kan lösa genom att använda det här målet.

### Användningsfall 1

Rikta er till era befintliga följare och kunder i Twitter och skapa relevanta marknadsföringskampanjer genom att aktivera era målgrupper som skapats inom Adobe Experience Platform som [!DNL List Custom Audiences] i Twitter.

## Anslut till mål {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för målkonfiguration](../../ui/connect-destination.md).

### Anslutningsparametrar {#parameters}

När du [konfigurerar](../../ui/connect-destination.md) det här målet måste du ange följande information:

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Account ID]**: Ditt  [!DNL Twitter Ads] konto-ID. Detta finns i dina [!DNL Twitter Ads]-inställningar.

## Aktivera segment till den här destinationen {#activate}

Läs [Aktivera profiler och segment för att direktuppspela segmentets exportmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] framtvingar datastyrning finns i [Datastyrningsöversikten](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Ytterligare resurser {#additional-resources}

När du mappar målgruppssegment till Twitter måste du se till att följande krav för namngivning av segment uppfylls:

1. Ge segmentmappningsnamn som kan läsas av människor. Vi rekommenderar att du använder samma namn som du använde för Experience Platform-segmenten.
2. Använd inte specialtecken (+ &amp; , % : ; @ / = ? $) i namn på segmentmappning och segmentmappning. Om Experience Platform-segmentnamnet innehåller dessa tecken tar du bort dem innan du mappar segmentet till ett Twitter-mål.

Mer information om [!DNL List Custom Audiences] i Twitter finns i [Twitter-dokumentationen](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).