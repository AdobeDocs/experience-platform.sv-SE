---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;enable profile;Enable profile
title: Utvecklarhandbok för kundprofil-API i realtid
topic: guide
description: Real-time Customer Profile API innehåller flera slutpunkter som beskrivs nedan.
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] Utvecklarhandbok för API

[!DNL Real-time Customer Profile] ger er en helhetsbild av var och en av era enskilda kunder inom Adobe Experience Platform. [!DNL Profile] kan ni sammanställa olika kunddata från olika kanaler, t.ex. online, offline, CRM och data från tredje part, i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

API:t innehåller [!DNL Real-time Customer Profile] flera slutpunkter, som beskrivs nedan. Besök de enskilda slutpunktshandböckerna för mer information och se [komma igång-guiden](getting-started.md) för viktig information om obligatoriska huvuden, läsning av exempel-API-anrop med mera.

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder går du till API-referenssaggen för kundprofiler i [realtid](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

En guide till hur du arbetar med [!DNL Real-time Customer Profile] data i [!DNL Experience Platform] användargränssnittet finns i användarhandboken [för](../ui/user-guide.md)profiler.

## (Alfa) Beräknade attribut {#computed-attributes}

>[!IMPORTANT]
>
>Funktionen för beräknade attribut är alfavärden och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

Med beräknade attribut kan du automatiskt beräkna fältvärden baserat på andra värden, beräkningar och uttryck. Beräknade attribut fungerar på profilnivån, vilket innebär att du kan samla värden över alla poster och händelser. Varje beräknat attribut innehåller ett uttryck, eller &quot;rule&quot;, som utvärderar inkommande data och lagrar resultatvärdet i ett profilattribut eller i en händelse. Med hjälp av dessa beräkningar kan du enkelt besvara frågor som rör inköpstid, tid mellan köp eller antal programöppningar, utan att behöva utföra komplexa beräkningar manuellt varje gång informationen behövs. Du kan skapa, visa, redigera och ta bort beräknade attribut med hjälp av `config/computedAttributes` slutpunkten. Om du vill lära dig hur du använder den här slutpunkten kan du gå till guiden [för](computed-attributes.md)beräknade attribut.

## Kantprojektioner {#edge-projections}

Adobe Experience Platform möjliggör personalisering av kundupplevelser i realtid genom att göra data lättillgängliga på strategiskt placerade servrar som kallas&quot;kanter&quot;. API:t innehåller slutpunkter för att arbeta med kanter via komponenter som kallas för &quot;projektioner&quot;. [!DNL Real-time Customer Profile] Detta inkluderar projektionskonfigurationer för att bestämma vilka data som ska projiceras för varje kant, liksom projektionsdestinationer för att definiera var projektionen ska dirigeras. Detaljerad information om hur du arbetar med kantprojektioner finns i guiden [för](edge-projections.md)projektionskonfigurationer och destinationspunkter.

## Enheter ([!DNL Profile] åtkomst) {#entities}

Via Adobe Experience Platform kan du komma åt [!DNL Real-time Customer Profile] data med RESTful API:er eller användargränssnittet. Om du vill lära dig hur du får åtkomst till enheter, som ofta kallas&quot;profiler&quot;, med API:t, följer du stegen som beskrivs i slutpunktshandboken för [enheter](entities.md). Mer information om hur du får åtkomst till profiler med hjälp av [!DNL Platform] användargränssnittet finns i [användarhandboken](../ui/user-guide.md)för profilen.

## Exportera jobb ([!DNL Profile] export) {#profile-export}

[!DNL Real-time Customer Profile] data kan exporteras till en datauppsättning för vidare bearbetning, som att exportera målgruppssegment för aktivering eller profilattribut för rapportering. Exportjobb för målgruppssegment är en del av [!DNL Adobe Experience Platform Segmentation Service] API:t. Läs slutpunktsguiden [för](../../profile/api/export-jobs.md) segmenteringsexportjobb om du vill veta mer. Stegvisa instruktioner om hur du skapar och hanterar exportjobb för profilattribut finns i slutpunktshandboken för [exportjobb](export-jobs.md).

## Sammanfoga profiler {#merge-policies}

När data från flera källor samlas i [!DNL Experience Platform]är sammanslagningsprinciper de regler som [!DNL Platform] använder för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa enskilda kundprofiler. Med API:t kan du skapa nya sammanfogningsprinciper, hantera befintliga profiler och ange en standardsammanfogningsprincip för organisationen. [!DNL Real-time Customer Profile] Mer information om hur du arbetar med sammanfogningspolicyer med API finns i slutpunktshandboken för [sammanfogningspolicyer](merge-policies.md).

En guide till hur du arbetar med sammanfogningsprinciper med hjälp av [!DNL Platform] användargränssnittet finns i användarhandboken för [sammanfogningsprinciper](../ui/merge-policies.md).

## Förhandsgranska exempelstatus ([!DNL Profile] förhandsgranskning) {#profile-preview}

När data som är aktiverade för profilen hämtas till Experience Platform lagras de i datalagret Profil. När antalet poster i profilarkivet ökar eller minskar körs ett exempeljobb som innehåller information om hur många profilfragment och sammanfogade profiler som finns i datalagret. Med hjälp av profil-API:t kan du förhandsgranska det senaste framgångsrika exemplet samt lista profildistributionen per datauppsättning och per identitetsnamnområde. Information om hur du kommer igång med `/profilepreviewstatus` slutpunkten finns i guiden [för](preview-sample-status.md)förhandsvisningsexempelstatus.

## Profilsystemjobb {#profile-system-jobs}

Data som hämtas till [!DNL Platform] lagras i [!DNL Data Lake] såväl som i [!DNL Real-time Customer Profile] datalagret. Ibland kan det vara nödvändigt att ta bort en datauppsättning eller en batch från [!DNL Profile] butiken för att ta bort data som du inte längre behöver eller som har lagts till av misstag. Detta kräver att API:t används för att skapa en [!DNL Profile System Job], så kallad&quot;[!DNL delete request]&quot;, som också kan ändras, övervakas eller tas bort om det behövs. Om du vill lära dig hur du arbetar med borttagningsbegäranden med hjälp av `/system/jobs` slutpunkten i [!DNL Real-time Customer Profile] API:t följer du stegen som beskrivs i slutpunktshandboken för [profilsystemjobb](profile-system-jobs.md).

## Nästa steg {#next-steps}

Om du vill börja ringa anrop med [!DNL Real-time Customer Profile] API:t läser du [Komma igång-guiden](getting-started.md) och väljer sedan en av slutpunktshandböckerna för att lära dig hur du använder specifika [!DNL Profile]relaterade slutpunkter. Om du vill arbeta med [!DNL Profile] data med [!DNL Experience Platform] användargränssnittet läser du användarhandboken för [kundprofilen i realtid](../ui/user-guide.md).