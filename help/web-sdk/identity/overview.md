---
title: Identitetsdata i Web SDK
description: Lär dig hur du hämtar och hanterar Adobe Experience Cloud ID:n (ECID) med Adobe Experience Platform Web SDK.
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 3724c43090e37d21384e9dfe45e60ee2eec68a81
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 0%

---


# Identitetsdata i Web SDK

Adobe Experience Platform Web SDK använder [Adobe Experience Cloud ID:n (ECID)](../../identity-service/features/ecid.md) för att spåra besökares beteende. Om du använder [!DNL ECIDs] kan du se till att varje enhet har en unik identifierare som kan finnas kvar i flera sessioner och koppla alla träffar som inträffar under och mellan webbsessioner till en viss enhet.

Det här dokumentet innehåller en översikt över hur du hanterar [!DNL ECIDs] och [!DNL CORE IDs] med Web SDK.

## Spåra ECID:n med Web SDK {#tracking-ecids-web-sdk}

SDK tilldelar och spårar [!DNL ECIDs] med hjälp av cookies, med flera tillgängliga metoder för att konfigurera hur dessa cookies genereras.

När en ny användare kommer till din webbplats försöker [Adobe Experience Cloud Identity Service](../../identity-service/home.md) att ange en cookie för enhetsidentifiering för den användaren.

* För förstagångsbesökare genereras en [!DNL ECID] och returneras i det första svaret från Experience Platform Edge Network.
* För återkommande besökare hämtas [!DNL ECID] från cookien `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` och läggs till i nyttolasten för begäran av Edge Network.

När cookie-filen som innehåller [!DNL ECID] har ställts in, kommer varje efterföljande begäran som skapas av Web SDK att innehålla en kodad [!DNL ECID] i `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity`-cookien.

När du använder cookies för enhetsidentifiering har du två sätt att interagera med Edge Network:

