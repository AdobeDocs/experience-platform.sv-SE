---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Utvecklarhandbok för kundprofil-API i realtid
topic: guide
translation-type: tm+mt
source-git-commit: d0ccaa5511375253a2eca8f1235c2f953b734709

---


# Utvecklarhandbok för kundprofil-API i realtid

Med kundprofilen i realtid kan ni se en helhetsbild av var och en av era enskilda kunder i Adobe Experience Platform. Med en profil kan ni sammanställa olika kunddata från flera olika kanaler, t.ex. online-, offline-, CRM- och tredjepartsdata, i en enhetlig vy med ett användbart tidsstämplat konto för varje kundinteraktion.

## Getting started {#getting-started}

Med hjälp av API:t för kundprofil i realtid kan du utföra grundläggande CRUD-åtgärder mot profilresurser, som att konfigurera beräknade attribut, komma åt enheter, exportera profildata och ta bort onödiga datauppsättningar eller batchar.

Om du vill använda den här utvecklarhandboken måste du ha en fungerande förståelse för de olika Adobe Experience Platform-tjänster som används i arbetet med profildata. Innan du börjar arbeta med kundprofils-API:t i realtid bör du läsa dokumentationen för följande tjänster:

* [Kundprofil](../home.md)i realtid: Ger en enhetlig kundprofil i realtid baserad på aggregerade data från flera källor.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Få en bättre bild av kunden och deras beteende genom att överbrygga identiteter mellan olika enheter och system.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Gör att ni kan bygga målgruppssegment utifrån kundprofildata i realtid.
* [Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.
* [Sandlådor](../../sandboxes/home.md): Experience Platform innehåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna anropa API-slutpunkter för profiler.

### Läser exempel-API-anrop

I dokumentationen för kundprofil i realtid finns exempel-API-anrop som visar hur begäranden formateras korrekt. Det kan vara sökvägar, obligatoriska rubriker och korrekt formaterade begärandenyttolaster. Ett exempel på JSON som returneras i API-svar finns också. Information om de konventioner som används i dokumentationen för exempel-API-anrop finns i avsnittet [om hur du läser exempel-API-anrop](../../landing/troubleshooting.md#how-do-i-format-an-api-request) i felsökningsguiden för Experience Platform.

### Obligatoriska rubriker

API-dokumentationen kräver också att du har slutfört [autentiseringssjälvstudiekursen](../../tutorials/authentication.md) för att kunna anropa plattformsslutpunkter. När du slutför självstudiekursen för autentisering visas värdena för var och en av de huvuden som krävs i API-anrop för Experience Platform, vilket visas nedan:

* Behörighet: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alla resurser i Experience Platform är isolerade till specifika virtuella sandlådor. Begäranden till plattforms-API:er kräver ett huvud som anger namnet på sandlådan som åtgärden ska utföras i:

* x-sandbox-name: `{SANDBOX_NAME}`

Mer information om sandlådor i plattformen finns i översiktsdokumentationen för [sandlådan](../../sandboxes/home.md).

Alla begäranden med en nyttolast i begärandetexten (som POST-, PUT- och PATCH-anrop) måste innehålla en `Content-Type` rubrik. Godkända värden som är specifika för varje anrop finns i anropsparametrarna.

## (Alfa) Beräknade attribut

>[!IMPORTANT]
>Funktionen för beräknade attribut är alfavärden och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

Med beräknade attribut kan du automatiskt beräkna fältvärden baserat på andra värden, beräkningar och uttryck. Beräknade attribut fungerar på profilnivån, vilket innebär att du kan samla värden för alla poster och händelser.

Varje beräknat attribut innehåller ett uttryck, &quot;rule&quot;, som utvärderar inkommande data och lagrar resultatvärdet i ett profilattribut eller i en händelse. Med hjälp av dessa beräkningar kan du enkelt besvara frågor som rör inköpstid, tid mellan köp eller antal programöppningar, utan att behöva utföra komplexa beräkningar manuellt varje gång informationen behövs.

Du kan skapa, visa, redigera och ta bort beräknade attribut med hjälp av `config/computedAttributes` slutpunkterna. Om du vill lära dig hur du använder dessa slutpunkter kan du gå till underhandboken för [beräknade attribut](computed-attributes.md).

## Kantprojektioner

Adobe Experience Platform möjliggör personalisering av kundupplevelser i realtid genom att göra data lättillgängliga på strategiskt placerade servrar som kallas&quot;kanter&quot;. Real-time Customer Profile API innehåller slutpunkter för att arbeta med kanter via komponenter som kallas för &quot;projektioner&quot;. Detta inkluderar projektionskonfigurationer för att bestämma vilka data som ska projiceras för varje kant, liksom projektionsdestinationer för att definiera var projektionen ska dirigeras.

Detaljerad information om hur du arbetar med kantprojektioner finns i [underhandboken](edge-projections.md)för kantprojektioner.

## Enheter

Med Adobe Experience Platform kan ni få åtkomst till kundprofildata i realtid med RESTful API:er eller användargränssnittet. Om du vill lära dig hur du får åtkomst till enheter, som ofta kallas&quot;profiler&quot;, med API:t, följer du stegen som beskrivs i underhandboken för [enheter](entities.md).

## Sammanfoga profiler

När data från flera källor samlas i Experience Platform är sammanslagningsprinciper de regler som Platform använder för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa enskilda kundprofiler.

Med hjälp av kundprofils-API:t i realtid kan du skapa nya kopplingsprofiler, hantera befintliga profiler och ange en standardkopplingsprofil för organisationen. Mer information om hur du arbetar med sammanfogningspolicyer med API:t finns i [underhandboken](merge-policies.md)för sammanfogningspolicyer.

En guide till hur du arbetar med sammanfogningsprinciper med hjälp av användargränssnittet för plattformen finns i [användarhandboken](../ui/merge-policies.md)för sammanfogningsprinciper.

## Profilsökning

Profilsökning används för att söka efter och indexera konfigurerbara fält som finns i olika datakällor och returnera dem i nära realtid. Information om hur du börjar arbeta med profilsökning finns i [sökunderhandboken](profile-search.md)

## Profilsystemjobb

Data som hämtas till Platform lagras i Data Lake samt i datalagret för kundprofiler i realtid. Ibland kan det vara nödvändigt att ta bort en datauppsättning eller en batch från profilarkivet för att ta bort data som du inte längre behöver eller som har lagts till av misstag. Detta kräver att API:t används för att skapa ett profilsystemjobb, som kallas&quot;delete request&quot;, som också kan ändras, övervakas eller tas bort om det behövs.

Om du vill lära dig hur du arbetar med borttagningsbegäranden med hjälp av `/system/jobs` slutpunkterna i kundprofils-API:t i realtid, följer du stegen som beskrivs i underguiden [för](profile-system-jobs.md)profilsystemjobb.

## Nästa steg

Om du vill börja ringa samtal med hjälp av kundprofils-API:t i realtid väljer du en av delguiderna för att lära dig hur du använder specifika profilrelaterade slutpunkter. Mer information om hur du arbetar med profildata med hjälp av plattformsgränssnittet finns i användarhandboken för [kundprofiler i realtid](../ui/user-guide.md).