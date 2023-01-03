---
keywords: Experience Platform;hemmabruk;populära ämnen;CJA;reseanalys;kundreseanalys;kampanjsamordning;orkestrering;kundresa;resa;resesamordning;kapacitet;region
title: Adobe Experience Platform kompletta exempelarbetsflöde
topic-legacy: getting started
description: Lär dig det grundläggande arbetsflödet från början till slut för Adobe Experience Platform på en hög nivå.
exl-id: 0a4d3b68-05a5-43ef-bf0d-5738a148aa77
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1835'
ht-degree: 0%

---

# Adobe Experience Platform kompletta exempelarbetsflöde

Adobe Experience Platform är det mest kraftfulla, flexibla och öppna systemet på marknaden för att bygga och hantera kompletta lösningar som ger en bättre kundupplevelse. Med Platform kan organisationer centralisera och standardisera kunddata och innehåll från alla system och tillämpa datavetenskap och maskininlärning för att dramatiskt förbättra utformningen och leveransen av avancerade, personaliserade upplevelser.

Platform bygger på RESTful-API:er och ger utvecklarna tillgång till systemets alla funktioner, vilket gör det enkelt att integrera företagslösningar med välbekanta verktyg. Med Platform kan ni få en helhetsbild av era kunder genom att inhämta era kunddata, segmentera data till de målgrupper ni vill ha och aktivera dessa målgrupper till en extern målgrupp. I följande självstudiekurs visas ett komplett arbetsflöde som visar alla steg från inmatning via källor till målgruppsaktivering via destinationer.

