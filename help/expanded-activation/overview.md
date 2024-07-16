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

Med Audience Manager Expanded Activation (Adobe Experience Platform) kan befintliga [Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/aam-home)-användare aktivera sina målgrupper på målplattformarna [social](../destinations/catalog/social/overview.md) och [annonsering](../destinations/catalog/advertising/overview.md) från Real-Time CDP, till exempel [Facebook](../destinations/catalog/social/facebook.md), [Google Ads](../destinations/catalog/advertising/google-ads-destination.md) .

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation] är bara tillgängligt för befintliga [!DNL Audience Manager]-användare.

## Terminologi {#terminology}

Audience Manager Expanded Activation (Aktivering) använder koncept och komponenter från Adobe Experience Platform. Om du vill förstå det utökade aktiveringsarbetsflödet och vilka komponenter du ska använda, måste du ha en grundläggande förståelse för följande koncept:

* [Målgrupper](../segmentation/ui/overview.md): Målgrupper är uppsättningar personer som delar liknande beteenden och/eller egenskaper. Den här mängden personer kan antingen genereras av Adobe Experience Platform med segmentdefinitioner eller målgruppskomposition (plattformsgenererad publik) eller från externa källor som anpassade uppladdningar (externt genererade målgrupper). I Utökad aktivering importeras dina Audience Manager-segment (målgrupper) som [anpassade överföringar](../segmentation/ui/audience-portal.md#import-audience).
* [Source-anslutningar](../sources/home.md): Source-anslutningar (kallas även källor) hjälper Experience Platform-användare att enkelt importera data från flera källor, vilket möjliggör strukturering, märkning och förbättring av data med hjälp av Experience Platform-tjänster. Data kan hämtas från en mängd olika källor som molnbaserad lagring, tredjepartsprogramvara och CRM-system.
* [Målanslutningar](../destinations/home.md): Målen beskriver alla slutpunkter, till exempel ett Adobe-program, en annonsplattform, molnlagringstjänst eller marknadsföringstjänst, där en målgrupp aktiveras och levereras. [!DNL Expanded Activation] har stöd för aktivering av målgrupper för [annonser](../destinations/catalog/advertising/overview.md) och [sociala](../destinations/catalog/social/overview.md) målanslutningar.

## Förhandskrav {#prerequisites}

Innan du kan aktivera målgrupper med hjälp av Expanded Activation (Utökad aktivering) måste du kontrollera att du uppfyller de krav som beskrivs nedan.

### Krav för användare och roll {#permission-requirements}

Innan du kan använda [!DNL Expanded Activation] måste du skapa ett användarkonto från Admin Console och tilldela det till rollen [!DNL Expanded Activation]. På sidan [administration](administration.md) finns detaljerade anvisningar om hur du gör detta.

### Målgruppskrav {#audience-requirements}

Om du vill aktivera målgrupper via [!DNL Expanded Activation] kontrollerar du att dina Audience Manager-målgrupper baseras på **hashade e-postadresser**. Det finns två sätt att säkerställa detta, baserat på hur du använder Audience Manager:

* Om du använder funktionen [Audience Manager personbaserade destinationer](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview), infogar du redan hash-kodade e-postadresser i Audience Manager. I det här fallet behöver du inte göra något mer. Du kan hoppa till [aktivering av målgrupper via utökad aktivering](activate-audiences.md).
* Om du _inte_ använder funktionen [Audience Manager personbaserade mål](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) måste du skapa en ny datakälla i Audience Manager och använda den för att lagra hash-kodade e-postadresser. Mer information om hur du gör detta finns i dokumentationen om [hur du konfigurerar en datakälla för hash-kodade e-postarbetsflöden](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails). När du har infogat hash-kodade e-postadresser i Audience Manager-datakällan kan du läsa dokumentationen om [aktivering av målgrupper med utökad aktivering](activate-audiences.md).

## Nästa steg {#next-steps}

Nu när du får en bättre förståelse för användningsexempel och fördelar med att använda [!DNL Expanded Activation] kan du börja med att [konfigurera ditt konto](administration.md) och sedan [aktivera dina målgrupper](activate-audiences.md).
