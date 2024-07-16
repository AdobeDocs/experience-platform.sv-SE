---
keywords: Experience Platform;hem;populära ämnen;dataplats;dataplats;datahantering;datahantering;rad;rad;datatyp;datatyp;datatyper;datatyp
solution: Experience Platform
title: Datauppsättningar - översikt
description: Det här dokumentet innehåller en översikt på hög nivå över datauppsättningar i Experience Platform.
user-guide-description: Få en översikt över datauppsättningar på hög nivå i Experience Platform med den här guiden. Lär dig hur du skapar dem, tillämpar begränsningar för data och importerar data till datauppsättningar här.
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: 81f570f8e5401624ccac74696b2323252a4de0a9
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 1%

---

# Datauppsättningar - översikt

Alla data som har importerats till Adobe Experience Platform lagras i [!DNL Data Lake] som datauppsättningar. En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell, som innehåller ett schema (kolumner) och fält (rader). Datauppsättningar innehåller också metadata som beskriver olika aspekter av de data som lagras.

Det här dokumentet ger en översikt på hög nivå över datauppsättningar i [!DNL Experience Platform].

## Skapa datauppsättningar och spåra metadata

[!DNL Catalog Service] är ett system för post för dataplats och datalinje inom [!DNL Experience Platform] och används för att skapa och hantera datamängder. [!DNL Catalog] spårar metadata för varje datauppsättning, som innehåller en referens till [!DNL Experience Data Model] (XDM)-schemat som datauppsättningen följer (förklaras i nästa avsnitt) och antalet poster som hämtas in till den datauppsättningen.

Mer information finns i [Katalogtjänstöversikt](../home.md).

## Tvingande begränsningar för datauppsättningsdata

[!DNL Experience Data Model] (XDM) är det standardiserade ramverk som [!DNL Platform] organiserar kundupplevelsedata med. Alla data som är inkapslade i [!DNL Platform] måste överensstämma med ett fördefinierat XDM-schema innan de kan sparas i [!DNL Data Lake] som en datauppsättning.

Alla datauppsättningar innehåller en referens till XDM-schemat som begränsar formatet och strukturen för de data som kan lagras. Om du försöker överföra data till en datauppsättning som inte är kompatibel med datauppsättningens XDM-schema kommer det att leda till att importen misslyckas.

Mer information om XDM finns i [XDM-systemöversikt](../../xdm/home.md).

## Samla in data i datauppsättningar

Adobe Experience Platform datainmatning representerar de olika metoder som [!DNL Platform] använder för att importera data från olika källor. Oavsett vilken metod som används konverteras alla importerade data till gruppfiler. Batchar är dataenheter som består av en eller flera filer som ska importeras som en enda enhet. Dessa gruppfiler läggs sedan till i dedikerade datamängder och sparas i [!DNL Data Lake].

Mer information finns i [Översikt över datainmatning](../../ingestion/home.md).

## Etiketter som tillämpas på datauppsättningar från scheman

Med Adobe Experience Platform Data Governance kan ni hantera kunddata för att säkerställa efterlevnad av regler, begränsningar och policyer som gäller för dataanvändning. Med ramverket för datastyrning kan du använda användningsetiketter för att kategorisera data enligt de användningsprinciper som gäller för dessa data. Etiketter kan användas på enskilda scheman, fält inom dessa scheman och hela enskilda datauppsättningar. När etiketter används direkt i ett schema sprids dessa etiketter till alla befintliga och framtida datauppsättningar som baseras på det schemat.

>[!IMPORTANT]
>
>Etiketter kan inte längre användas på fält på datauppsättningsnivå. Det här arbetsflödet har ersatts med etiketter på schemanivå. Etiketter som tidigare använts på datauppsättningens objektnivå stöds fortfarande i plattformsgränssnittet fram till den 31 maj 2024. För att etiketterna ska vara enhetliga i alla scheman måste du migrera alla etiketter som tidigare har kopplats till fält på datauppsättningsnivå till schemanivån under det kommande året. Mer information om hur du gör detta finns i avsnittet [migrera tidigare använda etiketter](../../data-governance/e2e.md#migrate-labels).

Mer information om tjänsten finns i [Datastyrningsöversikten](../../data-governance/home.md). Anvisningar om hur du arbetar med användningsetiketter i [!DNL Platform] finns i följande guider:

* [Hantera etiketter i användargränssnittet](../../data-governance/labels/user-guide.md)
* [Hantera datauppsättningsrubriker i API](../../data-governance/labels/dataset-api.md)

## Datauppsättningar i underordnade [!DNL Platform]-tjänster

När datauppsättningar har använts för att lagra inkapslade data används dessa datauppsättningar av [!DNL Platform]-tjänster längre fram i kedjan för att uppdatera kundprofiler, få insikter via maskininlärning och mycket annat.

Nedan följer en lista över tjänster längre fram i kedjan som använder datauppsättningar för olika åtgärder. Mer information finns i dokumentationen för respektive tjänst.

* [[!DNL Data Access API]](../../data-access/home.md): Gör att du kan komma åt och hämta innehållet i filer som lagras i datauppsättningar.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Förena identiteter mellan enheter och system genom att länka samman datauppsättningar baserat på de identitetsfält som definieras av XDM-scheman som de följer.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): utnyttjar [!DNL Identity Service] för att skapa detaljerade kundprofiler från dina datauppsättningar i realtid. [!DNL Real-Time Customer Profile] hämtar data från [!DNL Data Lake] och behåller kundprofiler i sitt eget separata datalager.
* [Adobe Experience Platform segmenteringstjänst](../../segmentation/home.md): Gör att du kan skapa segment och generera målgrupper utifrån dina [!DNL Real-Time Customer Profile]-data. Dessa målgrupper kan sedan exporteras till sina egna datauppsättningar inom [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Använder maskininlärning och artificiell intelligens för att identifiera insikter i stora datamängder.
* [Adobe Experience Platform Query Service](../../query-service/home.md): Gör att du kan använda standard-SQL för att fråga data i [!DNL Experience Platform], koppla datauppsättningar i [!DNL Data Lake] och hämta frågeresultat som en ny datamängd för användning i rapporter, [!DNL Data Science Workspace] eller [!DNL Real-Time Customer Profile].
* [Adobe Experience Platform destinationstjänst](../../destinations/home.md): Gör att du kan [exportera datamängder](/help/destinations/ui/export-datasets.md) till önskat molnlagringsutrymme eller e-postmarknadsföringsmål för rapporter- eller datavetenskapsaktiviteter.

## Nästa steg

Genom att läsa det här dokumentet har du introducerats till de viktigaste användningsområdena för datauppsättningar i [!DNL Experience Platform], samt till de olika [!DNL Platform]-tjänster som använder datauppsättningar. Mer information om de många sätt som datauppsättningar används på i [!DNL Platform] finns i servicedokumentationen som är länkad i den här översikten.

Anvisningar om hur du interagerar med datauppsättningar i användargränssnittet för [!DNL Experience Platform] finns i användarhandboken för [datauppsättningar](user-guide.md).
