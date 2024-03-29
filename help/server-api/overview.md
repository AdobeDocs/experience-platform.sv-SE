---
title: API-översikt för Edge Network Server
description: Lär dig vad API:t för Edge Network Server är och hur du kan använda det.
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# API-översikt för Edge Network Server {#overview}

Adobe Experience Platform Edge Network är ett optimerat sätt för kunder att interagera med alla Adobe Experience Cloud- och Adobe Experience Platform Edge-tjänster.

The [!DNL Edge Network Server API] kan användas för olika typer av datainsamling, personalisering, annonsering och marknadsföring. The [!DNL Server API] kan användas på servrar, [!DNL IoT] enheter, digitalboxar och andra enheter.

Sedan [!DNL Server API] förlitar sig inte på att några bibliotek laddas, utan är ett blixtsnabbt sätt att interagera med Adobe Experience Platform Edge Network och lösningar som stöds.

Fördelarna med [!DNL Server API] arkitekturen innefattar:

* Minskad sidladdningstid
* Förbättrad latens
* Insamling av data från första part
* Effektiv kommunikation på serversidan mellan tjänster

The [!DNL Server API] har stöd för interaktiv datainsamling och batchdatainsamling via två dedikerade slutpunkter:

1. Den interaktiva slutpunkten har stöd för kommunikation med Adobe Experience Platform- och Adobe Experience Cloud-tjänster som stöder avancerad segmentering, personalisering och andra användningsfall inom marknadsföring.
2. Batchslutpunkten tillåter att begäranden skickas i batch när data måste sparas utan att något svar från de program som anropas tas emot.

The [!DNL Server API] stöder följande typer av begäranden:

* Autentiserade begäranden via [Adobe Developer](https://developer.adobe.com/), med `server.adobedc.net` slutpunkt.
* Oautentiserade begäranden via `edge.adobedc.net` slutpunkt.

Detta möjliggör användning som möjliggör säker, autentiserad insamling av känsliga data, i enlighet med organisationens sekretesspolicy. Förutom autentisering stöder Server-API:t märkning av datastreams så att endast autentiserad kommunikation via API accepteras.

I videon nedan visas en smidig översikt över Server-API:t.

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
