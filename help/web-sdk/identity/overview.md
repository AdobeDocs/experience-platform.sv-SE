---
title: Identitetsdata i Web SDK
description: Lär dig hur du hämtar och hanterar Adobe Experience Cloud ID:n (ECID) med Adobe Experience Platform Web SDK.
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: b8c38108e7481a5c4e94e4122e0093fa6f00b96c
workflow-type: tm+mt
source-wordcount: '1480'
ht-degree: 0%

---

# Identitetsdata i Web SDK

Adobe Experience Platform Web SDK använder [Adobe Experience Cloud ID (ECID)](../../identity-service/features/ecid.md) för att spåra besökares beteende. Med hjälp av ECID:n kan du se till att varje enhet har en unik identifierare som kan finnas kvar i flera sessioner och koppla alla träffar som inträffar under och mellan webbsessioner till en viss enhet.

I det här dokumentet finns en översikt över hur du hanterar ECID:n med Platform Web SDK.

## Spåra ECID:n med SDK

Platform Web SDK tilldelar och spårar ECID:n med hjälp av cookies, med flera tillgängliga metoder för att konfigurera hur dessa cookies genereras.

När en ny användare kommer till din webbplats försöker Adobe Experience Cloud Identity Service att ange en cookie för enhetsidentifiering för den användaren. För förstagångsbesökare genereras ett ECID som returneras i det första svaret från Adobe Experience Platform Edge Network. För återkommande besökare hämtas ECID från `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` cookie och har lagts till i nyttolasten av Edge Network.

När cookie-filen som innehåller ECID har ställts in innehåller varje efterföljande begäran som genererats av Web SDK ett kodat ECID i `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` cookie.

När du använder cookies för enhetsidentifiering har du två alternativ för att interagera med Edge Network:

