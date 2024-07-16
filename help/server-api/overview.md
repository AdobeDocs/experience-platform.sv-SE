---
title: API-översikt för Edge Network Server
description: Lär dig vad Edge Network Server-API:t är och hur du kan använda det.
exl-id: 46bd8798-d7f9-405b-9ca8-856ad4aa688c
source-git-commit: 041a1782442df5f08bb52e4e450734a51c7781ea
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# API-översikt för Edge Network Server {#overview}

Adobe Experience Platform Edge Network är ett optimerat sätt för kunderna att interagera med alla Adobe Experience Cloud- och Adobe Experience Platform Edge-tjänster.

[!DNL Edge Network Server API] kan användas för olika typer av datainsamling, personalisering, annonsering och marknadsföring. [!DNL Server API] kan användas på servrar, [!DNL IoT]-enheter, digitalboxar och andra enheter.

Eftersom [!DNL Server API] inte förlitar sig på att några bibliotek ska läsas in är det ett blixtsnabbt sätt att interagera med Adobe Experience Platform Edge Network och lösningar som stöds.

Fördelarna med arkitekturen [!DNL Server API] är bland annat:

* Minskad sidladdningstid
* Förbättrad latens
* Insamling av data från första part
* Effektiv kommunikation på serversidan mellan tjänster

[!DNL Server API] har stöd för interaktiv datainsamling och batchdatainsamling, via två dedikerade slutpunkter:

1. Den interaktiva slutpunkten har stöd för kommunikation med Adobe Experience Platform- och Adobe Experience Cloud-tjänster som stöder avancerad segmentering, personalisering och andra användningsfall inom marknadsföring.
2. Batchslutpunkten tillåter att begäranden skickas i batch när data måste sparas utan att något svar från de program som anropas tas emot.

[!DNL Server API] stöder följande typer av begäranden:

* Autentiserade begäranden via [Adobe Developer](https://developer.adobe.com/) med slutpunkten `server.adobedc.net`.
* Oautentiserade begäranden via slutpunkten `edge.adobedc.net`.

Detta möjliggör användning som möjliggör säker, autentiserad insamling av känsliga data, i enlighet med organisationens sekretesspolicy. Förutom autentisering stöder Server-API:t märkning av datastreams så att endast autentiserad kommunikation via API accepteras.

I videon nedan visas en smidig översikt över Server-API:t.

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
