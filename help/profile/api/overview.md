---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;enhetlig profil;Enhetlig profil;Enhetlig;Profil;rtcp;aktivera profil;Aktivera profil
title: API-guide för kundprofil i realtid
description: Med Real-Time Customer Profile API kan utvecklare utforska och arbeta med profildata, inklusive visa profiler, skapa och uppdatera sammanfogningsprinciper, exportera eller sampla profildata och ta bort profildata som inte längre behövs eller som har lagts till av misstag. Följ den här användarhandboken om du vill lära dig hur du utför viktiga åtgärder med API:t.
role: Developer
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 1%

---

# API-guide för [!DNL Real-Time Customer Profile]

Med [!DNL Real-Time Customer Profile] kan du visa en helhetsbild av alla dina enskilda kunder inom Adobe Experience Platform. Med [!DNL Profile] kan du konsolidera olika kunddata från flera olika kanaler, som online-, offline-, CRM- och tredjepartsdata, till en enhetlig vy med ett användbart, tidsstämplat konto för varje kundinteraktion.

API:t [!DNL Real-Time Customer Profile] innehåller flera slutpunkter som beskrivs nedan. Besök de enskilda slutpunktsguiderna för mer information och se [kom igång-guiden](getting-started.md) för viktig information om obligatoriska huvuden, läsning av exempel-API-anrop med mera.

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder går du till [Real-Time Customer Profile API Reference swagger](https://www.adobe.com/go/profile-apis-en).

En guide till hur du arbetar med [!DNL Real-Time Customer Profile]-data i [!DNL Experience Platform]-gränssnittet finns i [användarhandboken för profilen](../ui/user-guide.md).

## Beräknade attribut {#computed-attributes}

Beräknade attribut är funktioner som används för att samla data på händelsenivå i attribut på profilnivå. Funktionerna beräknas automatiskt så att de kan användas för segmentering, aktivering och personalisering.

Varje beräknat attribut innehåller ett uttryck, eller &quot;rule&quot;, som utvärderar inkommande data och lagrar resultatvärdet i ett profilattribut. Med hjälp av dessa beräkningar kan du enkelt besvara frågor som rör inköpstid, tid mellan köp eller antal programöppningar, utan att behöva utföra komplexa beräkningar manuellt varje gång informationen behövs. Dessa beräknade attributvärden kan sedan visas i en profil, användas för att skapa en målgrupp eller nås via ett antal olika åtkomstmönster.

Du kan skapa, visa, redigera och ta bort beräknade attribut med slutpunkten `ca/attributes/`. Mer information om hur du använder beräknade attribut finns i [översikten över beräknade attribut](../computed-attributes/overview.md). API-åtgärder finns i [API-slutpunktshandboken för beräknade attribut](../computed-attributes/api.md).

## Enheter ([!DNL Profile] åtkomst) {#entities}

Via Adobe Experience Platform kan du komma åt [!DNL Real-Time Customer Profile]-data med RESTful API:er eller användargränssnittet. Följ stegen som beskrivs i [enheternas slutpunktshandbok](entities.md) för att lära dig hur du får åtkomst till entiteter, som ofta kallas&quot;profiler&quot; med API:t. Mer information om hur du får åtkomst till profiler med hjälp av användargränssnittet för [!DNL Experience Platform] finns i [användarhandboken för profilen](../ui/user-guide.md).

## Exportera jobb ([!DNL Profile] export) {#profile-export}

[!DNL Real-Time Customer Profile] data kan exporteras till en datauppsättning för vidare bearbetning, till exempel exportera målgrupper för aktivering eller profilattribut för rapportering. Exportjobb för målgrupper är en del av [!DNL Adobe Experience Platform Segmentation Service]-API:t. Läs [slutpunktsguiden för segmenteringsexportjobb](../../profile/api/export-jobs.md) om du vill veta mer. Stegvisa instruktioner om hur du skapar och hanterar exportjobb för profilattribut finns i [slutpunktshandboken för exportjobb](export-jobs.md).

## Sammanfoga profiler {#merge-policies}

När data från flera källor samlas i [!DNL Experience Platform] är sammanfogningsprinciper de regler som [!DNL Experience Platform] använder för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa enskilda kundprofiler. Med API:t [!DNL Real-Time Customer Profile] kan du skapa nya sammanfogningsprinciper, hantera befintliga principer och ange en standardsammanfogningsprincip för organisationen. Om du vill arbeta med sammanslagningsprinciper med API:t går du till [slutpunktshandboken för sammanslagningsprinciper](merge-policies.md).

Om du vill veta mer om sammanfogningsprinciper och deras roll i Experience Platform kan du börja med att läsa översikten [för sammanfogningsprinciper](../merge-policies/overview.md).

## Förhandsgranska exempelstatus ([!DNL Profile] förhandsgranskning) {#profile-preview}

När data hämtas till Experience Platform körs ett exempeljobb för att uppdatera profilantalet och andra datarelaterade mått för kundprofiler i realtid. Resultaten av det här exempeljobbet kan visas med slutpunkten `/previewsamplestatus`, som ingår i kundprofils-API:t i realtid. Den här slutpunkten kan också användas för att lista profildistributioner av både datauppsättningen och identitetsnamnutrymmet, samt för att generera flera rapporter för att få synlighet i kompositionen för organisationens profilarkiv.  Om du vill komma igång med att använda slutpunkten `/profilepreviewstatus` kan du läsa [guiden för förhandsgranskningsexempelstatus](preview-sample-status.md).

## Profilsystemjobb {#profile-system-jobs}

Profilaktiverade data som är inkapslade i [!DNL Experience Platform] lagras i både datalagret [!DNL Data Lake] och datalagret [!DNL Real-Time Customer Profile]. Ibland kan det vara nödvändigt att ta bort profildata som är kopplade till en datauppsättning från profilarkivet för att ta bort data som inte längre behövs eller som har lagts till av misstag. Detta kräver att API används för att skapa en [!DNL Profile System Job], även kallad [!DNL delete request], som kan ändras, övervakas eller tas bort om det behövs. Om du vill lära dig hur du arbetar med borttagningsbegäranden med hjälp av `/system/jobs`-slutpunkten i [!DNL Real-Time Customer Profile] API:t följer du stegen som beskrivs i [slutpunktshandboken för profilsystemjobb](profile-system-jobs.md).

## Uppdatera profilattribut {#update-profile}

Ibland kan det vara nödvändigt att uppdatera data i din organisations profilarkiv. Du kan till exempel behöva korrigera poster eller ändra ett attributvärde. Detta kan göras via batchinmatning och kräver en profilaktiverad datauppsättning som konfigurerats med en upsert-tagg. Mer information om hur du konfigurerar en datauppsättning för attributuppdateringar finns i självstudiekursen för [att aktivera en datauppsättning för profil och uppdatering](../../catalog/datasets/enable-upsert.md).

## Nästa steg {#next-steps}

Om du vill börja ringa anrop med API:t [!DNL Real-Time Customer Profile] läser du [kom igång-guiden](getting-started.md) och väljer sedan en av slutpunktshandböckerna för att lära dig hur du använder specifika [!DNL Profile]-relaterade slutpunkter. Om du vill arbeta med [!DNL Profile]-data med [!DNL Experience Platform]-gränssnittet läser du användarhandboken för [kundprofilen i realtid](../ui/user-guide.md).