1. Skicka data direkt till Edge Network `adobedc.net`. Den här metoden kallas [datainsamling från tredje part](#third-party).
1. Skapa en CNAME på din egen domän som pekar på `adobedc.net`. Den här metoden kallas [datainsamling från första part](#first-party).

Som förklaras i avsnitten nedan har den datainsamlingsmetod som du väljer att använda en direkt inverkan på cookie-livstiden i olika webbläsare.

### Datainsamling från tredje part {#third-party}

Insamling av data från tredje part innebär att data skickas direkt till Edge Network-domänen `adobedc.net`.

Under de senaste åren har webbläsare blivit allt mer restriktiva när det gäller hantering av cookies som fastställs av tredje part. Vissa webbläsare blockerar cookies från tredje part som standard. Om du använder cookies från tredje part för att identifiera webbplatsbesökare är livslängden för dessa cookies nästan alltid kortare än vad som annars skulle vara tillgängligt med cookies från första part i stället. Ibland upphör en cookie från tredje part om så lite som sju dagar.

När datainsamling från tredje part används begränsar vissa annonsblockerare dessutom trafiken till slutpunkterna för datainsamling i Adobe helt och hållet.

### Insamling av data från första part {#first-party}

Första parts datainsamling innebär att cookies ställs in via en CNAME på din egen domän som pekar på `adobedc.net`.

Webbläsare har långa behandlade cookies som anges av CNAME-slutpunkter på ungefär samma sätt som de som anges av webbplatsägda slutpunkter, men de senaste ändringarna som implementeras av webbläsare har gjort en skillnad i hur CNAME-cookies hanteras. Det finns inga webbläsare som blockerar CNAME-cookies från första part som standard, men vissa webbläsare begränsar livstiden för cookies som anges med CNAME till endast sju dagar.

### Effekter av livscykeln för cookies i Adobe Experience Cloud-program {#lifespans}

Oavsett om du väljer datainsamling från första part eller från tredje part har den tid en cookie kan finnas kvar en direkt inverkan på antalet besökare i Adobe Analytics och Customer Journey Analytics. Slutanvändare kan dessutom uppleva inkonsekventa personaliseringsupplevelser när Adobe Target eller Offer decisioning används på webbplatsen.

Tänk dig till exempel en situation där du har skapat en personaliseringsupplevelse som befordrar ett objekt till hemsidan om en användare har visat det tre gånger under de senaste sju dagarna.

Om en slutanvändare besöker webbplatsen tre gånger i veckan och sedan inte återvänder till webbplatsen på sju dagar, kan den användaren betraktas som en ny användare när han eller hon kommer tillbaka till webbplatsen, eftersom deras cookies kan ha tagits bort av en webbläsarprincip (beroende på vilken webbläsare användaren använde när han eller hon besökte webbplatsen). Om detta inträffar behandlar analysverktyget besökaren som en ny användare även om de besökte webbplatsen för bara drygt sju dagar sedan. Alla försök att personalisera upplevelsen för användaren börjar också om.

### Enhets-ID:n från första part

Om du vill ta hänsyn till effekterna av cookie-livscykler enligt ovan kan du välja att ställa in och hantera dina egna enhetsidentifierare i stället. Se guiden på [enhets-ID:n från första part](./first-party-device-ids.md) för mer information.

## Hämta ECID och region för den aktuella användaren {#retrieve-ecid}

Beroende på ditt sätt att arbeta finns det två sätt att komma åt [!DNL ECID]:

* [Hämta [!DNL ECID] via Data Prep för datainsamling](#retrieve-ecid-data-prep): Det här är den rekommenderade metod som du bör använda.
* [Hämta [!DNL ECID] via `getIdentity()` kommando](#retrieve-ecid-getidentity): Använd bara den här metoden när du behöver [!DNL ECID] information på klientsidan.

### Hämta [!DNL ECID] via Data Prep för datainsamling {#retrieve-ecid-data-prep}

Använd [Dataförberedelse för datainsamling](../../datastreams/data-prep.md) för att mappa [!DNL ECID] till [!DNL XDM] fält. Det här är det rekommenderade sättet att komma åt [!DNL ECID].

Om du vill göra det anger du följande sökväg i källfältet:

```js
xdm.identityMap.ECID[0].id
```

Ställ sedan in målfältet på en XDM-sökväg där fältet är av typen `string`.

![](../../tags/extensions/client/web-sdk/assets/access-ecid-data-prep.png)


### Hämta [!DNL ECID] via `getIdentity()` kommando {#retrieve-ecid-getidentity}


>[!IMPORTANT]
>
>Du bör bara hämta ECID via `getIdentity()` om du behöver [!DNL ECID] på klientsidan. Om du bara vill mappa ECID till ett XDM-fält använder du [Dataförberedelse för datainsamling](#retrieve-ecid-data-prep) i stället.

Om du vill hämta den aktuella besökarens unika ECID använder du `getIdentity` -kommando. För förstagångsbesökare som inte har [!DNL ECID] ännu skapar det här kommandot ett nytt [!DNL ECID]. `getIdentity` returnerar också region-ID för besökaren.

>[!NOTE]
>
>Den här metoden används vanligtvis med anpassade lösningar som kräver att [!DNL Experience Cloud] ID eller behöver ett platstips för Adobe Audience Manager. Den används inte av en standardimplementering.

```javascript
alloy("getIdentity")
  .then(function(result) {
    // The command succeeded.
    console.log("ECID:", result.identity.ECID);
    console.log("RegionId:", result.edge.regionId);
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information.
  });
```

## Använda `identityMap` {#using-identitymap}

Använda en XDM [`identityMap` fält](../../xdm/schema/composition.md#identityMap)kan du identifiera en enhet/användare med flera identiteter, ange deras autentiseringstillstånd och avgöra vilken identifierare som ska vara den primära. Om ingen identifierare har angetts som `primary`, blir det primära standardvärdet `ECID`.

`identityMap` fälten uppdateras med `sentEvent` -kommando.

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "authenticated",
          "primary": true
        }
      ]
    }
  }
});
```

>[!NOTE]
>
>Adobe rekommenderar att du skickar namnutrymmen som representerar en person, till exempel `CRMID`, som primär identitet.


Varje egenskap i `identityMap` representerar identiteter som tillhör en viss [namnutrymme för identitet](../../identity-service/features/namespaces.md). Egenskapsnamnet ska vara identitetssymbolen för namnutrymmet, som du hittar i användargränssnittet i Adobe Experience Platform under &quot;[!UICONTROL Identities]&quot;. Egenskapsvärdet ska vara en array med identiteter som gäller det identitetsnamnutrymmet.

>[!IMPORTANT]
>
>Det namnområdes-ID som skickades i `identityMap` är skiftlägeskänsligt. Se till att använda rätt namnområdes-ID för att undvika ofullständig datainsamling.

Varje identitetsobjekt i identitetsarrayen innehåller följande egenskaper:

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `id` | Sträng | **(Obligatoriskt)** Det ID som du vill ange för det angivna namnutrymmet. |
| `authenticationState` | Sträng | **(Obligatoriskt)** Autentiseringstillståndet för ID:t. Möjliga värden är `ambiguous`, `authenticated`och `loggedOut`. |
| `primary` | Boolean | Avgör om den här identiteten ska användas som ett primärt fragment i profilen. Som standard anges ECID som användarens primära identifierare. Om det utelämnas används standardvärdet `false`. |

Använda `identityMap` fält för att identifiera enheter eller användare leder till samma resultat som om du använder [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html) metoden från [!DNL ID Service API]. Se [API-dokumentation för ID-tjänst](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html) för mer information.

## Migrera från Visitor API till ECID

När du migrerar från med Visitor API kan du även migrera befintliga AMCV-cookies. Om du vill aktivera ECID-migrering anger du `idMigrationEnabled` -parametern i konfigurationen. ID-migrering aktiverar följande användningsfall:

* När vissa sidor i en domän använder Visitor API och andra sidor använder denna SDK. Som stöd för detta fall läser SDK befintliga AMCV-cookies och skriver en ny cookie med befintligt ECID. Dessutom skriver SDK AMCV-cookies så att efterföljande sidor som är instrumenterade med Visitor API har samma ECID om ECID hämtas först på en sida som är instrumenterad med SDK.
* När Adobe Experience Platform Web SDK har konfigurerats på en sida som även har Visitor API. Om AMCV-cookien inte är inställd söker SDK efter besökar-API:t på sidan och anropar den för att hämta ECID.
* När hela webbplatsen använder Adobe Experience Platform Web SDK och inte har något Visitor-API är det bra att migrera ECID:n så att den returnerade besökarinformationen behålls. När SDK har distribuerats med `idMigrationEnabled` så att de flesta besökarnas cookies migreras kan inställningen inaktiveras.

### Uppdaterar egenskaper för migrering

När XDM-formaterade data skickas till Audience Manager måste dessa data konverteras till signaler vid migrering. Dina egenskaper måste uppdateras för att återspegla de nya nycklarna som finns i XDM. Den här processen blir enklare om du använder [BAAAM-verktyget](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) som Audience Manager har skapat.

## Använd vid vidarebefordran av händelse

Om du har [händelsevidarebefordran](../../tags/ui/event-forwarding/overview.md) aktiverat och använder `appmeasurement.js` och `visitor.js`kan du behålla funktionen för vidarebefordran av händelser aktiverad och detta kommer inte att orsaka några problem. På baksidan hämtar Adobe alla AAM segment och lägger till dem i anropet till Analytics. Om anropet till Analytics innehåller dessa segment kommer Analytics inte att anropa Audience Manager för att vidarebefordra data, så det finns ingen dubbel datainsamling. Du behöver heller inte använda platstips när du använder Web SDK eftersom samma segmenteringsslutpunkter anropas i serverdelen.
