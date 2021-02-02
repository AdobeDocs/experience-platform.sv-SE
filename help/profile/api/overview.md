---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;enhetlig profil;Enhetlig profil;Enhetlig;Profil;rtcp;aktivera profil;Aktivera profil
title: Utvecklarhandbok för kundprofil-API i realtid
topic: guide
description: Real-time Customer Profile API innehåller flera slutpunkter för att utforska och arbeta med profildata, inklusive visningsprofiler, skapa och uppdatera sammanfogningsprinciper, exportera eller sampla profildata och ta bort profildata som du inte längre behöver eller som har lagts till av misstag.
translation-type: tm+mt
source-git-commit: 823d89ab37156e775a2879e3a2c91bfd911b83bb
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] Utvecklarhandbok för API

[!DNL Real-time Customer Profile] ger er en helhetsbild av var och en av era enskilda kunder inom Adobe Experience Platform. [!DNL Profile] kan ni sammanställa olika kunddata från olika kanaler, t.ex. online, offline, CRM och data från tredje part, i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

API:t [!DNL Real-time Customer Profile] innehåller flera slutpunkter som beskrivs nedan. Mer information finns i de enskilda slutpunktshandböckerna och i [komma igång-guiden](getting-started.md) finns viktig information om obligatoriska huvuden, läsning av exempel-API-anrop med mera.

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder går du till [API-referenssaggen för kundprofiler i realtid](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

En guide till hur du arbetar med [!DNL Real-time Customer Profile]-data i [!DNL Experience Platform]-gränssnittet finns i [användarhandboken för profilen](../ui/user-guide.md).

## (Alfa) Beräknade attribut {#computed-attributes}

>[!IMPORTANT]
>
>Funktionen för beräknade attribut är alfavärden och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

Med beräknade attribut kan du automatiskt beräkna fältvärden baserat på andra värden, beräkningar och uttryck. Beräknade attribut fungerar på profilnivån, vilket innebär att du kan samla värden över alla poster och händelser. Varje beräknat attribut innehåller ett uttryck, eller &quot;rule&quot;, som utvärderar inkommande data och lagrar resultatvärdet i ett profilattribut eller i en händelse. Med hjälp av dessa beräkningar kan du enkelt besvara frågor som rör inköpstid, tid mellan köp eller antal programöppningar, utan att behöva utföra komplexa beräkningar manuellt varje gång informationen behövs. Du kan skapa, visa, redigera och ta bort beräknade attribut med `config/computedAttributes`-slutpunkten. Om du vill lära dig hur du använder den här slutpunkten kan du gå till [handboken för beräknade attribut](computed-attributes.md).

## Kantprojektioner {#edge-projections}

Adobe Experience Platform möjliggör personalisering av kundupplevelser i realtid genom att göra data lättillgängliga på strategiskt placerade servrar som kallas&quot;kanter&quot;. API:t [!DNL Real-time Customer Profile] innehåller slutpunkter för att arbeta med kanter genom komponenter som kallas för &quot;projektioner&quot;. Detta inkluderar projektionskonfigurationer för att bestämma vilka data som ska projiceras för varje kant, liksom projektionsdestinationer för att definiera var projektionen ska dirigeras. Detaljerad information om hur du arbetar med kantprojektioner finns i guiden [projektionskonfigurationer och målslutpunkter](edge-projections.md).

## Enheter ([!DNL Profile] åtkomst) {#entities}

Via Adobe Experience Platform kan du komma åt [!DNL Real-time Customer Profile]-data med RESTful API:er eller användargränssnittet. Följ stegen i [entitetens slutpunktshandbok](entities.md) för att lära dig hur du får åtkomst till entiteter, som ofta kallas &quot;profiler&quot; med API:t. Mer information om hur du får åtkomst till profiler med hjälp av användargränssnittet i [!DNL Platform] finns i [användarhandboken för profilen](../ui/user-guide.md).

## Exportera jobb ([!DNL Profile] export) {#profile-export}

[!DNL Real-time Customer Profile] data kan exporteras till en datauppsättning för vidare bearbetning, som att exportera målgruppssegment för aktivering eller profilattribut för rapportering. Exportjobb för målgruppssegment ingår i [!DNL Adobe Experience Platform Segmentation Service] API. Läs [slutpunktsguiden för segmenteringsexportjobb](../../profile/api/export-jobs.md) om du vill veta mer. Stegvisa instruktioner om hur du skapar och hanterar exportjobb för profilattribut finns i [slutpunktshandboken för exportjobb](export-jobs.md).

## Sammanfoga profiler {#merge-policies}

När data från flera källor samlas i [!DNL Experience Platform] är sammanfogningsprinciper de regler som [!DNL Platform] använder för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa enskilda kundprofiler. Med API:t [!DNL Real-time Customer Profile] kan du skapa nya sammanfogningsprinciper, hantera befintliga profiler och ange en standardsammanfogningsprincip för organisationen. Mer information om hur du arbetar med sammanfogningsprinciper med API:t finns i [slutpunktshandboken för sammanfogningsprinciper](merge-policies.md).

En guide till hur du arbetar med sammanfogningsprinciper med hjälp av användargränssnittet i [!DNL Platform] finns i [användarhandboken för sammanfogningsprinciper](../ui/merge-policies.md).

## Förhandsgranska exempelstatus ([!DNL Profile] preview) {#profile-preview}

När data som är aktiverade för profilen hämtas till Experience Platform lagras de i datalagret Profil. När antalet poster i profilarkivet ökar eller minskar körs ett exempeljobb som innehåller information om hur många profilfragment och sammanfogade profiler som finns i datalagret. Med hjälp av profil-API:t kan du förhandsgranska det senaste framgångsrika exemplet samt lista profildistributionen per datauppsättning och per identitetsnamnområde. Om du vill komma igång med att använda slutpunkten `/profilepreviewstatus` kan du läsa [guiden för att förhandsgranska exempelstatus](preview-sample-status.md).

## Profilsystemjobb {#profile-system-jobs}

Profilaktiverade data som är inkapslade i [!DNL Platform] lagras i både [!DNL Data Lake] och [!DNL Real-time Customer Profile]-datalagret. Ibland kan det vara nödvändigt att ta bort en datauppsättning eller en batch från [!DNL Profile]-butiken för att ta bort data som du inte längre behöver eller som har lagts till av misstag. Detta kräver att API används för att skapa en [!DNL Profile System Job], även kallad [!DNL delete request], som kan ändras, övervakas eller tas bort om det behövs. Om du vill lära dig hur du arbetar med borttagningsbegäranden med hjälp av `/system/jobs`-slutpunkten i [!DNL Real-time Customer Profile] API:t följer du stegen som beskrivs i [slutpunktshandboken för profilsystemjobb](profile-system-jobs.md).

## Nästa steg {#next-steps}

Om du vill börja ringa anrop med API:t [!DNL Real-time Customer Profile] läser du [Komma igång-guiden](getting-started.md) och väljer sedan en av slutpunktshandböckerna för att lära dig hur du använder specifika [!DNL Profile]-relaterade slutpunkter. Om du vill arbeta med [!DNL Profile]-data med hjälp av användargränssnittet för [!DNL Experience Platform] läser du användarhandboken för [kundprofilen i realtid](../ui/user-guide.md).