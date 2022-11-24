---
title: Översikt över Cloud Connector-tillägg
description: Lär dig mer om tillägget för händelsevidarebefordran i Cloud Connector i Adobe Experience Platform.
exl-id: f3713652-ac32-4171-8dda-127c8c235849
source-git-commit: c7344d0ac5b65c6abae6a040304f27dc7cd77cbb
workflow-type: tm+mt
source-wordcount: '1604'
ht-degree: 0%

---

# Översikt över tillägget Cloud Connector

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Med tillägget för händelsevidarebefordran i Cloud Connector kan du skapa anpassade HTTP-begäranden för att skicka data till ett mål eller hämta data från ett mål. Cloud Connector-tillägget fungerar som att ha Postman på Adobe Experience Platform Edge Network och kan användas för att skicka data till en slutpunkt som ännu inte har något dedikerat tillägg.

Använd den här referensen för information om de alternativ som är tillgängliga när du använder det här tillägget för att skapa en regel.

## Åtgärdstyp för Cloud Connector-tillägg

I det här avsnittet beskrivs åtgärdstypen Skicka data som finns i tillägget Adobe Experience Platform Cloud Connector.

### Typ av begäran

Välj önskad typ av begäran som krävs av slutpunkten under [!UICONTROL Request Type] listruta.

| Metod | Beskrivning |
|---|---|
| [GET](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/GET) | Begär en representation av den angivna resursen. Begäranden som använder GET bör bara hämta data. |
| [POST](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST) | Skickar en entitet till den angivna resursen, vilket ofta orsakar en ändring av tillstånd eller biverkningar på servern. |
| [PUT](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PUT) | Ersätter alla aktuella representationer av målresursen med den begärda nyttolasten. |
| [PATCH](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PATCH) | Tillämpar partiella ändringar på en resurs. |
| [DELETE](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/DELETE) | Tar bort den angivna resursen. |

### URL för slutpunkt

I textfältet bredvid listrutan Typ av begäran anger du URL:en för den slutpunkt som du skickar data till.

### Frågeparametrar, rubriker och innehållskonfiguration

Använd var och en av dessa flikar (Query Params, Headers och Body Data Elements) för att styra vilka data som skickas till en viss slutpunkt.

#### Frågeparametrar

Definiera en nyckel och ett värde för varje nyckelvärdepar som du vill skicka som en frågesträngsparameter. Om du vill ange ett dataelement manuellt använder du klammerparentesens dataelementtokenisering för vidarebefordran av händelser. Om du vill referera till värdet för ett dataelement med namnet&quot;siteSection&quot; som en nyckel eller ett värde anger du `{{siteSection}}`. Du kan också markera det dataelement som skapades tidigare genom att markera det i listrutan.

Om du vill lägga till fler frågeparametrar väljer du **[!UICONTROL Add Another]**.

#### Sidhuvuden

Definiera en nyckel och ett värde för varje nyckelvärdepar som du vill skicka som en rubrik. Om du vill ange ett dataelement manuellt använder du klammerparentesens dataelementtokenisering för vidarebefordran av händelser. Om du vill referera till värdet för ett dataelement med namnet&quot;pageName&quot; som en nyckel eller ett värde anger du `{{pageName}}`. Du kan också markera det dataelement som skapades tidigare genom att markera det i listrutan.

Om du vill lägga till fler rubriker väljer du **[!UICONTROL Add Another]**.

I följande tabell visas de fördefinierade rubrikerna. Du är inte begränsad till dessa rubriker och kan lägga till egna rubriker om det behövs, men de är tillgängliga för att underlätta.

>[!NOTE]
>
>Mer information om dessa rubriker finns på [https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers).