![Experience Platform från början till slut](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## Komma igång

Detta kompletta arbetsflöde använder flera Adobe Experience Platform-tjänster. Nedan följer en lista över de tjänster som används i det här arbetsflödet med länkar till översikter över dem:

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Det standardiserade ramverk som [!DNL Platform] organiserar kundupplevelsedata. För att utnyttja segmenteringen på bästa sätt bör du se till att dina data är inmatade som profiler och händelser enligt [bästa praxis för datamodellering](../xdm/schema/best-practices.md).
- [[!DNL Identity Service]](../identity-service/home.md): Förser er med en heltäckande bild av era kunder och deras beteende genom att överbrygga identiteter mellan olika enheter och system.
- [Källor](../sources/home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
- [[!DNL Segmentation Service]](../segmentation/home.md): [!DNL Segmentation Service] kan du dela upp data som lagras i [!DNL Experience Platform] som rör individer (t.ex. kunder, prospects, användare eller organisationer) i mindre grupper.
- [[!DNL Real-Time Customer Profile]](../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
- [Datauppsättningar](../catalog/datasets/overview.md): Konstruktionen för lagring och hantering av databeständighet i [!DNL Experience Platform].
- [Destinationer](../destinations/home.md): Destinationer är färdiga integreringar med vanliga applikationer som möjliggör smidig aktivering av data från Platform för flerkanalskampanjer, e-postkampanjer, riktad annonsering och många andra användningsfall.

## Skapa ett XDM-schema

Innan du importerar data till Platform måste du först skapa ett XDM-schema som beskriver datastrukturen. När du importerar dina data i nästa steg mappas dina inkommande data till det här schemat. Läs självstudiekursen om du vill lära dig hur du skapar ett XDM-exempelschema [skapa ett schema med Schemaredigeraren](../xdm/tutorials/create-schema-ui.md).

Ovanstående självstudiekurs visar hur du anger identitetsfält för dina scheman. Ett identitetsfält representerar ett fält som kan användas för att identifiera en enskild person som är relaterad till en post- eller tidsseriehändelse. Identitetsfält är en viktig komponent i hur kundidentitetsdiagram skapas i Platform, som i slutändan påverkar hur kundprofilen i realtid sammanfogar olika datablad för att få en fullständig bild av kunden. Mer information om hur du visar identitetsdiagram i plattformen finns i självstudiekursen om [hur du använder visningsprogrammet för identitetsdiagram](../identity-service/ui/identity-graph-viewer.md).

Du måste aktivera ditt schema för användning i kundprofilen i realtid så att kundprofiler kan skapas utifrån data som baseras på ditt schema. Se avsnittet om [aktivera ett schema för profil](../xdm/ui/resources/schemas.md#profile) i gränssnittshandboken för scheman för mer information.

## Infoga data i plattformen

När du har skapat ett XDM-schema kan du börja föra in data i systemet.

Alla data som hämtas till Platform lagras på enskilda datauppsättningar vid intag. En datauppsättning är en samling dataposter som mappar till ett specifikt XDM-schema. Innan dina data kan användas av [!DNL Real-Time Customer Profile]måste den aktuella datauppsättningen konfigureras specifikt. Fullständiga anvisningar om hur du aktiverar en datauppsättning för profilen finns i [Användargränssnittshandbok för datauppsättningar](../catalog/datasets/user-guide.md#enable-profile) och [API-självstudiekurs för konfiguration av datauppsättning](../profile/tutorials/dataset-configuration.md). När datauppsättningen har konfigurerats kan du börja inhämta data i den.

Plattformen gör det möjligt att importera data från externa källor samtidigt som du får möjlighet att strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserade lager, databaser och många andra. Du kan till exempel importera data med [Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md). En fullständig lista över tillgängliga källor finns i [översikt över källanslutningar](../sources/home.md).

Om du använder Amazon S3 som källanslutning kan du följa instruktionerna i antingen API-självstudiekursen på [skapa en Amazon S3-anslutning](../sources/tutorials/api/create/cloud-storage/s3.md) eller självstudiekursen på [skapa en Amazon S3-anslutning](../sources/tutorials/ui/create/cloud-storage/s3.md) för att lära dig hur du skapar, ansluter till och importerar data i kopplingen.

Mer detaljerad information om källanslutningar finns i [översikt över källanslutningar](../sources/home.md). Om du vill veta mer om Flow Service, det API som källorna baseras på, kan du läsa [API-referens för Flow Service](https://www.adobe.io/experience-platform-apis/references/flow-service/).

När data hämtas till Platform via källkopplingen och lagras i din profilaktiverade datauppsättning skapas kundprofiler automatiskt baserat på de identitetsdata som du konfigurerade i XDM-schemat.

När du överför data till en ny datauppsättning för första gången, eller när du konfigurerar en ny ETL-process eller datakälla, bör du noggrant kontrollera data för att se till att de har överförts korrekt och att de genererade profilerna innehåller de data du förväntar dig. Mer information om hur du får åtkomst till kundprofiler i plattformsgränssnittet finns i [Användargränssnittsguide för kundprofil i realtid](../profile/ui/user-guide.md). Mer information om hur du får åtkomst till profiler med hjälp av kundprofils-API:t i realtid finns i handboken [använda enheternas slutpunkt](../profile/api/entities.md).

## Utvärdera era data

När du har genererat profiler från dina inkapslade data kan du utvärdera dina data genom att använda segmentering. Segmentering är processen att definiera specifika attribut eller beteenden som delas av en delmängd av individer från din profilbutik, för att särskilja en marknadsföringsbar grupp av människor från din kundbas. Läs mer om segmentering i [segmenteringstjänst - översikt](../segmentation/home.md).

### Skapa en segmentdefinition

För att komma igång måste ni skapa en segmentdefinition för att klustra era kunder och skapa målgrupper. En segmentdefinition är en samling regler som du kan använda för att definiera målgruppen. Om du vill skapa en segmentdefinition följer du instruktionerna i användargränssnittshandboken för att använda [Segment Builder](../segmentation/ui/segment-builder.md) eller API-självstudiekursen på [skapa ett segment](../segmentation/tutorials/create-a-segment.md).

När du har skapat en segmentdefinition måste du tänka på segmentdefinitions-ID:t.

### Utvärdera din segmentdefinition

När du har skapat segmentdefinitionen kan du antingen skapa ett segmentjobb för att utvärdera segmentet som en engångsinstans eller skapa ett schema för att utvärdera segmentet kontinuerligt.

Om du vill utvärdera en segmentdefinition vid behov kan du skapa ett segmentjobb. Ett segmentjobb är en asynkron process som skapar ett nytt målgruppssegment baserat på den refererade segmentdefinitionen och sammanfogningsprinciperna. En sammanfogningspolicy är en uppsättning regler som Platform använder för att avgöra vilka data som ska användas för att skapa kundprofiler och vilka data som ska prioriteras när det finns skillnader mellan olika källor. Mer information om hur du arbetar med sammanfogningspolicyer finns i [gränssnittshandbok för sammanslagningsprinciper](../profile/merge-policies/ui-guide.md).

När segmentjobbet har skapats och utvärderats kan du få information om segmentet, t.ex. storlek på målgruppen eller fel som kan ha uppstått under bearbetningen. Om du vill veta hur du skapar ett segmentjobb, inklusive all information du behöver, kan du läsa [guide för segmentjobbutvecklare](../segmentation/api/segment-jobs.md).

Om du vill utvärdera en segmentdefinition kontinuerligt kan du skapa och aktivera ett schema. Ett schema är ett verktyg som kan användas för att automatiskt köra ett segmentjobb en gång om dagen vid en viss tidpunkt. Om du vill lära dig hur du skapar och aktiverar ett schema kan du följa instruktionerna i API-handboken på [slutpunkt för tidsplaner](../segmentation/api/schedules.md).

## Exportera utvärderade data

När du har skapat ett engångssegmentjobb eller ett pågående schema kan du antingen skapa ett segmentexportjobb för att exportera resultaten till en datauppsättning eller exportera resultaten till ett mål. I följande avsnitt finns vägledning om båda dessa alternativ.

### Exportera utvärderade data till en datauppsättning

När du har skapat ett engångssegmentjobb eller ett pågående schema kan du exportera resultatet genom att skapa ett segmentexportjobb. Ett segmentexportjobb är en asynkron uppgift som skickar information om den utvärderade målgruppen till en datauppsättning.

Innan du skapar ett exportjobb måste du först skapa en datauppsättning att exportera data till. Läs avsnittet om hur du skapar en datauppsättning [skapa en måldatauppsättning](../segmentation/tutorials/evaluate-a-segment.md#create-dataset) i självstudiekursen om hur du utvärderar ett segment och ser till att du noterar datauppsättnings-ID:t när det har skapats. När du har skapat en datauppsättning kan du skapa ett exportjobb. Om du vill lära dig hur du skapar ett exportjobb kan du följa instruktionerna i API-handboken på [slutpunkt för exportjobb](../segmentation/api/export-jobs.md).

### Exportera utvärderade data till ett mål

När du har skapat ett engångssegmentjobb eller ett pågående schema kan du också exportera resultatet till ett mål. Ett mål är en slutpunkt, till exempel ett Adobe-program på en extern tjänst, där en målgrupp kan aktiveras och levereras. En fullständig lista över tillgängliga destinationer finns i [målkatalog](../destinations/catalog/overview.md).

Instruktioner om hur du aktiverar data till marknadsföring via batch eller e-post finns i självstudiekursen om [hur du aktiverar målgruppsdata för att batchprofilera exportmål med hjälp av användargränssnittet för plattformen](../destinations/ui/activate-batch-profile-destinations.md) och [guide om hur du ansluter till batchmål och aktiverar data med API:t för Flow Service](../destinations/api/connect-activate-batch-destinations.md).

## Övervaka plattformsdataaktiviteter

Med Platform kan ni spåra hur data bearbetas med hjälp av dataflöden, vilket är en representation av jobb som flyttar data mellan plattformens olika komponenter. Dessa dataflöden är konfigurerade för olika tjänster, vilket hjälper dig att flytta data från källanslutningar till måldatauppsättningar, där de sedan används av [!DNL Identity Service] och [!DNL Real-Time Customer Profile] innan de aktiveras till destinationer. Kontrollpanelen ger dig en visuell representation av resan för ett dataflöde. Om du vill lära dig hur du övervakar dataflöden i plattformsgränssnittet kan du läsa självstudiekurserna på [övervaka dataflöden för källor](../dataflows/ui/monitor-sources.md) och [övervaka dataflöden för destinationer](../dataflows/ui/monitor-destinations.md).

Du kan också övervaka plattformsaktiviteter genom att använda statistiska värden och händelsemeddelanden med [!DNL Observability Insights]. Du kan prenumerera på varningsmeddelanden via plattformsgränssnittet eller skicka dem till en konfigurerad webkrok. Mer information om hur du visar, aktiverar, inaktiverar och prenumererar på tillgängliga aviseringar från användargränssnittet i Experience Platform finns i [[!UICONTROL Alerts] Användargränssnittsguide](../observability/alerts/ui.md). Mer information om hur du tar emot varningar via webbhookar finns i handboken [prenumerera på händelsemeddelanden från Adobe I/O](../observability/alerts/subscribe.md).

## Nästa steg

Genom att läsa den här självstudiekursen har du fått en grundläggande introduktion till ett enkelt helhetsflöde för Platform. Läs mer om Adobe Experience Platform i [Plattformsöversikt](./home.md). Läs mer om hur du använder plattformsgränssnittet och plattforms-API:t i [Användargränssnittshandbok för plattformen](./ui-guide.md) och [Plattforms-API-guide](./api-guide.md) respektive.
