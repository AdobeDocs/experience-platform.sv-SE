---
keywords: facebook extensions;facebook extension;facebook destinations;facebook;instagram;messenger;facebook messenger
title: Facebook-mål
seo-title: Facebook-mål
description: Aktivera profiler för era Facebook-kampanjer för målgruppsanpassning, personalisering och nedtryckning baserat på hashad-e-post.
seo-description: Aktivera profiler för era Facebook-kampanjer för målgruppsanpassning, personalisering och nedtryckning baserat på hashad-e-post.
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 4%

---


# [!DNL Facebook] Destination

## Översikt {#overview}

Aktivera profiler för era [!DNL Facebook] kampanjer för målgruppsanpassning, personalisering och nedtryckning baserat på hashad-e-post.

Du kan använda den här målgruppen för målgruppsanpassning i olika appar som stöds av [!DNL Facebook’s] , inklusive [!DNL Custom Audiences], [!DNL Facebook]och [!DNL Instagram][!DNL Audience Network] [!DNL Messenger]. Det program som ni valt att köra kampanjen mot anges av placeringsnivån i [!DNL Facebook Ads Manager].

![Facebook-mål i CDP-gränssnittet i realtid](/help/rtcdp/destinations/assets/facebook-destination.png)


## Användningsexempel

För att du bättre ska förstå hur och när du ska använda [!DNL Facebook] målet finns det två exempel på användningsområden som kunder med kunddataplattform i realtid kan lösa genom att använda den här funktionen.


### Användningsfall 1


En webbutik vill nå befintliga kunder via sociala plattformar och visa dem personaliserade erbjudanden baserat på deras tidigare order. Onlinebutiken kan importera e-postadresser från sin egen CRM till Adobe CDP i realtid, bygga segment utifrån sina egna offlinedata och skicka dessa segment till den [!DNL Facebook] sociala plattformen för att optimera annonsutgifterna.


### Användningsfall nr 2


Ett flygbolag har olika kundnivåer (Bronze, Silver och Gold) och vill kunna erbjuda varje nivå personaliserade erbjudanden via sociala plattformar. Alla kunder använder dock inte flygbolagets mobilapp, och vissa av dem har inte loggat in på företagets webbplats. De enda identifierare företaget har för dessa kunder är medlems-ID och e-postadresser.

För att rikta in sig på dem i olika sociala medier kan de lägga in kunddata från sina CRM i CDP i realtid i Adobe, med e-postadresserna som identifierare.

Därefter kan de använda sina offlinedata, inklusive tillhörande medlemskaps-ID:n och kundnivåer, för att skapa nya målgruppssegment som de kan rikta sig mot via [!DNL Facebook] målet.

## Destinationsspecifikationer {#destination-specs}

### Datastyrning för [!DNL Facebook] destinationer {#data-governance}

>[!IMPORTANT]
>
>Data som skickas till [!DNL Facebook] ska inte innehålla sammanfogade identiteter. Du ansvarar för att uppfylla denna skyldighet och kan göra det genom att se till att segment som markerats för aktivering inte använder ett sammanslagningsalternativ i sammanfogningspolicyn. Läs mer om [sammanfogningsprinciper](/help/profile/ui/merge-policies.md).

### Exporttyp {#export-type}

**Segmentexport** - du exporterar alla medlemmar i ett segment (publik) med identifierarna (namn, telefonnummer osv.) används i Facebook-målet.

### Krav för Facebook-konto {#facebook-account-prerequisites}

Innan du kan skicka målgruppssegment till [!DNL Facebook]kontrollerar du att du uppfyller följande krav:

1. Ditt [!DNL Facebook] användarkonto måste ha **[!DNL Manage campaigns]** behörighet aktiverat för annonskontot som du tänker använda.
2. Add the **Adobe Experience Cloud** business account as an advertising partner in your [!DNL Facebook Ad Account]. Använd `business ID=206617933627973`. Mer information finns i [Lägg till partner i din Business Manager](https://www.facebook.com/business/help/1717412048538897) i dokumentationen för Facebook.
   >[!IMPORTANT]
   >
   > When configuring the permissions for Adobe Experience Cloud, you must enable the **Manage campaigns** permission. Det krävs för [!DNL Adobe Real-time CDP]-integreringen.
3. Läs och signera [!DNL Facebook Custom Audiences] användarvillkoren. Gör det genom att gå till `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, där `accountID` är din [!DNL Facebook Ad Account ID].

### Krav för e-posthashning {#email-hashing-requirements}

[!DNL Facebook] kräver att ingen personligt identifierbar information (PII) skickas klart. Därför måste de målgrupper som aktiverats för [!DNL Facebook] kapas av *hash-* e-postadresser. Du kan välja att hash-koda e-postadresser innan du importerar dem till Adobe Experience Platform, eller så kan du välja att arbeta med e-postadresser i klartext i Experience Platform och låta algoritmen hash-koda dem när de aktiveras.

Om du vill veta mer om hur du kan importera e-postadresser i Experience Platform kan du läsa översikten över [](/help/ingestion/batch-ingestion/overview.md) batchimporten och översikten över [det](/help/ingestion/streaming-ingestion/overview.md)vanligaste inmatningsproblemet.

Om du väljer att hash-koda e-postadresserna själv måste du se till att uppfylla följande krav:

* Trimma alla inledande och avslutande blanksteg från e-poststrängen. exempel: `johndoe@example.com`, inte `<space>johndoe@example.com<space>`;
* När du hash-kodar e-poststrängarna ska du se till att hash-koda den gemena strängen.
   * Exempel: `example@email.com`, inte `EXAMPLE@EMAIL.COM`;
* Kontrollera att den hash-kodade strängen är i gemener
   * Exempel: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, inte `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Salt inte strängen.


>[!IMPORTANT]
>
>Om du väljer att inte hash-koda e-postadresser gör Adobe Real-time CDP det åt dig när du aktiverar segment till [!DNL Facebook]. I [aktiveringsarbetsflödet](/help/rtcdp/destinations/activate-destinations.md#activate-data) (se steg 5) väljer du det `Email` alternativ som visas nedan för *obearbetade e-postadresser* och `Email_LC_SHA256` för *hashade e-postadresser*.


![Hindrar vid aktivering](/help/rtcdp/destinations/assets/identity-mapping.png)

## Anslut till mål {#connect-destination}

Mer information om hur du ansluter till [!DNL Facebook] målet finns i autentiseringsarbetsflöde [för mål för](/help/rtcdp/destinations/social-network-destinations-workflow.md)sociala nätverk.


## Aktivera segment för att [!DNL Facebook] {#activate-segments}

Instruktioner om hur du aktiverar segment [!DNL Facebook]finns i [Aktivera data till mål](/help/rtcdp/destinations/activate-destinations.md).

## Exporterade data {#exported-data}

En lyckad aktivering [!DNL Facebook]innebär att en [!DNL Facebook] anpassad målgrupp skapas i [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segmentmedlemskap i målgruppen skulle läggas till och tas bort eftersom användarna är kvalificerade eller diskvalificerade för de aktiverade segmenten.

>[!TIP]
>
>Integrationen mellan CDP i realtid i Adobe och [!DNL Facebook] stöder historiska efterfyllningar. Alla historiska segmentkvalifikationer skickas till [!DNL Facebook] när du aktiverar segmenten till målet.