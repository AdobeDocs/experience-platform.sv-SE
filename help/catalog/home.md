---
keywords: Experience Platform;home;popular topics;catalog service;catalog;Catalog service;data location;Data Location;Data management;data management;Lineage;lineage;Catalog;enable dataset
solution: Experience Platform
title: Katalogtjänst - översikt
topic: overview
description: Katalogtjänsten är arkivsystemet för dataplatser och -länkar inom Adobe Experience Platform. Alla data som importeras till Experience Platform lagras i Data Lake som filer och kataloger, men i Catalog finns metadata och beskrivning för dessa filer och kataloger för sökning och övervakning.
translation-type: tm+mt
source-git-commit: 34cfcaac276bf2645a0365a0dfa71c4ead6e2ecb
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 0%

---


# [!DNL Catalog Service] översikt

[!DNL Catalog Service] är registersystemet för dataplatser och datalinje inom Adobe Experience Platform. Alla data som är inkapslade i [!DNL Experience Platform] lagras i [!DNL Data Lake] som filer och kataloger, men [!DNL Catalog] innehåller metadata och beskrivning för dessa filer och kataloger för sökning och övervakning.

Kort och gott: fungerar som ett metadataarkiv eller&quot;katalog&quot; där du kan hitta information om dina data [!DNL Catalog] [!DNL Experience Platform]. Du kan använda [!DNL Catalog] för att svara på följande frågor:

* Var finns mina data?
* I vilket skede av bearbetningen befinner sig dessa data?
* Vilka system eller processer har använt mina data?
* Hur mycket data har bearbetats?
* Vilka fel uppstod under bearbetningen?

[!DNL Catalog] innehåller ett RESTful-API som gör att du kan hantera [!DNL Platform] metadata med hjälp av grundläggande CRUD-åtgärder. Mer information finns i [Katalogutvecklarhandboken](api/getting-started.md) .

## [!DNL Catalog] och [!DNL Experience Platform] tjänster

Resurserna som [!DNL Catalog Service] spårar används av flera [!DNL Experience Platform] tjänster. För att få ut så mycket som möjligt av [!DNL Catalog's] funktionerna rekommenderar vi att du lär dig mer om dessa tjänster och hur de interagerar med [!DNL Catalog].

### [!DNL Experience Data Model] (XDM) System

[!DNL Experience Data Model] (XDM) System är det standardiserade ramverk som [!DNL Platform] organiserar kundupplevelsedata. [!DNL Experience Platform] utnyttjar XDM-scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt.

När data hämtas in till [!DNL Platform]mappas datastrukturen till ett XDM-schema och lagras i [!DNL Data Lake] som en del av en datauppsättning. Metadata för varje datauppsättning spåras av [!DNL Catalog Service], som innehåller en referens till XDM-schemat som datauppsättningen följer.

Mer allmän information om XDM System finns i [XDM-systemöversikten](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] importerar data från flera källor och behåller poster som datauppsättningar i [!DNL Data Lake]. [!DNL Catalog] spårar metadata för dessa datauppsättningar, oavsett källa eller metod för intaget.

När du använder gruppbearbetningsmetoden spåras även ytterligare metadata för gruppfiler [!DNL Catalog] . Batchar är dataenheter som består av en eller flera filer som ska importeras som en enda enhet. [!DNL Catalog] spårar metadata för dessa gruppfiler samt de datauppsättningar som de sparas i efter inmatning. Batchmetadata innehåller information om antalet poster som har importerats samt eventuella poster som misslyckades och associerade felmeddelanden.

Mer information finns i översikten över [](../ingestion/home.md) dataöverföring.

## [!DNL Catalog] objekt

Så som beskrivs i föregående avsnitt spårar metadata för flera olika typer av resurser och åtgärder som används av andra [!DNL Catalog] [!DNL Platform] tjänster. [!DNL Catalog] har ett eget arkiv med&quot;objekt&quot; som kapslar in dessa metadata. [!DNL Catalog] -objekt är sökbara representationer av data som gör att du kan söka efter, övervaka och märka data utan att behöva komma åt själva data. [!DNL Platform]

I följande tabell visas de olika objekttyper som stöds av [!DNL Catalog]:

| Objekt | API-slutpunkt | Definition |
|---|---|---|
| Konto | `/accounts` | Autentiseringsuppgifter måste anges när du skapar källanslutningar. Ett konto representerar en samling autentiseringsuppgifter som användes för att skapa en anslutning av en viss typ. Varje anslutning har en uppsättning unika parametrar som bevaras av [!DNL Catalog] och skyddas i en [!DNL Azure Key Vault]. |
| Grupp | `/batches` | Batchar är dataenheter som består av en eller flera filer som ska importeras som en enda enhet. Ett batchobjekt i [!DNL Catalog] visar batchens användningsmått (till exempel antalet poster som bearbetas eller storleken på disken) och kan även innehålla länkar till datauppsättningar, vyer och andra resurser som påverkades av batchåtgärden. |
| Anslutning | `/connections` | En anslutning är en enda instans av en källanslutning som är unik för din organisation och konfigurerad med lämpliga autentiseringsuppgifter för anslutningstypen. |
| Koppling | `/connectors` | Kopplingar definierar hur källanslutningar ska användas för att samla in data från andra Adobe-program (t.ex. Adobe Analytics och Adobe Audience Manager), molnlagringskällor från tredje part (t.ex. [!DNL Azure Blob], [!DNL Amazon S3]FTP-servrar och SFTP-servrar) och CRM-system från tredje part (t.ex. [!DNL Microsoft Dynamics] och [!DNL Salesforce]). |
| Datauppsättning | `/dataSets` | En datauppsättning är en lagrings- och hanteringskonstruktion som används för datainsamling (vanligtvis en tabell) som innehåller ett schema (kolumner) och fält (rader). Mer information finns i översikten över [datauppsättningar](./datasets/overview.md) . |
| Datauppsättningsfil | `/datasetFiles` | Datauppsättningsfiler representerar datablock som har sparats i [!DNL Platform]. Som poster för litterala filer är det här du kan hitta filens storlek, antalet poster som den innehåller och en referens till den grupp som importerade filen. |

## Nästa steg

Det här dokumentet innehåller en introduktion till [!DNL Catalog Service] och hur det fungerar inom det större omfånget av [!DNL Experience Platform]. Se [[!DNL Catalog] utvecklarhandboken](api/getting-started.md) för steg om hur du interagerar med de olika slutpunkterna i det [!DNL Catalog] API:t. Vi rekommenderar att du också läser guiden om [filtrering av katalogdata](api/filter-data.md) för att följa vedertagna standarder för att begränsa vilka data som returneras i API-svar.