---
keywords: Experience Platform;hem;populära ämnen;dataplats;dataplats;datahantering;datahantering;rad;rad;datatyp;datatyp;datatyper;datatyp
solution: Experience Platform
title: Datauppsättningar - översikt
topic: datasets
description: Det här dokumentet innehåller en översikt på hög nivå över datauppsättningar i Experience Platform.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---


# Översikt över datauppsättningar

Alla data som har importerats till Adobe Experience Platform lagras i [!DNL Data Lake] som datauppsättningar. En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell, som innehåller ett schema (kolumner) och fält (rader). Datauppsättningar innehåller också metadata som beskriver olika aspekter av de data som lagras.

Det här dokumentet ger en översikt på hög nivå över datauppsättningar i [!DNL Experience Platform].

## Skapa datauppsättningar och spåra metadata

[!DNL Catalog Service] är systemet för post för dataplats och -rader inom  [!DNL Experience Platform], och används för att skapa och hantera datamängder. [!DNL Catalog] spårar metadata för varje datauppsättning, som innehåller en referens till  [!DNL Experience Data Model] (XDM)-schemat som datauppsättningen följer (förklaras i nästa avsnitt) och antalet poster som hämtas in i den datauppsättningen.

Mer information finns i [Katalogtjänstöversikt](../home.md).

## Tvingande begränsningar för datauppsättningsdata

[!DNL Experience Data Model] (XDM) är det standardiserade ramverk som  [!DNL Platform] organiserar kundupplevelsedata. Alla data som är inkapslade i [!DNL Platform] måste överensstämma med ett fördefinierat XDM-schema innan de kan sparas i [!DNL Data Lake] som en datamängd.

Alla datauppsättningar innehåller en referens till XDM-schemat som begränsar formatet och strukturen för de data som kan lagras. Om du försöker överföra data till en datauppsättning som inte är kompatibel med datauppsättningens XDM-schema kommer det att leda till att importen misslyckas.

Mer information om XDM finns i [XDM-systemöversikt](../../xdm/home.md).

## Samla in data i datauppsättningar

Adobe Experience Platform datainmatning representerar de olika metoder som [!DNL Platform] använder för att importera data från olika källor. Oavsett vilken metod som används konverteras alla importerade data till gruppfiler. Batchar är dataenheter som består av en eller flera filer som ska importeras som en enda enhet. Dessa gruppfiler läggs sedan till i dedikerade datauppsättningar och sparas i [!DNL Data Lake].

Mer information finns i [Översikt över datainmatning](../../ingestion/home.md).

## Använda användningsetiketter på datauppsättningar

Med Adobe Experience Platform [!DNL Data Governance] kan ni hantera kunddata för att säkerställa efterlevnad av regler, begränsningar och policyer som gäller för dataanvändning. Med [!DNL Data Governance]-ramverket kan du använda användningsetiketter för att kategorisera data enligt de användningsprinciper som gäller för dessa data.

Dataanvändningsetiketter kan användas på hela datauppsättningar eller enskilda datauppsättningsfält. Etiketter som läggs till på datauppsättningsnivå ärvs av alla fält i den datauppsättningen.

Mer information om tjänsten finns i [Datastyrningsöversikten](../../data-governance/home.md). Anvisningar om hur du arbetar med användningsetiketter i [!DNL Platform] finns i följande handböcker:

* [Hantera etiketter i användargränssnittet](../../data-governance/labels/user-guide.md)
* [Hantera datauppsättningsrubriker i API](../../data-governance/labels/dataset-api.md)

## Datauppsättningar i underordnade [!DNL Platform]-tjänster

När datauppsättningar har använts för att lagra inkapslade data används dessa datauppsättningar av [!DNL Platform]-tjänster längre fram i kedjan för att uppdatera kundprofiler, få insikter via maskininlärning och mycket annat.

Nedan följer en lista över tjänster längre fram i kedjan som använder datauppsättningar för olika åtgärder. Mer information finns i dokumentationen för respektive tjänst.

* [[!DNL Data Access API]](../../data-access/home.md): Gör att du kan komma åt och hämta innehållet i filer som lagras i datauppsättningar.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Överbryggar identiteter mellan enheter och system och länkar samman datauppsättningar baserat på de identitetsfält som definieras av XDM-scheman som de följer.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Utnyttja  [!DNL Identity Service] för att skapa detaljerade kundprofiler utifrån era datauppsättningar i realtid. [!DNL Real-time Customer Profile] hämtar data från  [!DNL Data Lake] och behåller kundprofiler i sitt eget separata datalager.
* [Adobe Experience Platform segmenteringstjänst](../../segmentation/home.md): Gör att ni kan skapa segment och generera målgrupper utifrån era  [!DNL Real-time Customer Profile] data. Dessa målgrupper kan sedan exporteras till sina egna datauppsättningar i [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Använder maskininlärning och artificiell intelligens för att identifiera insikter i stora datamängder.
* [Adobe Experience Platform Query Service](../../query-service/home.md): Gör att du kan använda standard-SQL för att fråga data i  [!DNL Experience Platform]och koppla alla datauppsättningar i  [!DNL Data Lake] och hämta frågeresultat som en ny datamängd som kan användas för rapportering,  [!DNL Data Science Workspace]eller  [!DNL Real-time Customer Profile].

## Nästa steg

Genom att läsa det här dokumentet har du introducerats i de viktigaste användningsområdena för datauppsättningar i [!DNL Experience Platform], samt i de olika [!DNL Platform]-tjänsterna som använder datauppsättningar. Mer information om hur datauppsättningar används i [!DNL Platform] finns i den servicedokumentation som är länkad i den här översikten.

Anvisningar om hur du interagerar med datauppsättningar i användargränssnittet för [!DNL Experience Platform] finns i användarhandboken för [datauppsättningar](user-guide.md).