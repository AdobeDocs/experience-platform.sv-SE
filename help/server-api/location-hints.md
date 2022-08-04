---
title: Platstips
description: I den här artikeln beskrivs hur platstips fungerar i Edge Network Server API, så att slutanvändarförfrågningar alltid kan dirigeras till samma server.
source-git-commit: 7f1d8fba34c5478f0d6e727a5a52af642852c9dd
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---


# Platstips

## Översikt {#overview}

The [!DNL Adobe Experience Platform Edge Network] använder flera globalt distribuerade servrar för att säkerställa snabba svarstider oavsett var slutanvändaren befinner sig. Den använder också DNS-baserad routning för att säkerställa att begäranden alltid dirigeras till den Edge Network-plats som är närmast slutanvändarna.

Om slutanvändarna ansluter till ett VPN-nätverk eller byter nätverkstyper på sina mobila enheter under en session, kan förfrågningar från Edge Network ofta dirigeras till en annan plats. Det kan vara problematiskt att routa mellan servrar under flera sessioner eftersom Adobe Experience Platform- och Adobe Experience Cloud-lösningar lagrar slutanvändarprofilsinformation på Edge Network.

Det är här som platstipsen spelas upp.

För att säkerställa att slutanvändarna alltid interagerar med den regionala edge-nätverksservern som innehåller sina aktuella profildata ser funktionen för platstips till att alla begäranden till Edge Network skickas till samma server som den första begäran om en session gjordes. Detta gör att användarna får en enhetlig upplevelse, oavsett vilka nätverksändringar de får uppleva under en session.

## Användning av platstips

Platstips ingår i svaret på den initiala Edge Network-begäran och i alla efterföljande begäranden, vilket visas i exemplet nedan:

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

The `EdgeNetwork` omfånget innehåller all relevant information som Edge Network behöver för att skicka efterföljande begäranden i enlighet med detta. Som svar på den initiala och varje efterföljande begäran till Edge-nätverket finns det ett avsnitt i handtaget med en typ av `locationHint:result`.

Tipset som är associerat med `EdgeNetwork` omfånget kan innehålla något av följande värden:

* `or2`
* `va6`
* `irl1`
* `ind1`
* `jpn3`
* `sgp3`
* `aus3`

**API-format**

Om du vill vara säker på att efterföljande begäranden dirigeras korrekt infogar du platstipset i URL-sökvägen för efterföljande API-anrop mellan bassökvägen, vanligtvis `ee`och `v2` API-version.

```http
POST 'https://edge.adobedc.net/ee/{LOCATION_HINT}/v2/interact?dataStreamId={DataStream_ID}'
```

## Lagra platstips i cookies {#storing-hints-in-cookies}

För att säkerställa att det platstips som returneras av Edge Network finns kvar under hela sessionen kan du lagra platstipsvärdet i en cookie, tillsammans med cookie-livstiden som finns i `ttlSeconds` fält (vanligtvis 1 800 sekunder).

Precis som med de flesta cookies bör du förlänga den här cookie-filens livstid varje gång ett svar från Edge Network uppstår. Använd cookie-namnet för att säkerställa maximal kompatibilitet med Web SDK `kndctr_{IMSORG}_AdobeOrg_cluster`. IMS-organisationsnummer avslutas vanligtvis med `@AdobeOrg`. The `@` värdet måste konverteras till ett understreck för att cookien ska ha rätt format.
