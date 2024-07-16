---
title: Platstips
description: I den här artikeln beskrivs hur platstips fungerar i Edge Network Server API, så att slutanvändarförfrågningar alltid kan dirigeras till samma server.
exl-id: 8cd2f8e2-2065-4b7e-8d35-4ed1a716f1b3
source-git-commit: 2c7a5f007189d897ed32302a2a80c1e16af6af80
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# Platstips

## Översikt {#overview}

[!DNL Adobe Experience Platform Edge Network] använder flera globalt distribuerade servrar för att säkerställa snabba svarstider oavsett slutanvändarens plats. Den använder också DNS-baserad routning för att säkerställa att begäranden alltid dirigeras till den plats i Edge Network som är närmast slutanvändarna.

Om slutanvändarna ansluter till ett VPN-nätverk eller byter nätverkstyper på sina mobila enheter under en session, kan förfrågningar från Edge Network ofta dirigeras till en annan plats. Det kan vara problematiskt att routning mellan servrar mellan sessioner eftersom Adobe Experience Platform och Adobe Experience Cloud lagrar slutanvändarprofilsinformation på Edge Network.

Det är här som platstipsen spelas upp.

För att slutanvändarna alltid ska kunna interagera med den Edge Network-regionala server som innehåller deras aktuella profildata, ser funktionen för platstips till att alla begäranden till Edge Network skickas till samma server som den första begäran om en session gjordes. Detta gör att användarna får en enhetlig upplevelse, oavsett vilka nätverksändringar de får uppleva under en session.

## Användning av platstips

Platstips ingår i svaret på den ursprungliga Edge Network-begäran och i alla efterföljande förfrågningar, vilket visas i exemplet nedan:

```json
{
   "payload":[
      {
         "scope":"EdgeNetwork",
         "hint":"or2",
         "ttlSeconds":1800
      }
   ],
   "type":"locationHint:result"
}
```

Omfånget `EdgeNetwork` innehåller all relevant information som Edge Network behöver för att skicka efterföljande begäranden i enlighet med detta. Som svar på den initiala och efterföljande begäran till Edge-nätverket finns det ett avsnitt i referensen med typen `locationHint:result`.

Tipset som är associerat med omfånget `EdgeNetwork` kan innehålla något av följande värden:

* `or2`
* `va6`
* `irl1`
* `ind1`
* `jpn3`
* `sgp3`
* `aus3`

**API-format**

Om du vill vara säker på att efterföljande begäranden dirigeras korrekt infogar du platstipset i URL-sökvägen för efterföljande API-anrop mellan bassökvägen, vanligtvis `ee`, och `v2` API-version.

```http
POST 'https://edge.adobedc.net/ee/{LOCATION_HINT}/v2/interact?dataStreamId={DataStream_ID}'
```

## Lagra platstips i cookies {#storing-hints-in-cookies}

Om du vill vara säker på att platstipset som returneras av Edge Network finns kvar under hela sessionen kan du lagra platstipsets värde i en cookie, tillsammans med cookie-livstiden som finns i fältet `ttlSeconds` (vanligtvis 1 800 sekunder).

Precis som med de flesta cookies bör du förlänga den här kakans livstid varje gång det kommer ett svar från Edge Network. Använd cookie-namnet `kndctr_{IMSORG}_AdobeOrg_cluster` för att säkerställa maximal kompatibilitet med Web SDK. Organisations-ID:n avslutas vanligtvis med `@AdobeOrg`. Värdet `@` måste konverteras till ett understreck för att cookien ska ha rätt format.
