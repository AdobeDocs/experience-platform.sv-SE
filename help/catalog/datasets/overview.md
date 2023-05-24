---
keywords: Experience Platform;hem;populära ämnen;dataplats;dataplats;datahantering;datahantering;rad;rad;datatyp;datatyp;datatyper;datatyp
solution: Experience Platform
title: Datauppsättningar - översikt
description: Det här dokumentet innehåller en översikt på hög nivå över datauppsättningar i Experience Platform.
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: dca5c9df82434d75238a0a80f15e5562cf2fa412
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 2%

---

# Översikt över datauppsättningar

Alla data som har importerats till Adobe Experience Platform lagras i [!DNL Data Lake] som datauppsättningar. En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell, som innehåller ett schema (kolumner) och fält (rader). Datauppsättningar innehåller också metadata som beskriver olika aspekter av de data som lagras.

Det här dokumentet innehåller en översikt på hög nivå över datauppsättningar i [!DNL Experience Platform].

## Skapa datauppsättningar och spåra metadata

[!DNL Catalog Service] är systemet för registrering av dataplatser och -rader inom [!DNL Experience Platform]och används för att skapa och hantera datauppsättningar. [!DNL Catalog] spårar metadata för varje datauppsättning, som innehåller en referens till [!DNL Experience Data Model] (XDM)-schema som datauppsättningen följer (förklaras i nästa avsnitt) och antalet poster som hämtas till den datauppsättningen.

Se [Katalogtjänst - översikt](../home.md) för mer information.

## Tvingande begränsningar för datauppsättningsdata

[!DNL Experience Data Model] (XDM) är det standardiserade ramverk som [!DNL Platform] organiserar kundupplevelsedata. Alla data som har importerats till [!DNL Platform] måste följa ett fördefinierat XDM-schema innan det kan sparas i [!DNL Data Lake] som en datauppsättning.

Alla datauppsättningar innehåller en referens till XDM-schemat som begränsar formatet och strukturen för de data som kan lagras. Om du försöker överföra data till en datauppsättning som inte är kompatibel med datauppsättningens XDM-schema kommer det att leda till att importen misslyckas.

Mer information om XDM finns i [XDM - systemöversikt](../../xdm/home.md).

## Samla in data i datauppsättningar

Adobe Experience Platform datainmatning representerar de olika metoder som [!DNL Platform] importerar data från olika källor. Oavsett vilken metod som används konverteras alla importerade data till gruppfiler. Batchar är dataenheter som består av en eller flera filer som ska importeras som en enda enhet. Dessa gruppfiler läggs sedan till i dedikerade datauppsättningar och sparas i [!DNL Data Lake].

Se [Översikt över datainmatning](../../ingestion/home.md) för mer information.

## Etiketter som tillämpas på datauppsättningar från scheman

Med Adobe Experience Platform Data Governance kan ni hantera kunddata för att säkerställa efterlevnad av regler, begränsningar och policyer som gäller för dataanvändning. Med ramverket för datastyrning kan du använda användningsetiketter för att kategorisera data enligt de användningsprinciper som gäller för dessa data. Etiketter kan användas på enskilda scheman, fält inom dessa scheman och hela enskilda datauppsättningar. När etiketter används direkt i ett schema sprids dessa etiketter till alla befintliga och framtida datauppsättningar som baseras på det schemat.

>[!IMPORTANT]
>
>Etiketter kan inte längre användas på fält på datauppsättningsnivå. Det här arbetsflödet har ersatts med etiketter på schemanivå. Etiketter som tidigare använts på datauppsättningens objektnivå stöds fortfarande i plattformsgränssnittet fram till den 31 maj 2024. För att etiketterna ska vara enhetliga i alla scheman måste du migrera alla etiketter som tidigare har kopplats till fält på datauppsättningsnivå till schemanivån under det kommande året. Se avsnittet om [migrera tidigare använda etiketter](../../data-governance/e2e.md#migrate-labels) för instruktioner om hur man gör detta.

Se [Datastyrning - översikt](../../data-governance/home.md) för mer information om tjänsten. Anvisningar om hur du arbetar med användningsetiketter i [!DNL Platform]finns i följande handledningar:

* [Hantera etiketter i användargränssnittet](../../data-governance/labels/user-guide.md)
* [Hantera datauppsättningsrubriker i API](../../data-governance/labels/dataset-api.md)

## Datauppsättningar i underordnade [!DNL Platform] tjänster

När datauppsättningar har använts för att lagra inkapslade data, används dessa datauppsättningar av underordnade [!DNL Platform] tjänster för att uppdatera kundprofiler, få insikter via maskininlärning och mycket annat.

Nedan följer en lista över tjänster längre fram i kedjan som använder datauppsättningar för olika åtgärder. Mer information finns i dokumentationen för respektive tjänst.

* [[!DNL Data Access API]](../../data-access/home.md): Gör att du kan komma åt och hämta innehållet i filer som lagras i datauppsättningar.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Överbryggar identiteter mellan enheter och system och länkar samman datauppsättningar baserat på de identitetsfält som definieras av XDM-scheman som de följer.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Utnyttja [!DNL Identity Service] för att skapa detaljerade kundprofiler utifrån era datauppsättningar i realtid. [!DNL Real-Time Customer Profile] hämtar data från [!DNL Data Lake] och behåller kundprofiler i sitt eget separata datalager.
* [Adobe Experience Platform segmenteringstjänst](../../segmentation/home.md): Gör att ni kan skapa segment och generera målgrupper utifrån era [!DNL Real-Time Customer Profile] data. Dessa målgrupper kan sedan exporteras till sina egna datauppsättningar i [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Använder maskininlärning och artificiell intelligens för att identifiera insikter i stora datamängder.
* [Adobe Experience Platform Query Service](../../query-service/home.md): Gör att du kan använda standard-SQL för att fråga data i [!DNL Experience Platform], koppla alla datauppsättningar i [!DNL Data Lake] och hämta frågeresultat som en ny datamängd som kan användas vid rapportering, [!DNL Data Science Workspace], eller [!DNL Real-Time Customer Profile].
* [Adobe Experience Platform Destinationstjänst](../../destinations/home.md): Gör att du kan [exportera datamängder](/help/destinations/ui/export-datasets.md) till det molnlagringsutrymme eller e-postmarknadsföringsmål du vill ha för rapporter och datavetenskapliga aktiviteter.

## Nästa steg

Genom att läsa det här dokumentet har du introducerats i de viktigaste användningsområdena för datauppsättningar i [!DNL Experience Platform], samt de olika [!DNL Platform] tjänster som använder datauppsättningar. Mer information finns i [!DNL Platform], läs igenom servicedokumentationen som är länkad i denna översikt.

För steg om hur du interagerar med datauppsättningar i [!DNL Experience Platform] Gränssnitt, se [användarhandbok för datauppsättningar](user-guide.md).
