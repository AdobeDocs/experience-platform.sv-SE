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

[!DNL Catalog Service] är registersystemet för dataplatser och datalinje inom Adobe Experience Platform. Alla data som hämtas in till [!DNL Experience Platform] lagras i [!DNL Data Lake] som filer och kataloger, [!DNL Catalog] innehåller metadata och beskrivning av dessa filer och kataloger för sökning och övervakning.

Enkelt uttryckt [!DNL Catalog] fungerar som ett metadataarkiv eller en katalog där du kan hitta information om dina data i [!DNL Experience Platform]. Du kan använda [!DNL Catalog] svara på följande frågor:

* Var finns mina data?
* I vilket skede av bearbetningen befinner sig dessa data?
* Vilka system eller processer har använt mina data?
* Hur mycket data har bearbetats?
* Vilka fel uppstod under bearbetningen?

[!DNL Catalog] innehåller ett RESTful-API som gör att du kan hantera programmässigt [!DNL Platform] metadata med grundläggande CRUD-åtgärder. Se [Utvecklarhandbok för kataloger](api/getting-started.md) för mer information.

## [!DNL Catalog] och [!DNL Experience Platform] tjänster

Resurserna som [!DNL Catalog Service] spår används av flera [!DNL Experience Platform] tjänster. För att få ut det mesta av [!DNL Catalog's] vi rekommenderar att du bekanta dig med dessa tjänster och hur de interagerar med [!DNL Catalog].

### [!DNL Experience Data Model] (XDM) System

[!DNL Experience Data Model] (XDM) System är det standardiserade ramverk som [!DNL Platform] organiserar kundupplevelsedata. [!DNL Experience Platform] utnyttjar XDM-scheman för att beskriva datastrukturen på ett konsekvent och återanvändbart sätt.

När data hämtas till [!DNL Platform], mappas datastrukturen till ett XDM-schema och lagras i [!DNL Data Lake] som en del av en datauppsättning. Metadata för varje datauppsättning spåras av [!DNL Catalog Service], som innehåller en referens till XDM-schemat som datauppsättningen följer.

Mer allmän information om XDM System finns i [XDM - systemöversikt](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] importerar data från flera källor och behåller poster som datauppsättningar i [!DNL Data Lake]. [!DNL Catalog] spårar metadata för dessa datauppsättningar, oavsett källa eller metod för intaget.

När du använder batchmatningsmetoden, [!DNL Catalog] spårar även ytterligare metadata för gruppfiler. Batchar är dataenheter som består av en eller flera filer som ska importeras som en enda enhet. [!DNL Catalog] spårar metadata för dessa gruppfiler samt de datauppsättningar som de sparas i efter inmatning. Batchmetadata innehåller information om antalet poster som har importerats samt eventuella poster som misslyckades och associerade felmeddelanden.

Se [dataöverföring - översikt](../ingestion/home.md) för mer information.

## [!DNL Catalog] objekt

Enligt beskrivningen i föregående avsnitt [!DNL Catalog] spårar metadata för flera typer av resurser och åtgärder som används av andra [!DNL Platform] tjänster. [!DNL Catalog] har ett eget arkiv med&quot;objekt&quot; som kapslar in dessa metadata. [!DNL Catalog] objekt är sökbara representationer av [!DNL Platform] data som gör att du kan söka efter, övervaka och etikettera data utan att behöva komma åt själva data.

I följande tabell visas de olika objekttyper som stöds av [!DNL Catalog]:

| Objekt | API-slutpunkt | Definition |
|---|---|---|
| Grupp | `/batches` | Batchar är dataenheter som består av en eller flera filer som ska importeras som en enda enhet. Ett batchobjekt i [!DNL Catalog] sammanfattar batchens användningsmått (t.ex. antalet poster som bearbetas eller storleken på disken) och kan även innehålla länkar till datauppsättningar, vyer och andra resurser som påverkades av batchåtgärden. |
| Datauppsättning | `/dataSets` | En datauppsättning är en lagrings- och hanteringskonstruktion som används för datainsamling (vanligtvis en tabell) som innehåller ett schema (kolumner) och fält (rader). Se [datauppsättningar, översikt](./datasets/overview.md) för mer information. |
| Datauppsättningsfil | `/datasetFiles` | Datauppsättningsfiler representerar datablock som har sparats på [!DNL Platform]. Som poster för litterala filer är det här du kan hitta filens storlek, antalet poster som den innehåller och en referens till den grupp som importerade filen. |

## Nästa steg

Det här dokumentet innehåller en introduktion till [!DNL Catalog Service] och hur det fungerar i större utsträckning [!DNL Experience Platform]. Se [[!DNL Catalog] utvecklarhandbok](api/getting-started.md) för steg för interaktion med de olika slutpunkterna i [!DNL Catalog] API. Vi rekommenderar att du också läser guiden [filtrera katalogdata](api/filter-data.md) för att följa bästa praxis för att begränsa de data som returneras i API-svar.
