---
keywords: Experience Platform;home;popular topics;data location;Data Location;Data management;data management;Lineage;lineage;data type;data types;Data types;Data type
solution: Experience Platform
title: Översikt över datauppsättningar
topic: datasets
description: Det här dokumentet innehåller en översikt på hög nivå över datauppsättningar i Experience Platform.
translation-type: tm+mt
source-git-commit: 23516c66a67ae5663dcf90a40ccba98bfd266ab0
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---


# Översikt över datauppsättningar

Alla data som har importerats till Adobe Experience Platform lagras i [!DNL Data Lake] som datauppsättningar. En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell, som innehåller ett schema (kolumner) och fält (rader). Datauppsättningar innehåller också metadata som beskriver olika aspekter av de data som lagras.

Det här dokumentet innehåller en översikt på hög nivå över datauppsättningar i [!DNL Experience Platform].

## Skapa datauppsättningar och spåra metadata

[!DNL Catalog Service] är systemet för post för dataplats och -rader inom [!DNL Experience Platform], och används för att skapa och hantera datamängder. [!DNL Catalog] spårar metadata för varje datauppsättning, som innehåller en referens till [!DNL Experience Data Model] (XDM)-schemat som datauppsättningen följer (förklaras i nästa avsnitt) och antalet poster som hämtas in i den datauppsättningen.

Mer information finns i [Katalogtjänstöversikten](../home.md) .

## Tvingande begränsningar för datauppsättningsdata

[!DNL Experience Data Model] (XDM) är det standardiserade ramverk som [!DNL Platform] organiserar kundupplevelsedata. Alla data som är inkapslade i måste överensstämma med ett fördefinierat XDM-schema innan de kan sparas i [!DNL Platform] [!DNL Data Lake] som en datauppsättning.

Alla datauppsättningar innehåller en referens till XDM-schemat som begränsar formatet och strukturen för de data som kan lagras. Om du försöker överföra data till en datauppsättning som inte är kompatibel med datauppsättningens XDM-schema kommer det att leda till att importen misslyckas.

Mer information om XDM finns i [XDM-systemöversikt](../../xdm/home.md).

## Samla in data i datauppsättningar

Adobe Experience Platform datainmatning representerar de olika metoder som används för att [!DNL Platform] importera data från olika källor. Oavsett vilken metod som används konverteras alla importerade data till gruppfiler. Batchar är dataenheter som består av en eller flera filer som ska importeras som en enda enhet. Dessa gruppfiler läggs sedan till i dedikerade datauppsättningar och sparas i [!DNL Data Lake].

Mer information finns i översikten över [](../../ingestion/home.md) datainmatning.

## Använda användningsetiketter på datauppsättningar

Med Adobe Experience Platform [!DNL Data Governance] kan ni hantera kunddata för att säkerställa att ni följer gällande regler, begränsningar och policyer för dataanvändning. Med DULE (Data Usage Labeling and Enforcement) som huvudramverk kan du [!DNL Data Governance] använda användningsetiketter för att kategorisera data enligt de användningsprinciper som gäller för dessa data.

Dataanvändningsetiketter kan användas på hela datauppsättningar eller enskilda datauppsättningsfält. Etiketter som läggs till på datauppsättningsnivå ärvs av alla fält i den datauppsättningen.

Mer information om tjänsten finns i översikten över [](../../data-governance/home.md) datastyrning. Anvisningar om hur du arbetar med användningsetiketter i [!DNL Platform]finns i följande handböcker:

* [Hantera etiketter i användargränssnittet](../../data-governance/labels/user-guide.md)
* [Hantera datauppsättningsrubriker i API](../../data-governance/labels/dataset-api.md)

## Datauppsättningar i underordnade [!DNL Platform] tjänster

När datauppsättningar har använts för att lagra inkapslade data, används dessa datauppsättningar sedan av [!DNL Platform] tjänster längre fram i kedjan för att uppdatera kundprofiler, få insikter via maskininlärning med mera.

Nedan följer en lista över tjänster längre fram i kedjan som använder datauppsättningar för olika åtgärder. Mer information finns i dokumentationen för respektive tjänst.

* [!DNL Data Access API](../../data-access/home.md): Gör att du kan komma åt och hämta innehållet i filer som lagras i datauppsättningar.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Överbryggar identiteter mellan enheter och system och länkar samman datauppsättningar baserat på de identitetsfält som definieras av XDM-scheman som de följer.
* [!DNL Real-time Customer Profile](../../profile/home.md): Utnyttja [!DNL Identity Service] för att skapa detaljerade kundprofiler utifrån era datauppsättningar i realtid. [!DNL Real-time Customer Profile] hämtar data från [!DNL Data Lake] och behåller kundprofiler i sitt eget separata datalager.
* [Adobe Experience Platform segmenteringstjänst](../../segmentation/home.md): Gör att ni kan skapa segment och generera målgrupper utifrån era [!DNL Real-time Customer Profile] data. Dessa målgrupper kan sedan exporteras till sina egna datauppsättningar i [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Använder maskininlärning och artificiell intelligens för att identifiera insikter i stora datamängder.
* [Adobe Experience Platform Query Service](../../query-service/home.md): Gör att du kan använda standard-SQL för att fråga data i [!DNL Experience Platform]och koppla alla datauppsättningar i [!DNL Data Lake] och hämta frågeresultat som en ny datauppsättning som kan användas i rapporter, [!DNL Data Science Workspace]eller [!DNL Real-time Customer Profile].
* [Adobe Experience Platform Decisioning Service](../../decisioning-service/home.md): Utnyttjar [!DNL Real-time Customer Profile] för att fastställa det mest troliga val en kund kommer att göra utifrån en uppsättning alternativ, baserat på de beteendedata som [!DNL Profile] hämtas från aktiverade datauppsättningar.

## Nästa steg

Genom att läsa det här dokumentet har du introducerats i de viktigaste användningsområdena för datauppsättningar i [!DNL Experience Platform]samt i de olika [!DNL Platform] tjänster som använder datauppsättningar. Mer information om olika sätt som datauppsättningar används på [!DNL Platform]finns i servicedokumentationen som är länkad i den här översikten.

Anvisningar om hur du interagerar med datauppsättningar i [!DNL Experience Platform] användargränssnittet finns i användarhandboken för [datauppsättningar](user-guide.md).