1. Skapa en CNAME på din egen domän som pekar på `adobedc.net`. Den här metoden kallas för [första parts datainsamling](#first-party).
1. Skicka data direkt till Edge Network-domänen `adobedc.net`. Den här metoden kallas [tredjepartsdatainsamling](#third-party).

Som förklaras i avsnitten nedan har den datainsamlingsmetod som du väljer att använda en direkt inverkan på cookie-livstiden i olika webbläsare.

## Spåra CORE ID:n med Web SDK {#tracking-coreid-web-sdk}

När du använder Google Chrome med cookies från tredje part aktiverade och det inte finns någon cookie för `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` går den första Edge Network-begäran igenom en `demdex.net`-domän, som ställer in en demonstrationscookie. Den här cookien innehåller en [!DNL CORE ID]. Detta är ett unikt användar-ID, som skiljer sig från [!DNL ECID].

Beroende på implementeringen kan du vilja [komma åt  [!DNL CORE ID]](#retrieve-coreid).

### Insamling av data från första part {#first-party}

Första parts datainsamling innebär att ange cookies via en `CNAME` på din egen domän som pekar på `adobedc.net`.

Webbläsare har långa behandlade cookies som anges av `CNAME` slutpunkter på ungefär samma sätt som de som anges av webbplatsägda slutpunkter, men de senaste ändringar som implementeras av webbläsare har gjort skillnad i hur `CNAME` cookies hanteras. Det finns inga webbläsare som blockerar cookies från första part som standard, men vissa webbläsare begränsar livstiden för cookies som anges med `CNAME` till endast sju dagar.`CNAME`

### Datainsamling från tredje part {#third-party}

Insamling av data från tredje part innebär att data skickas direkt till Edge Network-domänen `adobedc.net`.

Under de senaste åren har webbläsare blivit allt mer restriktiva när det gäller hantering av cookies som fastställs av tredje parter. Vissa webbläsare blockerar cookies från tredje part som standard. Om du använder cookies från tredje part för att identifiera webbplatsbesökare är livslängden för dessa cookies nästan alltid kortare än vad som annars skulle vara tillgängligt med cookies från första part i stället. Ibland upphör en cookie från tredje part om så lite som sju dagar.

När du använder datainsamling från tredje part begränsar vissa annonsblockerare dessutom trafiken till slutpunkterna för datainsamling i Adobe helt och hållet.

### Effekter av livscykeln för cookies i Adobe Experience Cloud-program {#lifespans}

Oavsett om du väljer datainsamling från första part eller från tredje part har den tid en cookie kan finnas kvar en direkt inverkan på besökarantal i [Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics) och [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/customer-journey-analytics). Slutanvändare kan även uppleva inkonsekventa personaliseringsupplevelser när [Adobe Target](https://experienceleague.adobe.com/en/docs/target) eller [Offer decisioning](https://experienceleague.adobe.com/en/docs/target/using/integrate/ajo/offer-decision) används på webbplatsen.

Tänk dig till exempel en situation där du har skapat en personaliseringsupplevelse som befordrar ett objekt till hemsidan om en användare har visat det tre gånger under de senaste sju dagarna.

Om en slutanvändare besöker webbplatsen tre gånger i veckan och sedan inte återvänder till webbplatsen på sju dagar, kan den användaren betraktas som en ny användare när han eller hon kommer tillbaka till webbplatsen, eftersom deras cookies kan ha tagits bort av en webbläsarprincip (beroende på vilken webbläsare användaren använde när han eller hon besökte webbplatsen). Om detta händer behandlar analysverktyget besökaren som en ny användare trots att de besökte webbplatsen för bara lite över sju dagar sedan. Alla försök att personalisera upplevelsen för användaren börjar också om.

### Enhets-ID:n för första part (FPID:n) {#fpid}

Om du vill ta hänsyn till effekterna av cookie-livscykler enligt ovan kan du välja att ställa in och hantera dina egna enhetsidentifierare i stället. Mer information finns i handboken om [enhets-ID:n från första part](./first-party-device-ids.md).

## Hämta ECID och region för den aktuella användaren {#retrieve-ecid}

Beroende på ditt användningssätt kan du komma åt [!DNL ECID] på två sätt:

* [Hämta  [!DNL ECID] via datainställning för datainsamling](#retrieve-ecid-data-prep): Det här är den rekommenderade metoden som du bör använda.
* [Hämta  [!DNL ECID]  via `getIdentity()`-kommandot ](#retrieve-ecid-getidentity): Använd bara den här metoden när du behöver [!DNL ECID]-informationen på klientsidan.

### Hämta [!DNL ECID] via datapresten för datainsamling {#retrieve-ecid-data-prep}

Använd [Dataprep för datainsamling](../../datastreams/data-prep.md) för att mappa [!DNL ECID] till ett [!DNL XDM]-fält. Det här är det rekommenderade sättet att komma åt [!DNL ECID].

Om du vill göra det anger du följande sökväg i källfältet:

```js
xdm.identityMap.ECID[0].id
```

Ange sedan målfältet till en XDM-sökväg där fältet är av typen `string`.

![](../../tags/extensions/client/web-sdk/assets/access-ecid-data-prep.png)


### Hämta [!DNL ECID] via kommandot `getIdentity()` {#retrieve-ecid-getidentity}

>[!IMPORTANT]
>
>Du bör bara hämta ECID via kommandot `getIdentity()` om du kräver [!DNL ECID] på klientsidan. Om du bara vill mappa ECID till ett XDM-fält använder du [Dataprep för datainsamling](#retrieve-ecid-data-prep) i stället.

Om du vill hämta det unika ECID:t för den aktuella besökaren använder du kommandot `getIdentity`. För förstagångsbesökare som inte har [!DNL ECID] än genererar det här kommandot en ny [!DNL ECID]. `getIdentity` returnerar också region-ID:t för besökaren.

>[!NOTE]
>
>Den här metoden används vanligtvis med anpassade lösningar som kräver att du läser [!DNL Experience Cloud]-ID:t eller behöver ett platstips för Adobe Audience Manager. Den används inte av en standardimplementering.

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

## Hämta CORE ID för den aktuella användaren {#retrieve-coreid}

Om du vill hämta CORE-ID:t för en användare kan du använda kommandot [`getIdentity()`](../commands/getidentity.md) enligt nedan.

```js
alloy("getIdentity",{
  "namespaces": ["CORE"]
});
```


## Använder `identityMap` {#using-identitymap}

Med hjälp av ett XDM [`identityMap`-fält ](../../xdm/schema/composition.md#identityMap) kan du identifiera en enhet/användare med flera identiteter, ange deras autentiseringstillstånd och avgöra vilken identifierare som betraktas som den primära. Om ingen identifierare har angetts som `primary` blir standardvärdet `ECID`.

`identityMap` fält uppdateras med kommandot `sentEvent`.

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


Varje egenskap i `identityMap` representerar identiteter som tillhör ett visst [identitetsnamnområde](../../identity-service/features/namespaces.md). Egenskapsnamnet ska vara identitetsnamnutrymmessymbolen, som du hittar i Adobe Experience Platform-användargränssnittet under [!UICONTROL Identities]. Egenskapsvärdet ska vara en array med identiteter som gäller det identitetsnamnutrymmet.

>[!IMPORTANT]
>
>Det namnområdes-ID som skickades i `identityMap` är skiftlägeskänsligt. Se till att använda rätt namnområdes-ID för att undvika ofullständig datainsamling.

Varje identitetsobjekt i identitetsarrayen innehåller följande egenskaper:

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `id` | Sträng | **(Obligatoriskt)** Det ID som du vill ange för det angivna namnområdet. |
| `authenticatedState` | Sträng | **(Obligatoriskt)** Autentiseringstillståndet för ID:t. Möjliga värden är `ambiguous`, `authenticated` och `loggedOut`. |
| `primary` | Boolean | Avgör om den här identiteten ska användas som ett primärt fragment i profilen. Som standard anges ECID som användarens primära identifierare. Om det utelämnas blir det här värdet som standard `false`. |

Om du använder fältet `identityMap` för att identifiera enheter eller användare får du samma resultat som om du använder metoden [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html) från metoden [!DNL ID Service API]. Mer information finns i [API-dokumentationen för ID-tjänsten](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html).

## Migrera från Visitor API till ECID {#migrating-visitor-api-ecid}

När du migrerar från med Visitor API kan du även migrera befintliga AMCV-cookies. Om du vill aktivera ECID-migrering anger du parametern `idMigrationEnabled` i konfigurationen. ID-migrering aktiverar följande användningsfall:

* När vissa sidor i en domän använder Visitor API och andra sidor använder denna SDK. Som stöd för detta fall läser SDK befintliga AMCV-cookies och skriver en ny cookie med befintligt ECID. Dessutom skriver SDK AMCV-cookies så att efterföljande sidor som är instrumenterade med Visitor API har samma ECID om ECID hämtas först på en sida som är instrumenterad med SDK.
* När Adobe Experience Platform Web SDK är konfigurerat på en sida som även har Visitor API. Om AMCV-cookien inte är inställd söker SDK efter besökar-API:t på sidan och anropar den för att hämta ECID.
* När hela webbplatsen använder Adobe Experience Platform Web SDK och saknar Visitor-API är det bra att migrera ECID:n så att den returnerade besökarinformationen bevaras. När SDK har distribuerats med `idMigrationEnabled` en tid så att de flesta besöks-cookies migreras, kan inställningen inaktiveras.

### Uppdaterar egenskaper för migrering

När XDM-formaterade data skickas till Audience Manager måste dessa data konverteras till signaler vid migrering. Dina egenskaper måste uppdateras för att återspegla de nya nycklarna som finns i XDM. Den här processen blir enklare om du använder [BAAAM-verktyget](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) som Audience Manager har skapat.

## Använd vid vidarebefordran av händelse

Om du för närvarande har [vidarebefordring av händelser](../../tags/ui/event-forwarding/overview.md) aktiverat och använder `appmeasurement.js` och `visitor.js` kan du behålla funktionen för vidarebefordran av händelser aktiverad och detta orsakar inga problem. På baksidan hämtar Adobe alla AAM segment och lägger till dem i anropet till Analytics. Om anropet till Analytics innehåller dessa segment kommer Analytics inte att anropa Audience Manager för att vidarebefordra data, så det finns ingen dubbel datainsamling. Du behöver heller inte använda platstips när du använder Web SDK eftersom samma segmenteringsslutpunkter anropas i serverdelen.
