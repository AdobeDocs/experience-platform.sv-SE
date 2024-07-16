---
keywords: Experience Platform;hem;populära ämnen;katalogtjänst;katalog;katalogtjänst;dataplats;dataplats;datahantering;datahantering;rad;rad;katalog;aktivera datauppsättning
solution: Experience Platform
title: Katalogtjänst - översikt
description: Katalogtjänsten är arkivsystemet för dataplatser och -länkar inom Adobe Experience Platform. Alla data som importeras till Experience Platform lagras i Data Lake som filer och kataloger, men i Catalog finns metadata och beskrivning för dessa filer och kataloger för sökning och övervakning.
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
source-git-commit: 0ebe9eadb1bce6252b43a50af009ce1b0f6e5d6e
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# [!DNL Catalog Service] översikt

[!DNL Catalog Service] är arkivsystemet för dataplatser och datalänkning inom Adobe Experience Platform. Alla data som är inkapslade i [!DNL Experience Platform] lagras i [!DNL Data Lake] som filer och kataloger, men i [!DNL Catalog] lagras metadata och beskrivning för dessa filer och kataloger för sökning och övervakning.

Kort sagt fungerar [!DNL Catalog] som ett metadataarkiv eller en katalog där du kan hitta information om dina data i [!DNL Experience Platform]. Du kan använda [!DNL Catalog] för att svara på följande frågor:

* Var finns mina data?
* I vilket skede av bearbetningen befinner sig dessa data?
* Vilka system eller processer har använt mina data?
* Hur mycket data har bearbetats?
* Vilka fel uppstod under bearbetningen?

[!DNL Catalog] innehåller ett RESTful-API som gör att du kan hantera [!DNL Platform]-metadata programmatiskt med grundläggande CRUD-åtgärder. Mer information finns i [Utvecklarhandboken för ](api/getting-started.md).

## [!DNL Catalog] och [!DNL Experience Platform] tjänster

Resurserna som [!DNL Catalog Service] spårar används av flera [!DNL Experience Platform]-tjänster. För att få ut så mycket som möjligt av [!DNL Catalog's]-funktionerna rekommenderar vi att du lär dig mer om dessa tjänster och hur de interagerar med [!DNL Catalog].

### [!DNL Experience Data Model] (XDM) system

[!DNL Experience Data Model] (XDM) System är det standardiserade ramverk som [!DNL Platform] organiserar kundupplevelsedata med. [!DNL Experience Platform] använder XDM-scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt.

När data hämtas till [!DNL Platform] mappas datastrukturen till ett XDM-schema och lagras i [!DNL Data Lake] som en del av en datamängd. Metadata för varje datauppsättning spåras av [!DNL Catalog Service], som innehåller en referens till XDM-schemat som datauppsättningen följer.

Mer allmän information om XDM System finns i [XDM System overview](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] importerar data från flera källor och behåller poster som datauppsättningar i [!DNL Data Lake]. [!DNL Catalog] spårar metadata för dessa datauppsättningar, oavsett källa eller metod för intaget.

När du använder gruppbearbetningsmetoden spårar [!DNL Catalog] även ytterligare metadata för gruppfiler. Batchar är dataenheter som består av en eller flera filer som ska importeras som en enda enhet. [!DNL Catalog] spårar metadata för dessa gruppfiler samt de datauppsättningar som de sparas i efter att de har importerats. Batchmetadata innehåller information om antalet poster som har importerats samt eventuella poster som misslyckades och associerade felmeddelanden.

Mer information finns i [översikten över dataöverföring](../ingestion/home.md).

## [!DNL Catalog] objekt

Så som beskrivs i föregående avsnitt spårar [!DNL Catalog] metadata för flera typer av resurser och åtgärder som används av andra [!DNL Platform]-tjänster. [!DNL Catalog] underhåller en egen lagringsplats med&quot;objekt&quot; som kapslar in dessa metadata. [!DNL Catalog]-objekt är frågningsbara representationer av [!DNL Platform]-data som gör att du kan söka efter, övervaka och etikettera dina data utan att behöva komma åt själva data.

I följande tabell visas de olika objekttyper som stöds av [!DNL Catalog]:

| Objekt | API-slutpunkt | Definition |
|---|---|---|
| Grupp | `/batches` | Batchar är dataenheter som består av en eller flera filer som ska importeras som en enda enhet. Ett batchobjekt i [!DNL Catalog] visar batchens användningsmått (till exempel antalet poster som bearbetas eller storleken på disken) och kan även innehålla länkar till datauppsättningar, vyer och andra resurser som påverkats av batchåtgärden. |
| Datauppsättning | `/dataSets` | En datauppsättning är en lagrings- och hanteringskonstruktion som används för datainsamling (vanligtvis en tabell) som innehåller ett schema (kolumner) och fält (rader). Mer information finns i [översikten över datauppsättningar](./datasets/overview.md). |
| Datauppsättningsfil | `/datasetFiles` | Datauppsättningsfiler representerar datablock som har sparats på [!DNL Platform]. Som poster för litterala filer är det här du kan hitta filens storlek, antalet poster som den innehåller och en referens till den grupp som importerade filen. |

## Nästa steg

Det här dokumentet innehåller en introduktion till [!DNL Catalog Service] och hur det fungerar i det större omfånget av [!DNL Experience Platform]. I [[!DNL Catalog] utvecklarhandboken](api/getting-started.md) finns anvisningar om hur du interagerar med de olika slutpunkterna i det [!DNL Catalog] API:t. Vi rekommenderar att du även refererar till guiden [filtrera katalogdata](api/filter-data.md) för att följa bästa praxis för att begränsa vilka data som returneras i API-svar.
