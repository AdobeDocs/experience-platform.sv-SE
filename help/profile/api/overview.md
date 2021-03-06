---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;enhetlig profil;Enhetlig profil;Enhetlig;Profil;rtcp;aktivera profil;Aktivera profil
title: API-guide för kundprofil i realtid
description: Med kundprofils-API:t i realtid kan utvecklare utforska och arbeta med profildata, inklusive visa profiler, skapa och uppdatera sammanfogningsprinciper, exportera eller sampla profildata och ta bort profildata som inte längre behövs eller som har lagts till av misstag. Följ den här vägledningen när du vill lära dig hur du utför nyckelåtgärder med API:t.
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 9f00bff31f9e7d2da1294d3d1f24cba7870a4614
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] API-guide

[!DNL Real-time Customer Profile] ger er en helhetsbild av var och en av era enskilda kunder inom Adobe Experience Platform. [!DNL Profile] kan ni sammanställa olika kunddata från olika kanaler, t.ex. online, offline, CRM och data från tredje part, i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

The [!DNL Real-time Customer Profile] API innehåller flera slutpunkter som beskrivs nedan. Mer information finns i de enskilda slutpunktshandböckerna och i [komma igång-guide](getting-started.md) om du vill ha viktig information om obligatoriska rubriker, läsa exempel-API-anrop med mera.

