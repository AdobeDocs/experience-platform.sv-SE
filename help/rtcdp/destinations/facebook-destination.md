---
title: Facebook-mål
seo-title: Facebook-mål
description: Aktivera profiler för era Facebook-kampanjer för målgruppsanpassning, personalisering och nedtryckning baserat på hashad-e-post.
seo-description: Aktivera profiler för era Facebook-kampanjer för målgruppsanpassning, personalisering och nedtryckning baserat på hashad-e-post.
translation-type: tm+mt
source-git-commit: 522014f8e5f3de0f553a69763d3a37482953b7c4
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---


# Facebook-mål

## Översikt {#overview}

Aktivera profiler för era Facebook-kampanjer för målgruppsanpassning, personalisering och nedtryckning baserat på hashad-e-post.

![Facebook-mål i CDP-gränssnittet i realtid](/help/rtcdp/destinations/assets/facebook-destination.png)

## Användningsexempel

För att du bättre ska förstå hur och när du ska använda Facebook-destinationen finns det två exempel på användningsområden som kunder med Adobes kunddataplattform i realtid kan lösa genom att använda den här funktionen.


### Användningsfall 1


En webbutik vill nå befintliga kunder via sociala plattformar och visa dem personaliserade erbjudanden baserat på deras tidigare order. Onlinebutiken kan importera e-postadresser från sin egen CRM till Adobe CDP i realtid, bygga segment utifrån sina egna offlinedata och skicka dessa segment till den sociala Facebook-plattformen för att optimera annonsutgifterna.


### Användningsfall nr 2


Ett flygbolag har olika kundnivåer (Bronze, Silver och Gold) och vill kunna erbjuda varje nivå personaliserade erbjudanden via sociala plattformar. Alla kunder använder dock inte flygbolagets mobilapp, och vissa av dem har inte loggat in på företagets webbplats. De enda identifierare företaget har för dessa kunder är medlems-ID och e-postadresser.
För att rikta in dem på sociala medier kan de lägga in kunddata från sina CRM i Adobe CDP i realtid, med hjälp av hash-kodade e-postadresser som identifierare.
Sedan kan de kombinera sina offlinedata med sina befintliga onlineaktivitetsdata för att skapa nya målgruppssegment som de kan rikta sig mot via Facebook-målet.

## Destinationsspecifikationer {#destination-specs}

### Datastyrning för Facebook-destinationer {#data-governance}

>[!IMPORTANT]
>
>Data som skickas till Facebook får inte innehålla sammanfogade identiteter. Du ansvarar för att uppfylla denna skyldighet och kan göra det genom att se till att segment som markerats för aktivering inte använder ett sammanslagningsalternativ i sammanfogningspolicyn. Läs mer om [sammanfogningsprinciper](/help/profile/ui/merge-policies.md).

### Aktiveringstyp {#activation-type}

**Segmentexport** - du exporterar alla medlemmar i ett segment (publik) med identifierarna (namn, telefonnummer osv.) används i Facebook-målet.

### Krav för Facebook-konto {#facebook-account-prerequisites}

Innan du kan skicka målgruppssegment till [!DNL Facebook]kontrollerar du att du uppfyller följande krav:

1. Ditt [!DNL Facebook] användarkonto måste ha **[!DNL Manage campaigns]** behörighet aktiverat för annonskontot som du tänker använda.
2. Lägg till **Adobe Experience Cloud** -företagskontot som annonspartner i ert [!DNL Facebook Ad Account]företag. Använd `business ID=206617933627973`. Mer information finns i [Lägg till partner i din Business Manager](https://www.facebook.com/business/help/1717412048538897) i dokumentationen för Facebook.
   >[!IMPORTANT]
   > När du konfigurerar behörigheter för Adobe Experience Cloud måste du aktivera behörigheten **Hantera kampanjer** . Detta krävs för [!DNL Adobe Real-time CDP] integreringen.
3. Läs och signera [!DNL Facebook Custom Audiences] användarvillkoren. För att göra detta, gå till `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, var `accountID` är din [!DNL Facebook Ad Account ID].

### Krav för e-posthashning {#email-hashing-requirements}

Facebook kräver att ingen personligt identifierbar information skickas ut. Därför måste de målgrupper som aktiveras för Facebook vara avstängda från *hashade* e-postadresser. Du kan välja att hash-koda e-postadresser innan du importerar dem till Adobe Experience Platform, eller så kan du välja att arbeta med e-postadresser som är tydliga i Experience Platform och låta vår algoritm hash-koda dem när de aktiveras.

Om du vill veta mer om hur du kan importera e-postadresser i Experience Platform kan du läsa översikten över [](/help/ingestion/batch-ingestion/overview.md) gruppimporten och översikten över [det](/help/ingestion/streaming-ingestion/overview.md)strömmande intrycket.

Om du väljer att hash-koda e-postadresserna själv måste du se till att uppfylla följande krav:

* Trimma alla inledande och avslutande blanksteg från e-poststrängen. exempel: `johndoe@example.com`, inte `<space>johndoe@example.com<space>`;
* När du hash-kodar e-poststrängarna ska du se till att hash-koda den gemena strängen.
   * Exempel: `example@email.com`, inte `EXAMPLE@EMAIL.COM`;
* Kontrollera att den hash-kodade strängen är i gemener
   * Exempel: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, inte `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Salt inte strängen.


>[!IMPORTANT]
>
>Om du väljer att inte hash-koda e-postadresser gör Adobe CDP det åt dig i realtid när du aktiverar segment till Facebook. I [aktiveringsarbetsflödet](/help/rtcdp/destinations/activate-destinations.md#activate-data) (se steg 5) väljer du det `Email` alternativ som visas nedan för *obearbetade e-postadresser* och `Email_LC_SHA256` för *hashade e-postadresser*.


![Hindrar vid aktivering](/help/rtcdp/destinations/assets/identity-mapping.png)

## Anslut till mål {#connect-destination}

Mer information om hur du ansluter till Facebook-målet finns i [autentiseringsarbetsflöde](/help/rtcdp/destinations/social-network-destinations-workflow.md)för mål för sociala nätverk.


## Aktivera segment till Facebook {#activate-segments}

Instruktioner om hur du aktiverar segment till Facebook finns i [Aktivera data till mål](/help/rtcdp/destinations/activate-destinations.md).