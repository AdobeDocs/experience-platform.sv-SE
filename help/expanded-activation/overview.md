---
title: Audience Manager utökad aktivering
description: Lär dig hur du kan aktivera Audience Manager-målgrupper för sociala medier och annonser via Audience Manager Expanded Activation (aktivering).
exl-id: 1f209578-a688-40b8-8f13-dab0d4380b3b
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# Audience Manager utökad aktivering

Audience Manager Expanded Activation bygger på Adobe Experience Platform och hjälper befintliga [Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/aam-home) användare aktivera sina målgrupper för [social](../destinations/catalog/social/overview.md) och [reklam](../destinations/catalog/advertising/overview.md) målplattformar från Real-Time CDP, till exempel [Facebook](../destinations/catalog/social/facebook.md), [Google Ads](../destinations/catalog/advertising/google-ads-destination.md), med mera.

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation] är bara tillgängligt för befintliga [!DNL Audience Manager] -användare.

## Terminologi {#terminology}

Audience Manager Expanded Activation (Aktivering) använder koncept och komponenter från Adobe Experience Platform. Om du vill förstå det utökade aktiveringsarbetsflödet och vilka komponenter du ska använda, måste du ha en grundläggande förståelse för följande koncept:

* [Målgrupper](../segmentation/ui/overview.md): Målgrupper är grupper med människor som har liknande beteenden och/eller egenskaper. Den här mängden personer kan antingen genereras av Adobe Experience Platform med segmentdefinitioner eller målgruppskomposition (plattformsgenererad publik) eller från externa källor som anpassade uppladdningar (externt genererade målgrupper). I den utökade aktiveringen importeras era Audience Manager-segment (målgrupper) som [anpassade överföringar](../segmentation/ui/audience-portal.md#import-audience).
* [Source-anslutningar](../sources/home.md): Source-kopplingar (kallas även källor) hjälper Experience Platform att enkelt importera data från flera källor, vilket möjliggör strukturering, märkning och förbättring av data med hjälp av Experience Platform-tjänster. Data kan hämtas från en mängd olika källor som molnbaserad lagring, tredjepartsprogramvara och CRM-system.
* [Målanslutningar](../destinations/home.md): Målen beskriver alla slutpunkter, till exempel Adobe, annonsplattform, molnlagringstjänst eller marknadsföringstjänst, där en målgrupp aktiveras och levereras. [!DNL Expanded Activation] stöder aktivering av målgrupper för [reklam](../destinations/catalog/advertising/overview.md) och [social](../destinations/catalog/social/overview.md) målanslutningar.

## Förhandskrav {#prerequisites}

Innan du kan aktivera målgrupper med hjälp av Expanded Activation (Utökad aktivering) måste du kontrollera att du uppfyller de krav som beskrivs nedan.

### Krav för användare och roll {#permission-requirements}

Innan du kan använda [!DNL Expanded Activation]måste du skapa ett användarkonto från Admin Console och tilldela det till [!DNL Expanded Activation] roll. Se [administration](administration.md) sida med detaljerade anvisningar om hur du gör detta.

### Målgruppskrav {#audience-requirements}

Aktivera målgrupper genom [!DNL Expanded Activation], se till att era Audience Manager-målgrupper är baserade på **hash-kodade e-postadresser**. Det finns två sätt att säkerställa detta, baserat på hur du använder Audience Manager:

* Om du använder [Audience Manager personbaserade destinationer](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) så har du redan inhämtat hashade e-postadresser i Audience Manager. I det här fallet behöver du inte göra något mer. Du kan hoppa till [aktivera målgrupper genom utökad aktivering](activate-audiences.md).
* Om du _not_ med [Audience Manager personbaserade destinationer](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) måste du skapa en ny datakälla i Audience Manager och använda den för att lagra hashade e-postadresser. Läs dokumentationen om [konfigurera en datakälla för arbetsflöden för hashad e-post](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails) för att lära sig hur man gör detta. När du har infogat hash-kodade e-postadresser i Audience Manager-datakällan kan du läsa dokumentationen om [aktivera målgrupper genom utökad aktivering](activate-audiences.md).

## Nästa steg {#next-steps}

Nu när du har fått en bättre förståelse för användningsexempel och fördelar med att använda [!DNL Expanded Activation], start [konfigurera ditt konto](administration.md) och sedan [aktivera era målgrupper](activate-audiences.md).
