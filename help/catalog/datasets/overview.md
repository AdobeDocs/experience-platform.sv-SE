---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över datauppsättningar
topic: datasets
translation-type: tm+mt
source-git-commit: 06733eb374d1b9409102a7cf13d61ed266cedaad

---


# Översikt över datauppsättningar

Alla data som har importerats till Adobe Experience Platform lagras i Data Lake som datauppsättningar. En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell, som innehåller ett schema (kolumner) och fält (rader). Datauppsättningar innehåller också metadata som beskriver olika aspekter av de data som lagras.

Det här dokumentet ger en översikt på hög nivå över datauppsättningar i Experience Platform.

## Skapa datauppsättningar och spåra metadata

Katalogtjänsten är ett system för registrering av dataplatser och datalänkning inom Experience Platform och används för att skapa och hantera datamängder. Katalogen spårar metadata för varje datauppsättning, som innehåller en referens till XDM-schemat (Experience Data Model) som datauppsättningen följer (förklaras i nästa avsnitt) och antalet poster som hämtas till den datauppsättningen.

Mer information finns i [Katalogtjänstöversikten](../home.md) .

## Tvingande begränsningar för datauppsättningsdata

Experience Data Model (XDM) är det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata. Alla data som hämtas till Platform måste överensstämma med ett fördefinierat XDM-schema innan de kan sparas i Data Lake som en datauppsättning.

Alla datauppsättningar innehåller en referens till XDM-schemat som begränsar formatet och strukturen för de data som kan lagras. Om du försöker överföra data till en datauppsättning som inte är kompatibel med datauppsättningens XDM-schema kommer det att leda till att importen misslyckas.

Mer information om XDM finns i [XDM-systemöversikt](../../xdm/home.md).

## Samla in data i datauppsättningar

Adobe Experience Platforms datainmatning representerar de olika metoder som används för att importera data från olika källor. Oavsett vilken metod som används konverteras alla importerade data till gruppfiler. Batchar är dataenheter som består av en eller flera filer som ska importeras som en enda enhet. Dessa gruppfiler läggs sedan till i dedikerade datamängder och sparas i datasjön.

Mer information finns i översikten över [](../../ingestion/home.md) datainmatning.

## Använda användningsetiketter på datauppsättningar

Med Adobe Experience Platform Data Governance kan ni hantera kunddata för att säkerställa efterlevnad av regler, begränsningar och policyer som gäller för dataanvändning. Med hjälp av DULE (Data Usage Labeling and Enforcement) som huvudramverk kan du med datastyrning använda användningsetiketter för att kategorisera data enligt de användningsprinciper som gäller för dessa data.

Dataanvändningsetiketter kan användas på hela datauppsättningar eller enskilda datauppsättningsfält. Etiketter som läggs till på datauppsättningsnivå ärvs av alla fält i den datauppsättningen.

Mer information om tjänsten finns i [datastyrningsöversikten](../../data-governance/home.md) . Anvisningar om hur du arbetar med användningsetiketter i användargränssnittet för Experience Platform finns i användarhandboken för [dataanvändningsetiketter](../../data-governance/labels/user-guide.md).

## Datauppsättningar i plattformstjänster längre fram i kedjan

När datauppsättningar har använts för att lagra inkapslade data används dessa datauppsättningar av plattformstjänster längre fram i kedjan för att uppdatera kundprofiler, få insikter via maskininlärning och mycket annat.

Nedan följer en lista över tjänster längre fram i kedjan som använder datauppsättningar för olika åtgärder. Mer information finns i dokumentationen för respektive tjänst.

* [API](../../data-access/home.md)för dataåtkomst: Gör att du kan komma åt och hämta innehållet i filer som lagras i datauppsättningar.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Överbryggar identiteter mellan enheter och system och länkar samman datauppsättningar baserat på de identitetsfält som definieras av XDM-scheman som de följer.
* [Kundprofil](../../profile/home.md)i realtid: Använder Identity Service för att skapa detaljerade kundprofiler från era datauppsättningar i realtid. Realtidskund hämtar data från Data Lake och behåller kundprofiler i sitt eget separata datalager.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Gör att ni kan skapa segment och generera målgrupper utifrån kundprofildata i realtid. Dessa målgrupper kan sedan exporteras till sina egna datamängder inom Data Lake.
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Använder maskininlärning och artificiell intelligens för att identifiera insikter i stora datamängder.
* [Adobe Experience Platform Query Service](../../query-service/home.md): Gör att du kan använda standard-SQL för att fråga efter data i Experience Platform, förena datauppsättningar i Data Lake och samla in frågeresultat som en ny datauppsättning som kan användas för rapportering, Data Science Workspace eller kundprofil i realtid.
* [Adobe Experience Platform Decision Service](../../decisioning-service/home.md): Utnyttjar kundprofilen i realtid för att avgöra vilket alternativ en kund troligtvis kommer att göra utifrån en uppsättning alternativ, baserat på de beteendedata som profilen hämtar från aktiverade datauppsättningar.

## Nästa steg

Genom att läsa det här dokumentet har du introducerats till de viktigaste användningsområdena för datauppsättningar i Experience Platform, samt till de olika plattformstjänster som använder datauppsättningar. Mer information om de många sätt som datauppsättningar används på i Platform finns i servicedokumentationen som är länkad i den här översikten.

Anvisningar om hur du interagerar med datauppsättningar i användargränssnittet för Experience Platform finns i användarhandboken för [datauppsättningar](user-guide.md).