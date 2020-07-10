---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Utvecklarhandbok för kundprofil-API i realtid
topic: guide
translation-type: tm+mt
source-git-commit: c0b059d6654a98b74be5bc6a55f360c4dc2f216b
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---


# Utvecklarhandbok för kundprofil-API i realtid

Med kundprofilen i realtid kan ni få en helhetsbild av var och en av era enskilda kunder i Adobe Experience Platform. Med en profil kan ni sammanställa olika kunddata från flera olika kanaler, t.ex. online-, offline-, CRM- och tredjepartsdata, i en enhetlig vy med ett användbart tidsstämplat konto för varje kundinteraktion.

Real-time Customer Profile API innehåller flera slutpunkter som beskrivs nedan. Besök de enskilda slutpunktshandböckerna för mer information och se [komma igång-guiden](getting-started.md) för viktig information om obligatoriska huvuden, läsning av exempel-API-anrop med mera.

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder läser du API-referenssaggern för kundprofil i [realtid](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

## (Alfa) Beräknade attribut

>[!IMPORTANT]
>
>
>Funktionen för beräknade attribut är alfavärden och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

Med beräknade attribut kan du automatiskt beräkna fältvärden baserat på andra värden, beräkningar och uttryck. Beräknade attribut fungerar på profilnivån, vilket innebär att du kan samla värden för alla poster och händelser. Varje beräknat attribut innehåller ett uttryck, eller &quot;rule&quot;, som utvärderar inkommande data och lagrar resultatvärdet i ett profilattribut eller i en händelse. Med hjälp av dessa beräkningar kan du enkelt besvara frågor som rör inköpstid, tid mellan köp eller antal programöppningar, utan att behöva utföra komplexa beräkningar manuellt varje gång informationen behövs. Du kan skapa, visa, redigera och ta bort beräknade attribut med hjälp av `config/computedAttributes` slutpunkten. Om du vill lära dig hur du använder den här slutpunkten kan du gå till guiden [för](computed-attributes.md)beräknade attribut.

## Kantprojektioner

Adobe Experience Platform möjliggör personalisering av kundupplevelser i realtid genom att göra data lättillgängliga på strategiskt placerade servrar som kallas&quot;kanter&quot;. Real-time Customer Profile API innehåller slutpunkter för att arbeta med kanter via komponenter som kallas för &quot;projektioner&quot;. Detta inkluderar projektionskonfigurationer för att bestämma vilka data som ska projiceras för varje kant, liksom projektionsdestinationer för att definiera var projektionen ska dirigeras. Detaljerad information om hur du arbetar med kantprojektioner finns i guiden [för](edge-projections.md)projektionskonfigurationer och destinationspunkter.

## Enheter (profilåtkomst) {#entities}

Via Adobe Experience Platform får du åtkomst till kundprofildata i realtid med RESTful API:er eller användargränssnittet. Om du vill lära dig hur du får åtkomst till enheter, som ofta kallas&quot;profiler&quot;, med API:t, följer du stegen som beskrivs i slutpunktshandboken för [enheter](entities.md). Mer information om hur du får åtkomst till profiler med hjälp av användargränssnittet i Platform finns i användarhandboken för [profilen](../ui/user-guide.md).

## Sammanfoga profiler

När data från flera källor samlas i Experience Platform är kopplingsregler de regler som Platform använder för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa enskilda kundprofiler. Med hjälp av kundprofils-API:t i realtid kan du skapa nya kopplingsprofiler, hantera befintliga profiler och ange en standardkopplingsprofil för organisationen. Mer information om hur du arbetar med sammanfogningspolicyer med API finns i slutpunktshandboken för [sammanfogningspolicyer](merge-policies.md).

En guide till hur du arbetar med sammanfogningsprinciper med hjälp av Platform-gränssnittet finns i användarhandboken [för](../ui/merge-policies.md)sammanfogningsprinciper.

## Profilsystemjobb

Data som hämtas till Platform lagras i Data Lake samt i datalagret för kundprofiler i realtid. Ibland kan det vara nödvändigt att ta bort en datauppsättning eller en batch från profilarkivet för att ta bort data som du inte längre behöver eller som har lagts till av misstag. Detta kräver att API:t används för att skapa ett profilsystemjobb, som kallas&quot;delete request&quot;, som också kan ändras, övervakas eller tas bort om det behövs. Om du vill lära dig hur du arbetar med borttagningsbegäranden med hjälp av `/system/jobs` slutpunkten i kundprofils-API:t i realtid, följer du stegen som beskrivs i slutpunktshandboken för [profilsystemjobb](profile-system-jobs.md).

## Nästa steg

Om du vill börja ringa samtal med Real-time Customer Profile API läser du [Komma igång-guiden](getting-started.md) och väljer sedan en av slutpunktshandböckerna för att lära dig hur du använder specifika profilrelaterade slutpunkter. Mer information om hur du arbetar med profildata med Platform-gränssnittet finns i användarhandboken för [kundprofiler](../ui/user-guide.md)i realtid.