| Sidhuvud | Beskrivning |
|---|---|
| [A-IM](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept) |  |
| [Acceptera](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept) |  |
| [Accept-Charset](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Charset) |  |
| [Acceptera-kodning](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Encoding) |  |
| [Acceptera språk](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Language) |  |
| [Accept-DateTime](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept) | Överförd av en användaragent för att ange att den vill komma åt ett tidigare tillstånd för en ursprunglig resurs. För att uppnå detta `Accept-Datetime` huvudet förmedlas i en HTTP-begäran som utfärdas mot en TimeGate för en ursprunglig resurs, och dess värde anger datum/tid för det önskade tidigare tillståndet för den ursprungliga resursen. |
| Access-control-request-headers | Används av webbläsare vid utfärdande av en [preflight-förfrågan](https://developer.mozilla.org/en-US/docs/Glossary/preflight_request)för att tala om för servern vilken [HTTP-huvuden](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers) klienten kan skicka när den faktiska begäran har gjorts. |
| access-control-request-method | Används av webbläsare vid utfärdande av en [preflight-förfrågan](https://developer.mozilla.org/en-US/docs/Glossary/preflight_request)för att tala om för servern vilken [HTTP-metod](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods) kommer att användas när den faktiska begäran görs. Den här rubriken är nödvändig eftersom preflight-begäran alltid är en [ALTERNATIV](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/OPTIONS) och använder inte samma metod som den faktiska begäran. |
| Behörighet | Innehåller autentiseringsuppgifter för att autentisera en användaragent med en server. |
| [Cache-Control](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control) | Direktiv om mekanismer för cachelagring i både förfrågningar och svar. |
| [Anslutning](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Connection) | Kontrollerar om nätverksanslutningen förblir öppen när den aktuella transaktionen har slutförts. |
| [Content-Length](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Length) | Resursens storlek i antal byte. |
| [Content-Type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type) | Anger medietypen för resursen. |
| Cookie | Innehåller lagrade [HTTP-cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies) som tidigare skickats av servern med [`Set-Cookie`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie) header. |
| Datum | Allmän HTTP-rubrik innehåller datum och tid då meddelandet skapades. |
| [DNT](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/DNT) | Uttrycker användarens spårningsinställning. |
| Förvänta | Anger förväntningar som servern måste uppfylla för att kunna hantera begäran korrekt. |
| Vidarebefordrad | Innehåller information från [omvända proxyservrar](https://developer.mozilla.org/en-US/docs/Web/HTTP/Proxy_servers_and_tunneling) som ändras eller förloras när en proxy är inblandad i sökvägen till begäran. |
| Från | Innehåller en Internet-e-postadress för en användare som styr den begärande användaragenten. |
| Värd | Anger värd- och portnummer för servern som begäran skickas till. |
| If-Match |  |
| If-Modified-Since |  |
| [If-None-Match](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-None-Match) |  |
| [Om-Intervall](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Range) |  |
| [If-Unmodified-Since](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Unmodified-Since) |  |
| [Max-Forwards](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Unmodified-Since) |  |
| [Ursprung](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Origin) |  |
| [Pragma](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Pragma) | Implementeringsspecifikt huvud som kan ha olika effekter var som helst längs kedjan för begäran/svar. Används för bakåtkompatibilitet med HTTP/1.0-cacheminnen där Cache-Control-huvudet ännu inte finns. |  |
| [Proxyauktorisering](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Proxy-Authorization) |
| [Intervall](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Range) | Anger den del av ett dokument som servern ska returnera. |  |
| [Referent](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer) | Adressen till den föregående webbsidan från vilken en länk till den begärda sidan följdes. |  |
| TE | Anger de överföringskoder som användaragenten är villig att acceptera. (Du kan ringa det elektroniskt `Accept-Transfer-Encoding`, vilket skulle vara mer intuitivt). |
| Uppgradera | Det relevanta RFC-dokumentet för [`Upgrade` rubrikfältet är RFC 7230, avsnitt 6.7](https://tools.ietf.org/html/rfc7230#section-6.7). Standarden innehåller regler för uppgradering eller ändring till ett annat protokoll på den aktuella klient-, server- och transportprotokollanslutningen. Den här huvudstandarden tillåter till exempel en klient att ändra från HTTP 1.1 till HTTP 2.0, förutsatt att servern bestämmer sig för att bekräfta och implementera `Upgrade` rubrikfält. Ingen av parterna behöver acceptera villkoren som anges i `Upgrade` rubrikfält. Den kan användas både i klient- och serverrubriker. Om `Upgrade` huvudfältet anges, sedan MÅSTE avsändaren också skicka `Connection` rubrikfält med `upgrade` angivet alternativ. |  |
| [Användaragent](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent) | Innehåller en karakteristisk sträng som gör att nätverksprotokollets peer-datorer kan identifiera programtyp, operativsystem, programvaruleverantör eller programvaruversion för den begärande programvaruanvändarens agent. |
| [Via](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Via) | Läggs till av proxies, både framåt- och bakåt-proxies, och kan visas i begäranrubrikerna och svarshuvudena. |
| [Varning](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Warning) | Allmän varningsinformation om möjliga problem. |
| X-CSRF-token |  |
| X-requested-with |  |

#### Brödtext som JSON

Definiera en nyckel och ett värde för varje nyckelvärdepar som du vill skicka i själva förfrågningen. Om du vill ange ett dataelement manuellt använder du klammerparentesens dataelementtokenisering för vidarebefordran av händelser. Om du vill referera till värdet för ett dataelement med namnet&quot;appSection&quot; som en nyckel eller ett värde anger du `{{appSection}}`. Du kan också markera det dataelement som skapades tidigare genom att markera det i listrutan.

Om du vill lägga till fler nyckelvärdepar väljer du **[!UICONTROL Add Another]**.

#### Brödtext som Raw

Definiera en nyckel och ett värde för varje nyckelvärdepar som du vill skicka i själva förfrågningen. Om du vill ange ett dataelement manuellt använder du klammerparentesens dataelementtokenisering för vidarebefordran av händelser. Om du vill referera till värdet för ett dataelement med namnet&quot;appSection&quot; som en nyckel eller ett värde anger du `{{appSection}}`. Du kan också markera det dataelement som skapades tidigare genom att markera det i listrutan. Du kan lägga till ett eller flera dataelement.

### Avancerat

Åtgärder i regler för vidarebefordran av händelser utförs sekventiellt. Det kan finnas situationer där du vill hämta data från en extern källa som inte finns i den inkommande händelsen från klienten och sedan ta detta svar och antingen omvandla eller skicka dessa data till ett slutmål i en efterföljande åtgärd i en enda regel. Det här aktiveras av&quot;Spara begäransvaret&quot; i det avancerade avsnittet.

Om du vill spara svarstexten från en slutpunkt ska du kontrollera **[!UICONTROL Save the request response]** och definiera en svarsnyckel i textfältet.

Om du har definierat svarsnyckeln som `productDetails`refererar du till dessa data i ett dataelement och refererar sedan detta dataelement i en efterföljande åtgärd i samma regel. Skapa ett dataelement som refererar `productDetail`, skapa ett dataelement av typen `path` och ange följande sökväg:

```Json
arc.ruleStash.[EXTENSION-NAME-HERE].responses.[RESPONSE-KEY-HERE] 

arc.ruleStash.adobe-cloud-connector.reponses.productDetails 
```