Om du vill visa alla tillgängliga slutpunkter och CRUD-åtgärder går du till [Referenssöka för kundprofil-API i realtid](https://www.adobe.com/go/profile-apis-en).

En guide till hur du arbetar med [!DNL Real-time Customer Profile] data i [!DNL Experience Platform] Gränssnittet, se [Användarhandbok för profil](../ui/user-guide.md).

## (Alfa) Beräknade attribut {#computed-attributes}

>[!IMPORTANT]
>
>Funktionen för beräknade attribut är alfavärden och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

Beräknade attribut är funktioner som används för att samla data på händelsenivå i attribut på profilnivå. Funktionerna beräknas automatiskt så att de kan användas för segmentering, aktivering och personalisering.

Varje beräknat attribut innehåller ett uttryck, eller &quot;rule&quot;, som utvärderar inkommande data och lagrar resultatvärdet i ett profilattribut. Med hjälp av dessa beräkningar kan du enkelt besvara frågor som rör inköpstid, tid mellan köp eller antal programöppningar, utan att behöva utföra komplexa beräkningar manuellt varje gång informationen behövs. Dessa beräknade attributvärden kan sedan visas i en profil, användas för att skapa ett segment eller nås via ett antal olika åtkomstmönster.

Du kan skapa, visa, redigera och ta bort beräknade attribut med `config/computedAttributes` slutpunkt. Mer information om hur du använder beräknade attribut finns i [översikt över beräknade attribut](../computed-attributes/overview.md). API-åtgärder finns på [API-slutpunktsguide för beräknade attribut](../computed-attributes/ca-api.md).

## Kantprojektioner {#edge-projections}

Adobe Experience Platform möjliggör personalisering av kundupplevelser i realtid genom att göra data lättillgängliga på strategiskt placerade servrar som kallas&quot;kanter&quot;. The [!DNL Real-time Customer Profile] API har slutpunkter för arbete med kanter via komponenter som kallas för &quot;projektioner&quot;. Detta inkluderar projektionskonfigurationer för att bestämma vilka data som ska projiceras för varje kant, liksom projektionsdestinationer för att definiera var projektionen ska dirigeras. Detaljerad information om hur du arbetar med kantprojektioner finns på [Projektionskonfigurationer och slutpunktsguide för destinationer](edge-projections.md).

## Enheter ([!DNL Profile] åtkomst) {#entities}

Via Adobe Experience Platform har du åtkomst [!DNL Real-time Customer Profile] data med RESTful API:er eller användargränssnittet. Följ stegen i [slutpunktsguide för enheter](entities.md). Så här får du åtkomst till profiler med [!DNL Platform] Gränssnittet, se [Användarhandbok för profil](../ui/user-guide.md).

## Exportjobb ([!DNL Profile] exportera) {#profile-export}

[!DNL Real-time Customer Profile] data kan exporteras till en datauppsättning för vidare bearbetning, som att exportera målgruppssegment för aktivering eller profilattribut för rapportering. Exportjobb för målgruppssegment ingår i [!DNL Adobe Experience Platform Segmentation Service] API, läs [slutpunktsguide för segmenteringsexportjobb](../../profile/api/export-jobs.md) om du vill veta mer. Stegvisa instruktioner om hur du skapar och hanterar exportjobb för profilattribut finns i [slutpunktsguide för exportjobb](export-jobs.md).

## Sammanfoga profiler {#merge-policies}

När data från olika källor samlas in i [!DNL Experience Platform], sammanfogningsprinciper är reglerna som [!DNL Platform] använder för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa enskilda kundprofiler. Använda [!DNL Real-time Customer Profile] API kan du skapa nya sammanfogningsprinciper, hantera befintliga profiler och ange en standardsammanfogningsprincip för organisationen. Gå till [slutpunktshandbok för sammanslagningsprinciper](merge-policies.md).

Om du vill veta mer om policyer för sammanslagning och deras roll inom Platform börjar du med att läsa [sammanfogningsprinciper - översikt](../merge-policies/overview.md).

## Förhandsgranska exempelstatus ([!DNL Profile] förhandsgranskning) {#profile-preview}

När data hämtas till Platform körs ett exempeljobb för att uppdatera profilantalet och andra datarelaterade mått för kundprofiler i realtid. Resultaten av det här exempeljobbet kan visas med `/previewsamplestatus` slutpunkt, som ingår i kundprofils-API:t i realtid. Den här slutpunkten kan också användas för att lista profildistributioner av både datauppsättning och identitetsnamnområde, samt för att generera flera rapporter för att få synlighet i sammansättningen av organisationens profilarkiv.  Så här kommer du igång med `/profilepreviewstatus` slutpunkt, se [förhandsgranska exempelstatusslutpunktshandbok](preview-sample-status.md).

## Profilsystemjobb {#profile-system-jobs}

Profilaktiverade data som är inkapslade i [!DNL Platform] lagras i [!DNL Data Lake] och [!DNL Real-time Customer Profile] datalager. Ibland kan det vara nödvändigt att ta bort en datauppsättning eller en sats från [!DNL Profile] lagra för att ta bort data som du inte längre behöver eller som har lagts till av misstag. Detta kräver att API används för att skapa en [!DNL Profile System Job], som också kallas[!DNL delete request]&quot;, som vid behov kan ändras, övervakas eller tas bort. Så här lär du dig arbeta med borttagningsbegäranden med `/system/jobs` slutpunkt i [!DNL Real-time Customer Profile] API: följ stegen som beskrivs i [slutpunktsguide för profilsystemjobb](profile-system-jobs.md).

## Uppdatera profilattribut {#update-profile}

Ibland kan det vara nödvändigt att uppdatera data i din organisations Profile Store. Du kan till exempel behöva korrigera poster eller ändra ett attributvärde. Detta kan göras via batchinmatning och kräver en profilaktiverad datauppsättning som konfigurerats med en upsert-tagg. Mer information om hur du konfigurerar en datauppsättning för attributuppdateringar finns i självstudiekursen för [aktivera en datauppsättning för profil och upsert](../../catalog/datasets/enable-upsert.md).

## Nästa steg {#next-steps}

Börja ringa samtal med [!DNL Real-time Customer Profile] API, läs [komma igång-guide](getting-started.md) välj sedan en av slutpunktsguiderna för att lära dig hur du använder specifika [!DNL Profile]-relaterade slutpunkter. Arbeta med [!DNL Profile] data med [!DNL Experience Platform] Gränssnittet, se [Användarhandbok för kundprofil i realtid](../ui/user-guide.md).
